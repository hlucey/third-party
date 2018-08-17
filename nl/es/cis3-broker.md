---


copyright:
  years: 2018
lastupdated: "2018-06-26"


---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:download: .download}

# Paso 3: Desarrollo y alojamiento de intermediarios de servicio

Utilizando los metadatos que ha exportado desde la consola de gestión de recursos, va a crear uno o varios intermediarios de servicio nuevos en el lenguaje de programación que elija.

Los intermediarios de servicio gestionan el ciclo de vida de los servicios. La plataforma {{site.data.keyword.Bluemix_notm}} interactúa con intermediarios de servicio para suministrar y gestionar instancias de servicio (una instancia de una oferta de servicio) y enlaces de servicio (la representación de una asociación entre una aplicación y una instancia de servicio, que a menudo contiene las credenciales que utilizará la aplicación para comunicarse con la instancia de servicio). Al proporcionar valores de metadatos válidos se creará una respuesta de API RESTful correcta cuando se realice una solicitud.

Puede empezar a crear el intermediario utilizando una combinación de los metadatos que ha exportado desde la consola de gestión de recursos, nuestros ejemplos de intermediarios de servicio públicos de {{site.data.keyword.Bluemix_notm}} y la documentación de la API del intermediario de recursos. Para desarrollar el intermediario, puede:

1. Ver el escenario de suministro de nuestra plataforma
2. Consultar la especificación OSB
2. Examinar los ejemplos de intermediarios de {{site.data.keyword.Bluemix_notm}}
3. Utilizar la documentación de la API del intermediario de recursos para comprender la lógica del punto final de la API REST
4. Utilizar los metadatos que ha exportado desde la consola de gestión de recursos para informar sobre su desarrollo
5. Ver la información de intermediario que proporciona la plataforma {{site.data.keyword.Bluemix_notm}}
6. Leer las recomendaciones adicionales para optimizar su desarrollo
7. Alojar el intermediario
8. Probar el intermediario

## Antes de empezar

En este paso se presupone que se ha aprobado que suministre un servicio de facturación integrado. Si aún no ha completado el proceso de registro y aprobación inicial en Provider Workbench, consulte la [Guía de aprendizaje de iniciación](/docs/third-party/index.md).
{: tip}

Asegúrese de que ha comenzado el paso 1 y ha completado el paso 2
1. [Crear documentación del servicio y anuncio de marketing](/docs/third-party/cis1-docs-marketing.html).
2. [Definir su oferta en la consola de gestión de recursos](/docs/third-party/cis2-rmc-define.html).


## Vea nuestro caso de ejemplo de suministro de la plataforma {{site.data.keyword.Bluemix_notm}}

