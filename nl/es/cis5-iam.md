---


copyright:
  years: 2018
lastupdated: "2018-07-27"


---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:download: .download}

# Paso 4: Desarrollo de un flujo de autenticación

Cuando definió la oferta, la consola de gestión de recursos, página **Gestión de acceso**, le proporcionó un ID de cliente y un secreto de IAM (Identity and Access Management) de {{site.data.keyword.Bluemix_notm}}, un ID de servicio y una clave de API. Ahora es el momento de utilizar estos valores para llevar a cabo los pasos siguientes:

1. Obtener el URI de redirección en función de su manejo de `dashboard_url`, volver a la consola de gestión de recursos y añadirlo al separador IAM, asegurándose de que actualiza el ID de cliente.
2. Desarrollar el flujo de OAuth para la autenticación. Utilizará los URI de redirección, el ID de cliente y el secreto de cliente como parámetros para las API Rest de IAM `token_endpoint` para completar este flujo.
3. Validar la autorización de usuario:
   1. Comuníquese con IAM para obtener una señal de acceso de la clave de API
   2. Valide la autorización del usuario en el panel de control de servicio mediante `authorization_endpoint` (/v2/authz POST)

En este paso se presupone que se ha aprobado que suministre un servicio de facturación integrado. Si aún no ha realizado el proceso de registro y aprobación inicial en PWB, consulte [Cómo comenzar a publicar su oferta de terceros en {{site.data.keyword.Bluemix_notm}}](/docs/third-party/index.html)
{: tip}

## Antes de empezar

Asegúrese de que ha comenzado el paso 1 y ha completado los pasos 2 y 3:
1. [Crear documentación del servicio y anuncio de marketing](/docs/third-party/cis1-docs-marketing.html).
2. [Definir su oferta en la consola de gestión de recursos](/docs/third-party/cis2-rmc-define.html).
3. [Desarrollar y alojar sus intermediarios de servicio](/docs/third-party/cis3-broker.html).


## Obtenga su URI de redirección de IAM (consola de gestión de recursos: página IAM)

Cuando definió el servicio en la consola de gestión de recursos, generó un ID de cliente, pero tenga en cuenta que probablemente no tenía un URI de redirección en ese momento. Esto significa que IAM ha creado un ID de cliente que se ha establecido en "false". No tendrá un verdadero ID de cliente hasta que vuelva a la consola de gestión de recursos con su URI de redirección.

La buena noticia es que, en el paso de desarrollo anterior, ha desarrollado un OSB y lo ha alojado (probablemente haya visto valores de IAM en el código de intermediario de ejemplo). El valor `redirect_uri` suele ser el url del host en el que reside la app con algún url adicional que manejará la autenticación y la autorización.

 A continuación se muestran algunos URI de redirección de ejemplo

```
https://myapp.bluemix.net/integrate/auth/callback
http://localhost:3000/auth/callback <-- for testing locally
```

Vuelva a la consola de gestión de recursos y añada el URI de redirección en el separador IAM:

1. Inicie una sesión en la consola
2. Seleccione su URI de redirección
3. Vuelva a la consola de gestión de recursos
4. En el **separador IAM**, pegue el URI de redirección en el campo **URI de redirección**.
5. Pulse **Actualizar ID de cliente** para actualizar su ID de cliente.

Ahora debería tener un ID de cliente que entiende el URI de redirección y que está establecido en "true". Puede utilizar dicho ID de cliente en los pasos siguientes para desarrollar el flujo de OAuth.