Va a desarrollar un Open Service Broker que funcione con la plataforma {{site.data.keyword.Bluemix_notm}}. Consulte nuestro [Caso de ejemplo de suministro](/docs/third-party/platform.html#provisioning-scenario-pulling-it-all-together) para obtener una visión general del funcionamiento del proceso de creación de recursos.

## Familiarícese con la especificación OSB

{{site.data.keyword.Bluemix_notm}} utiliza la API de la especificación Open Service Broker (OSB) `versión 2.12`. Examine y familiarícese con la [especificación de la API Open Broker](https://github.com/openservicebrokerapi/servicebroker/blob/v2.12/spec.md){: new_window} ![Icono de enlace externo](../icons/launch-glyph.svg "Icono de enlace externo") y utilice el archivo readme como guía para obtener más información.

## Vea nuestros ejemplos de intermediarios de {{site.data.keyword.Bluemix_notm}}

[https://github.com/IBM/sample-resource-service-brokers](https://github.com/IBM/sample-resource-service-brokers){: new_window} ![Icono de enlace externo](../icons/launch-glyph.svg "Icono de enlace externo")

**Nota:** no todos los lenguajes están representados mediante un ejemplo. Si necesita, por ejemplo, un ejemplo de intermediario Python, debería poder encontrar un ejemplo de Cloud Foundry buscando en Google. Es posible que tenga que ajustar este ejemplo para que se ajuste a sus requisitos de OSB.


## Vea la documentación de nuestra API de Open Service Broker de {{site.data.keyword.Bluemix_notm}}

Los intermediarios de servicio se deberían desarrollar con un cierto conocimiento de la [{{site.data.keyword.Bluemix_notm}}API de Open Service Broker](https://console.bluemix.net/apidocs/821-ibm-cloud-open-service-broker-api?&language=node#introduction){: new_window} ![Icono de enlace externo](../icons/launch-glyph.svg "Icono de enlace externo"). Familiarícese con la API de intermediario y con la forma en que interactúa con el intermediario o los intermediarios.

{{site.data.keyword.Bluemix_notm}} Open Service Broker amplía la especificación Open Service Broker 2.12.
{: tip}

### Lógica de punto final necesaria para todos los intermediarios de servicio

Los intermediarios de servicio deben proporcionar un conjunto estándar de valores de metadatos que consumen las API REST, y los intermediarios de {{site.data.keyword.Bluemix_notm}} deben contener lógica para los siguientes puntos finales/vías de acceso de la API REST:

<dl>
  <dt>catálogo (GET)</dt>
  <dd>Devuelve los metadatos de catálogo incluidos en el intermediario. Hay muchos valores de metadatos de catálogo adicionales que no se devuelven; estos valores se añaden exclusivamente en la consola de gestión de recursos y se almacenan en el catálogo de {{site.data.keyword.Bluemix_notm}}.</dd>
  <dt>instancias de recursos (PUT)</dt>
  <dd>Suministra la instancia de servicio</dd>
  <dt>instancias de recursos (DELETE)</dt>
  <dd>Anula el suministro de la instancia de servicio.</dd>
  <dt>instancias de recursos (PATCH)</dt>
  <dd>Actualiza la instancia de servicio.</dd>
</dl>

**Nota sobre el catálogo (GET)**: este punto final define el contrato entre el intermediario y la plataforma {{site.data.keyword.Bluemix_notm}} en lo que respecta a los servicios y planes a los que el intermediario da soporte. Este punto final devuelve los metadatos de catálogo almacenados en el intermediario. Estos valores definen el contrato de suministro mínimo entre el servicio y la plataforma {{site.data.keyword.Bluemix_notm}}. Todos los metadatos de catálogo adicionales que no son obligatorios para el suministro se almacenan en el catálogo de {{site.data.keyword.Bluemix_notm}}, y las actualizaciones de los valores de visualización del catálogo que se utilizan para representar el panel de control como enlaces, iconos y metadatos convertidos i18n, se deben actualizar en la consola de gestión de recursos (y no alojarse en el intermediario). Ninguno de los metadatos que se almacenan en el intermediario se visualiza en la consola de {{site.data.keyword.Bluemix_notm}} ni en la CLI de {{site.data.keyword.Bluemix_notm}}; la consola y la CLI devolverán lo que se ha establecido en la consola de gestión de recursos y se ha almacenado en el catálogo de {{site.data.keyword.Bluemix_notm}}. Estos son los valores mínimos necesarios que debe devolver el catálogo (GET):

```
{
       "services": [{
           "id": "ibmcloud-link",
           "name": "ibmcloud-link",
           "description": "An IBM provided service that enables aliasing to service instances in the {{site.data.keyword.Bluemix_notm}}.",
           "bindable": true,
           "plan_updateable": false,
           "plans": [
               {
                   "id": "ibmcloud-link-alias",
                   "name": "ibmcloud-alias",
                   "free": true,
                   "description": "The {{site.data.keyword.Bluemix_notm}} alias plan used for linking."
               }
               ]
       }]
}
```

### Lógica de los puntos finales necesarios para servicios que se pueden enlazar

Si mi servicio se puede enlazar a aplicaciones en {{site.data.keyword.Bluemix_notm}}, debe poder devolver los puntos finales de la API y las credenciales a los consumidores del servicio. Un servicio que se puede enlazar debe utilizar las operaciones enlazables de la especificación Open Service Broker y debe utilizar los siguientes puntos finales/vías de acceso:

<dl>
  <dt>enlaces y credenciales (PUT)</dt>
  <dd>Enlaza la instancia de servicio a una aplicación.</dd>
  <dt>enlaces y credenciales (DEL)</dt>
  <dd>Anula en enlace de la instancia de servicio de una aplicación.</dd>
</dl>

### Puntos finales necesarios de extensión de {{site.data.keyword.Bluemix_notm}}

La especificación OSB *no* da soporte a un estado de instancia inhabilitada, pero aún no suprimida. Para que {{site.data.keyword.Bluemix_notm}} dé soporte a los clientes que puedan experimentar un vencimiento de facturación u otra situación que pueda dar lugar a la suspensión de la cuenta (pero no cancelación), {{site.data.keyword.Bluemix_notm}} ha definido puntos finales de API ampliados que permiten inhabilitar y volver a habilitar instancias de servicio. Las siguientes extensiones de punto final son **obligatorias**:

<dl>
  <dt>habilitar e inhabilitar instancias (GET)</dt>
  <dd>Estado: devuelve el estado de la instancia de servicio.</dd>
  <dt>habilitar e inhabilitar instancias (PUT)</dt>
  <dd>Le permite habilitar o inhabilitar una instancia de servicio.</dd>
</dl>

** Nota **: es responsabilidad del proveedor del servicio inhabilitar el acceso a la instancia de servicio cuando se invoca una inhabilitación del punto final y volver a habilitar dicho acceso cuando se invoca una habilitación del punto final.

## Cómo utilizar los metadatos exportados como guía en el desarrollo del intermediario

Los metadatos que ha exportado desde la consola de gestión de recursos se pueden utilizar como guía para desarrollar su propio intermediario. No todos los valores que ha especificado en la consola de gestión de recursos son obligatorios para suministrar un servicio. Los metadatos que ha exportado desde la consola de gestión de recursos definen el contrato de suministro mínimo entre el servicio y la plataforma {{site.data.keyword.Bluemix_notm}}. El archivo json exportado debe suministrar los siguientes valores:

```
{
services :
            [
                {
                    bindable         : true,
                    description      : "Test Node Resource Service Broker Description",
                    // TODO - GUID generated by http://www.guidgenerator.com
                    // TODO - This service id must be unique within an IBM Cloud environment's set of service offerings
                    id               : "df35cab6-347b-4ba5-8f39-e9c23a237f5b",
                    metadata         :
                    {
                        displayName         : "Test Node Resource Service Broker Display Name",
                        documentationUrl    : baseMetadataUrl + "documentation.html",
                        imageUrl            : baseMetadataUrl + "services.svg", // Copied from https://github.com/carbon-design-system/carbon-icons/blob/master/src/svg/services.svg
                        instructionsUrl     : baseMetadataUrl + "instructions.html",
                        longDescription     : "Test Node Resource Service Broker Long Description",
                        providerDisplayName : "Company Name",
                        supportUrl          : baseMetadataUrl + "support.html",
                        termsUrl            : baseMetadataUrl + "terms.html"
                    },
                    name             : SERVICE_NAME,
                    // TODO - Ensure this value is accurate for your service. Requires PATCH of /v2/service_instances/:instance_id below if true
                    plan_updateable  : true,
                    tags             : ["lite", "tag1a", "tag1b"],
                    plans            :
                    [
                        {
                            bindable    : true,
                            description : "Test Node Resource Service Broker Plan Description",
                            free        : true,
                            // TODO - GUID generated by http://www.guidgenerator.com
                            // TODO - This service plan id must be unique within an IBM Cloud environment's set of service plans
                            id          : "2a1d139b-1b05-4e33-b72e-a1f8c14be559",
                            metadata    :
                            {
                                bullets     : ["Test bullet 1", "Test bullet 2"],
                                displayName : "Lite"
                            },
                            // TODO - This service plan name must be unique within the containing service definition
                            name        : "lite"
                        }
                    ]
                }
            ]
}
```


La matriz de servicios OSB debe ser exactamente la misma que la de los metadatos de la oferta que ha añadido a la consola de gestión de recursos. Para garantizar una paridad uno a uno entre OSB y la consola de gestión de recursos, resulta esencial que compare la matriz de servicios de `catalog.json` que ha descargado de la consola de gestión de recursos con la matriz de servicios real del intermediario. Todos los ID y nombres de servicio y de plan deben coincidir.
{: tip}

## Información de intermediario que proporciona la plataforma {{site.data.keyword.Bluemix_notm}}

El intermediario o intermediarios de servicio recibirán la siguiente información de la plataforma {{site.data.keyword.Bluemix_notm}}:

### X-Broker-API-Originating-Identity

Se proporcionará la **cabecera de identidad de usuario** mediante una API que origina la cabecera de identidad. Esta cabecera de solicitud incluirá la identidad IAM de {{site.data.keyword.Bluemix_notm}} del usuario. La identidad de IAM estará codificará en base64. {{site.data.keyword.Bluemix_notm}} da soporte a un único dominio de autenticación: `IBMid`. El dominio de `IBMid` utiliza un ID exclusivo de IBMid (IUI) para identificar la identidad del usuario en {{site.data.keyword.Bluemix_notm}}. Este IUI es una serie opaca para el proveedor del servicio.

Ejemplo:

```
X-Broker-API-Originating-Identity: ibmcloud eyJpYW1faWQiOiJJQk1pZC01MEdOUjcxN1lFIn0=
Decoded:
{"iam_id":"IBMid-50GNR717YE"}
```

### Versión de la cabecera de API

La **cabecera de la versión de API** será [2.12](https://github.com/openservicebrokerapi/servicebroker/blob/v2.12/spec.md){: new_window} ![Icono de enlace externo](../icons/launch-glyph.svg "Icono de enlace externo"). Por ejemplo: `X-Broker-Api-Version: 2.12`.

### body.context de la instancia del recurso (PUT) y body.context de la instancia del recurso (PATCH)

`PUT /v2/service_instances/:resource_instance_id` y `PATCH /v2/service_instances/:resource_instance_id` recibirán el siguiente valor en **body.context**: `{ "platform": "ibmcloud", "account_id": "tracys-account-id", "crn": "resource-instance-crn" }`.

## Recomendaciones adicionales sobre el intermediario

### Recomendaciones sobre el uso de operaciones síncronas frente a asíncronas

La API OSB da soporte a las modalidades de operación síncronas y asíncronas. Si las operaciones van a tardar menos de 10 segundos, se recomiendan las operaciones síncronas.  De lo contrario, debe utilizar la modalidad de operación asíncrona.  Encontrará más información sobre este tema en la especificación de OSB.

Si la operación asíncrona tarda menos de 10 segundos, cuando se intente suministrar una instancia, la plataforma excederá el tiempo de espera.
{: tip}

### Recomendaciones para gestionar intermediarios entre ubicaciones

Es importante que los usuarios conozcan la ubicación de sus servicios de nube para saber la latencia, disponibilidad y residencia de los datos.

Cuando se suministran instancias de servicio en {{site.data.keyword.Bluemix_notm}}, uno de los parámetros obligatorios que especificarán los usuarios es la ubicación en la que desean que se suministre la instancia de servicio. Algunos servicios pueden dar soporte al suministro en varias ubicaciones. Por ejemplo, un servicio de base de datos se puede suministrar en todas las regiones de {{site.data.keyword.Bluemix_notm}} o puede dar soporte a un subconjunto.

Si el servicio basado en API de terceros se implementa en otra nube y se expone en {{site.data.keyword.Bluemix_notm}}, la ubicación debe indicar la ubicación del servicio en la otra nube.

Al realizar la incorporación a {{site.data.keyword.Bluemix_notm}}, debe implementar al menos un intermediario OSB, pero tiene la opción de tener más de un intermediario, en función de la estrategia de despliegue y de las ubicaciones a las que desea dar soporte para el servicio.  Dentro de la herramienta de la consola de gestión de recursos, se establece la correlación entre la combinación de servicio/plan/ubicación y el intermediario que va a dar servicio a las operaciones de dicha combinación. Las opciones típicas serían definir un solo intermediario para dar servicio a todas las ubicaciones para el servicio o definir un intermediario por ubicación; la elección corresponde al proveedor del servicio.

Para ver una lista de las ubicaciones disponibles, consulte las [ubicaciones del catálogo global de IBM](https://resource-catalog.bluemix.net/search?q=kind:geography){: new_window} ![Icono de enlace externo](../icons/launch-glyph.svg "Icono de enlace externo"). Si el servicio requiere que se definan más ubicaciones en el catálogo global, póngase en contacto con el equipo de incorporación de {{site.data.keyword.Bluemix_notm}}.


## Alojamiento de los intermediarios

El intermediario debe estar alojado como parte de una aplicación que pueda responder a las llamadas de API REST. Y su ubicación alojada debe cumplir las directrices de seguridad de {{site.data.keyword.Bluemix_notm}}. Puede alojarse en {{site.data.keyword.Bluemix_notm}} o se puede alojar externamente, siempre que sea accesible públicamente desde el propio {{site.data.keyword.Bluemix_notm}}.

Para alojar el intermediario fuera de IBM, debe asegurarse de que cumple las siguientes directrices de seguridad:
- Debe seguir el protocolo Transport Layer Security (TLS) versión 1.2
- Debe estar alojado en un punto final HTTPs válido que sea accesible en Internet público

Si desea alojarlo en {{site.data.keyword.Bluemix_notm}}, encontrará información sobre cómo crear una app utilizando Containers (Kubernetes) aquí: [Adoptadores internos - Información de uso](/docs/containers/cs_internal.html#cs_internal).

Necesitará la ubicación alojada del intermediario de servicio para completar el paso siguiente. Tenga preparados el URL y las credenciales asociadas a la app antes de pasar al siguiente paso.
{: tip}

## Cómo probar el intermediario del servicio

Debe validar el intermediario ejecutando mandatos curl sobre los distintos puntos finales que va a habilitar. El archivo readme de ejemplo ofrece una guía excelente para preparar los puntos finales OSB: https://github.com/IBM/sample-resource-service-brokers/blob/master/README.md

### Cómo preparar el intermediario del servicio

Utilice el ejemplo siguiente para probar la respuesta curl del intermediario:

```
curl -X PUT  https://<sample-service-broker>/v2/service_instances/<encoded-resource-crn> \
     -u '<your broker user>:<your broker password>' \
     -H 'content-type: application/json' \
      -d '{ "context": {"platform": "ibmcloud", \
                        "account_id": "34ff5928-c3c7-4d46-bbf6-1a5628c325d1", \
                        "resource_group_crn": "crn:v1:bluemix:public:resource-controller::a/003e9bc3993aec710d30a5a719e57a80::resource-group:b4570a825f7f4d57aa54e8e1d9507926", \
                        "crn": "<resource-crn>", \
                        "target_crn": "<target_crn>"}, \
            "service_id": "a07f025c-90db-4652-afd1-cf4adfac93c8", \
            "plan_id": "fe442cec-2eef-41fe-9f92-58d6c094584f"}'
```

## Pasos siguientes

¡Ya dispone de conocimientos avanzados! Acaba de crear y alojar un intermediario de servicio que cumple con la especificación OSB. Consulte [Paso 4: Desarrollo de un flujo de autenticación](/docs/third-party/cis5-iam.html).