## Desarrolle el flujo de OAuth para la autenticación
{: #oauth}


**Autenticación - Paso 0:** busque el punto final regional de IAM correspondiente al inicio de sesión en la interfaz de usuario que esté más cerca de la aplicación desplegado; para ello realice una llamada a `https://iam.bluemix.net/identity/.well-known/openid-configuration`.

```
curl -X GET \
  https://iam.bluemix.net/identity/.well-known/openid-configuration
```

```
HTTP/1.1 200 OK
Content-Type: application/json
{
  "issuer": "https://iam.bluemix.net/identity",
  "authorization_endpoint": "https://iam-region2.bluemix.net/identity/authorize",
  "token_endpoint": "https://iam-region2.bluemix.net/identity/token",
...
}
```

Esta solicitud se puede realizar una vez cuando se inicia la aplicación y de nuevo si `authorization_endpoint` falla. Debería poder almacenar en memoria caché el valor de `authorization_endpoint` durante un breve periodo de tiempo y renovar una vez que haya caducado la memoria caché o se haya encontrado un error.


**Autenticación - Paso 1:** cuando un usuario vaya a su `dashboard_url`, redirija el navegador a `<authorization_endpoint>?client_id=<your-client-id>&redirect_uri=<your-redirect-uri>&response-type=code&state=<your-resource-instance-id>`


-> aparecerá la solicitud de inicio de sesión

-> el usuario especifica las credenciales

-> devolución de llamada del navegador para redirigir al uri proporcionando un parámetro de respuesta "code" y un valor "state"


**Autenticación - Paso 2:** intercambie el código para una llamada de señal de acceso

### PUBLIQUE (POST) <token_endpoint>

#### Cabeceras:
{: #headers1}

  - Authorization: Basic *[client id]: [client secret]*
  - Content-Type: application/x-www-form-urlencoded
  - Accept: application/json

#### Con los parámetros:
{: #parameters1}

  - client_id=*[id cliente]*
  - client_secret=*[secreto cliente]*
  - grant_type=authorization_code
  - response_type=cloud_iam
  - redirect_uri=*[mismo uri que redirect_uri del paso 1]*
  - code=*[código de la devolución de llamada]*

```
curl -k -X POST \
  -u "<your-client-id>:<your-client-secret>" \
  -H "Content-Type: application/x-www-form-urlencoded" \
  -H "Accept: application/json" \
  --data-urlencode "client_id=<your-client-id>" \
  --data-urlencode "client_secret=<your-client-secret>" \
  --data-urlencode "grant_type=authorization_code" \
  --data-urlencode "response_type=cloud_iam" \
  --data-urlencode "code=<code-from-the-callback>" \
  --data-urlencode "redirect_uri=<redirect_uri>" \
  "https://iam-region2.bluemix.net/identity/token"
```
{: codeblock}

### Respuesta:
{: #response1}

```
{
  "access_token": "eyJraWQiOiI......XmpBTIDdR5w",
  "refresh_token": "SPrXw5tBE3......KBQ+luWQVY=",
  "token_type": "Bearer",
  "expires_in": 3600,
  "expiration": 1473188353
}
```
{: codeblock}

  Asegúrese de almacenar el valor de access_token del usuario devuelto en esta respuesta, ya que se utilizará a continuación durante la autorización del usuario.

Consulte el ejemplo de nuestros intermediarios de ejemplo: https://github.com/IBM/sample-resource-service-brokers

## Ahora es el momento de validar la autorización de usuario
{: #validate}

1. Comuníquese con IAM para obtener una señal de acceso para una clave de API
2. Valide la autorización del usuario en la instancia de servicio (/v2/authz POST)

### Autorización - Paso 1: obtenga una señal de IAM de {{site.data.keyword.Bluemix_notm}} utilizando una clave de API.
{: #iam_token_using_api_key}

### POST /identidad/señal

#### Cabeceras:
{: #headers2}

  - Authorization: Basic *[client id]: [client secret]*
  - Content-Type: application/x-www-form-urlencoded
  - Accept: application/json

#### Con los parámetros:
{: #parameters2}

  - grant_type=urn:ibm:params:oauth:grant-type:apikey
  - response_type=cloud_iam
  - apikey=*[clave API]*

```
curl -k -X POST \
  -H "Content-Type: application/x-www-form-urlencoded" \
  -H "Accept: application/json" \
  --data-urlencode "grant_type=urn:ibm:params:oauth:grant-type:apikey" \
  --data-urlencode "response_type=cloud_iam" \
  --data-urlencode "apikey=<apikey>" \
  "https://iam-region2.bluemix.net/identity/token"
```
{: codeblock}

### Respuesta:
{: #response2}

```
{
  "access_token": "eyJhbGciOiJIUz......sgrKIi8hdFs",
  "refresh_token": "SPrXw5tBE3......KBQ+luWQVY=",
  "token_type": "Bearer",
  "expires_in": 3600,
  "expiration": 1473188353
}
```
{: codeblock}

**Nota:** esta señal es válida durante una hora y se puede volver a utilizar tantas veces como sea necesario durante el intervalo de tiempo de una hora. Se recomienda encarecidamente almacenar esta señal en memoria caché para evitar realizar esta solicitud para cada acceso a `dashboard_url`.


### Autorización - Paso 2: valide la autorización del usuario en la instancia de servicio (/v2/authz POST)

Ahora que hemos autenticado al usuario y que tenemos nuestra propia señal de acceso, tenemos que comprobar que el usuario tiene la capacidad de acceder al panel de control del servicio. En primer lugar, necesitaremos algunos fragmentos de información incluidos en la señal de acceso del usuario, que decodificaremos en el paso 2.1. A continuación, utilizaremos dicha información para llamar a IAM para comprobar si el usuario tiene autorización para acceder al panel de control en el paso 2.2.

**Paso 2.1**: decodifique la señal de acceso del usuario (devuelta durante ` ** Autenticación - Paso 2: ** intercambiar el código para una señal de acceso` que se encuentra más arriba).
   Se trata de una señal JWT que se puede decodificar utilizando cualquier biblioteca compatible con JWT. Por ejemplo, consulte la biblioteca que se incluye en nuestro [código de intermediario de ejemplo](https://github.com/IBM/sample-resource-service-brokers).
   Una vez decodificada la señal, el formato se muestra a continuación; tendremos que extraer los campos `iam_id` y `scope` que se utilizarán en el siguiente paso:

```
{
  "iam_id": "IBMid-XXXXXXX",
  "id": "IBMid-XXXXXXX",
  "realmid": "IBMid",
  "identifier": "XXXXXXX",
  "given_name": "Don",
  "family_name": "Quixote",
  "name": "Don Quixote",
  "email": "quixote@email.com",
  "sub": "quixote@email.com",
  "account": {
    "bss": "123123123123123"
  },
  "iat": 1522114004,
  "exp": 1522117604,
  "iss": "https://iam.bluemix.net/identity",
  "grant_type": "urn:ibm:params:oauth:grant-type:apikey",
  "scope": "openid <your serviceName>",
  "client_id": "bx",
  "acr": 1,
  "amr": [
    "pwd"
  ]
}
```

**Paso 2.2**: llame a IAM para comprobar si el usuario tiene autorización para acceder al panel de control

```
curl -X POST \
  -H "Accept: application/json" \
  -H "Authorization: <access token from step 1>" \
  -d '[ \
    { \
      "subject" : \
      { \
        "attributes": \
        { \
          "id": "<iam_id field value from user's token>", \
          "scope": "<scope field value from user's token>" \
        } \
      }, \
      "resource" : \
      { \
        "crn" : "<resource instance CRN>" \
      }, \
      action : <your service name> + ".dashboard.view" \
    } \
  ]' \
  https://iam.bluemix.net/v2/authz
```

Consulte el ejemplo de nuestros intermediarios de ejemplo: https://github.com/IBM/sample-resource-service-brokers

## Definición del ámbito de señales de {{site.data.keyword.Bluemix_notm}} Identity and Access Management para terceros
{: #token_scoping}

Las señales de acceso de usuario creadas con el ID de cliente solo se pueden utilizar para acceder a las API de servicio. Las solicitudes a otras API de nube que utilizan esta señal tendrán como resultado un acceso denegado, aunque el usuario tenga configurada una política adecuada.

Como parte de la integración de terceros, se utiliza una definición de ámbito de señales para garantizar que las señales tienen el ámbito de acceso mínimo necesario para cumplir los objetivos del usuario. Para facilitar esta tarea, las señales de IAM tendrán acceso en función del ID de cliente que ha creado la señal. Esto significa que, si un servicio de terceros ha creado una señal de IAM, un usuario final no podrá ejecutar determinadas API y funciones, aunque si el usuario tenga configurada una política adecuada.

El impacto sobre las autorizaciones (todas las llamadas a `https://iam.bluemix.net/v2/authz`) es la necesidad de pasar información de la variable `scope` en el asunto. Esta información está contenida dentro de una señal de IAM (codificada en base64) en la variable `scope`.

A continuación se muestra un ejemplo de lo que se ha añadido en la llamada de autorización:
```
  [
   {  Headers
   `Authorization` -> una señal jwt que representa el servicio de terceros y/o el panel de control
   `Transaction-ID` -> "un guid exclusivo que permite ayudar a realizar el rastreo completo de la solicitud"
   `Accept` -> `application/vnd.authz.v2+json`
   `Content-Type` -> `application/json`

      Body
      "subject":{
         "attributes":{
            "id":"IBMid-123",
            "scope":"libraryservice openid"
         }
      },
      "action":"libraryservice.books.read",
      "resource":{
         "attributes":{
            "serviceName":"libraryservice",
            "serviceInstance":"12345",
            "accountId":"123456789"
         }
      }
   }
]
```
{: codeblock}

Esto se aplica a todos los usos (`user, serviceId, crn`) y todos los `subject.attributes` necesitan un ámbito.

## Pasos siguientes

Ahora es el momento de aunar todos estos elementos. Vuelva a la consola de gestión de recursos para publicar el servicio con visibilidad limitada y para validar la oferta en el catálogo. Consulte: [Publicación y prueba del servicio](/docs/third-party/cis4-rmc-publish.html).