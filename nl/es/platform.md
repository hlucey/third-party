---

copyright:

  years: 2018, 2019

lastupdated: "2019-02-25"

keywords: IBM Cloud platform, integrated billing services, lifecycle of IBM Cloud resources, provisioning layer 

subcollection: third-party

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:note: .note}
{:download: .download}

# Cómo utilizan la plataforma {{site.data.keyword.Bluemix_notm}} los servicios de facturación integrados
{: #how-it-works}

Los servicios de facturación integrados son distintos de los servicios de referencia. Un servicio de facturación integrado utiliza la plataforma {{site.data.keyword.Bluemix_notm}} para la autenticación, el acceso, el suministro, la medición y la facturación. En este tema encontrará una visión general de los componentes de la plataforma que utiliza el servicio de facturación integrado.

## La capa de suministro de {{site.data.keyword.Bluemix_notm}}
{: #provisioning-layer}

La capa de suministro gestiona el ciclo de vida de los recursos de {{site.data.keyword.Bluemix_notm}}. La capa de suministro es la responsable de controlar y realizar un seguimiento del ciclo de vida de los recursos en una cuenta de cliente. Los *recursos* son componentes físicos o lógicos que se pueden suministrar o reservar para una aplicación o instancia de servicio. Los ejemplos de recursos incluyen límites almacenamiento, base de datos, cuentas, procesador y memoria. En general, los recursos de los que la capa de suministro realiza un seguimiento están pensados para asociar métricas de uso y métodos de facturación, pero no siempre es así. En algunos casos, el recurso puede estar asociado a la capa de suministro para garantizar que el ciclo de vida del recurso se puede gestionar junto con el ciclo de vida de la cuenta.

### Gestión del ciclo de vida de un recurso
{: #lifecycle}

La capa de suministro proporciona API comunes para controlar el ciclo de vida de los recursos desde el suministro (creación de una instancia), pasando por el enlace (creación de credenciales de acceso) y el desenlace (eliminación del acceso), hasta la anulación del suministro (supresión de una instancia). Además, la plataforma {{site.data.keyword.Bluemix_notm}} proporciona varias CLI y una interfaz de usuario que puede gestionar el ciclo de vida de estos recursos que no requieren que cree sus propias instalaciones.

La capa de suministro proporciona varias API para ayudarle a gestionar los siguientes elementos del ciclo de vida del recurso:
* Suministro
* Actualización de una instancia del recurso
* Enlace
* Claves del recurso
* Desenlace
* Anulación de suministro

## {{site.data.keyword.Bluemix_notm}} Identity and Access Management (IAM)
{: #iam}

Identity Access Management (IAM) le permite autenticar usuarios de forma segura y controlar el acceso a todos los recursos de la nube de forma coherente en {{site.data.keyword.Bluemix_notm}}. La capa de suministro de {{site.data.keyword.Bluemix_notm}} ha adoptado IAM para la autenticación y autorización de acciones que se emprenden sobre la capa de suministro. Los proveedores de ofertas de terceros utilizan IAM para crear un flujo de autenticación (OAuth). Para obtener más información, consulte [¿Qué es IAM?](/docs/iam?topic=iam-iamoverview#iamoverview)?

Si su oferta utiliza bibliotecas de OpenID Connect (OIDC), IAM da soporte a la integración de OIDC. OIDC es una capa de autenticación en la parte superior de OAuth 2.0, una infraestructura de autorización, y puede ayudar a simplificar el proceso de incorporación. Para obtener más información sobre OIDC, consulte [Open ID Connect](http://openid.net/connect/){: new_window} ![Icono de enlace externo](../icons/launch-glyph.svg "Icono de enlace externo").

## Catálogo de {{site.data.keyword.Bluemix_notm}}
{: #catalog}

El catálogo de {{site.data.keyword.Bluemix_notm}} almacena las definiciones de la oferta (descripción, características, imágenes, URL, etc.) de los recursos que se muestran en la consola de {{site.data.keyword.Bluemix_notm}}. La consola de gestión de recursos se utiliza para definir todos los aspectos de los metadatos necesarios del servicio. Estos metadatos se publican en el catálogo y son los que se visualizan en el catálogo. Encontrará información detallada sobre los campos de metadatos obligatorios y opcionales de las páginas **Oferta** y **Plan** de la consola de gestión de recursos. Aquí se incluyen los elementos clave para agilizar el proceso de aprendizaje.

   * Nombre de servicio: nombre técnico del servicio. El nombre de servicio es muy importante y se debe definir correctamente. Debe proporcionar un nombre de servicio, que se utiliza para identificar el servicio en la plataforma {{site.data.keyword.Bluemix_notm}}, y un nombre de visualización, que es el que ven los clientes en el catálogo de {{site.data.keyword.Bluemix_notm}}. El nombre de servicio no es el nombre de visualización.
   * Nombre de visualización del servicio: nombre descriptivo de usuario para el servicio. Por ejemplo, "Compose Redis"
   * ID de servicio: GUID del servicio que se utiliza en las llamadas de API al intermediario OSB. Este valor debe ser exclusivo.
   * Icono del servicio: SVG con el logotipo del servicio
   * Descripción del servicio: la descripción del recurso que se muestra cuando se pasa el ratón por encima del icono del recurso en la interfaz de usuario del catálogo de {{site.data.keyword.Bluemix_notm}}. Puede añadir una única frase a la descripción.
   * Descripción detallada del servicio: el primer párrafo que aparece en la página de listado del catálogo. Considere la posibilidad de utilizar al menos dos frases en el caso de una descripción detallada.
   * URL de la documentación: un enlace a la documentación de {{site.data.keyword.Bluemix_notm}}. Se crea en PWB, y este genera automáticamente el valor de url.
   * URL de términos: un enlace a los términos y condiciones del servicio para su uso. Tenga en cuenta que, para fines de GDPR, no enlace con los términos y condiciones de servicios de terceros. En su lugar, debe proporcionar una página exclusiva para un servicio de facturación integrado.
   * URL de instrucciones: de forma similar al URL de documentación, apuntará a la documentación de {{site.data.keyword.Bluemix_notm}}; sin embargo, el URL de instrucciones extrae de forma dinámica la documentación en un separador Iniciación del panel de control del servicio.
   * Categoría: selección de las categorías disponibles de {{site.data.keyword.Bluemix_notm}} en las que se coloca el servicio en el catálogo.
   * Viñetas: pequeños puntos con descripciones del servicio
   * Medios: capturas de pantalla y vídeos sobre el servicio
   * Nombre del plan de servicio: cada plan tiene un nombre técnico. Debe estar en minúsculas, sin espacios y puede incluir "-". Por ejemplo, `gold`.
   * Nombre de visualización del plan de servicio: nombre descriptivo del plan. Por ejemplo, `Gold`
   * ID del plan de servicio: GUID para el plan de servicio que se utiliza en las llamadas de API al intermediario OSB. Este valor debe ser exclusivo. La consola de gestión de recursos genera este valor.
   * Descripción del plan de servicio: la descripción del plan del recurso. La descripción se visualiza después de que se seleccione un plan en la página de detalles del recurso en el catálogo de IBM Cloud
   * Viñetas del plan de servicio: breves puntos descriptivos sobre el plan de servicio


## Open Service Broker
{: #open-service}

Los intermediarios de servicio gestionan el ciclo de vida de los servicios. La plataforma {{site.data.keyword.Bluemix_notm}} interactúa con intermediarios de servicio para suministrar y gestionar instancias de servicio (una instancia de una oferta de servicio) y enlaces de servicio (la representación de una asociación entre una aplicación y una instancia de servicio, que a menudo incluye las credenciales que utiliza la aplicación para comunicarse con la instancia de servicio). Al proporcionar valores de metadatos válidos se crea una respuesta de API REST correcta cuando se realiza una solicitud.

{{site.data.keyword.Bluemix_notm}} utiliza la API de la especificación Open Service Broker (OSB) `versión 2.12`. Examine y familiarícese con la [especificación de la API Open Broker](https://github.com/openservicebrokerapi/servicebroker/blob/v2.12/spec.md){: new_window} ![Icono de enlace externo](../icons/launch-glyph.svg "Icono de enlace externo") y utilice el archivo readme como guía para obtener más información.

Cuando el controlador de recursos recibe una solicitud para suministrar un recurso, llama a OSB para validar el tipo de servicio, la oferta, los planes y la disponibilidad de las regiones. El controlador de recursos también valida la visibilidad del plan que está asociado con la cuenta del cliente. {{site.data.keyword.Bluemix_notm}} ofrece ejemplos de intermediario y documentación sobre la API que amplían la especificación OSB. Encontrará más detalles sobre el desarrollo y el alojamiento del intermediario a medida que siga los pasos detallados de desarrollo e incorporación de la facturación integrada.

## Servicio de medición de {{site.data.keyword.Bluemix_notm}}
{: #metering-service}

Si un servicio ofrece un plan de medición, se factura a los usuarios de {{site.data.keyword.Bluemix_notm}} en función de la cantidad de recursos que utilizan. Por ejemplo, se puede facturar a los usuarios de {{site.data.keyword.Bluemix_notm}} que utilizan servicios de base de datos en función de la cantidad de almacenamiento que utilizan sus aplicaciones. Para poder convertir el uso en un registro facturable se deben enviar datos sobre uso.

Todos los servicios de facturación integrados que ofrecen un plan de medición utilizan el servicio de medición de {{site.data.keyword.Bluemix_notm}} para notificar los datos sobre uso.

Es necesario automatizar el envío de uso por hora utilizando la API de servicio de medición si ofrece un plan de medición.

Para obtener más información sobre la medición, consulte: [Integración de mediciones](/docs/third-party?topic=third-party-meteringintera#meteringintera). Para obtener más información sobre el envío de datos de uso de medición, consulte [Envío de datos sobre uso para planes de medición](/docs/third-party?topic=third-party-submitusage#submitusage).

## Caso de ejemplo de suministro: combinación de todos los elementos
{: #provision2}

Ahora vamos a combinar todos los conceptos y examinaremos un ejemplo de cómo funciona la creación de una instancia de servicio con la plataforma {{site.data.keyword.Bluemix_notm}}.

![Caso de ejemplo de suministro](images/flow-am.svg "Cómo gestiona la plataforma la creación de instancias de un servicio")

Cuando un usuario desea crear una instancia de servicio, puede crearla de una de las dos maneras siguientes:
* **CLI**: con `ibmcloud cli [ ibmcloud resource service-instance-create NAME SERVICE_NAME SERVICE_PLAN_NAME LOCATION ]`
* **Consola de {{site.data.keyword.Bluemix_notm}}**: el usuario puede seleccionar el servicio y el plan y utilizar la operación **Crear**.

La plataforma {{site.data.keyword.Bluemix_notm}} valida que el usuario tiene permiso para crear la instancia de servicio mediante {{site.data.keyword.Bluemix_notm}} IAM. Después de que se produzca esta validación, se inicia el punto final de suministro del intermediario de servicio (PUT /v2/resource_instances/:resource_instance_id). Cuando se produce el suministro, se deben cumplir las siguientes reglas:
* Se debe incluir el contexto {{site.data.keyword.Bluemix_notm}} en la variable context
* `X-Broker-API-Originating-Identity` tiene el ID de IAM de IBM del usuario que ha iniciado la solicitud
* La sección parameters incluye la ubicación solicitada (y más parámetros que necesita el servicio).

Solicitud de suministro de ejemplo:

```
    PUT /v2/service_instances/crn%3Av1%3Abluemix%3Apublic%3Acompose-redis%3Aus-south%3Aa%2F46aa677e-e83f-4d17-a2b6-5b752564477c%3A416d769b-682d-4833-8bd7-5ef8778e5b52?accepts_incomplete=true HTTP/1.1
    Host:  https://broker.compose.cloud.ibm.com
    Authorization: basic dXNlcjpwYXNzd29yZA==
    X-Broker-Api-Version: 2.12
    X-Broker-API-Originating-Identity: ibmcloud aWJtaWQtNDU2MzQ1WA==
    {
      "service_id": "0bc9d744-6f8c-4821-9648-2278bf6925bb", // GUID del servicio de los datos de incorporación
      "plan_id": "ecc19311-aba2-49f7-8198-1e450c8460d4", // GUID del plan de los datos de incorporación
      "context": {
        "platform": "ibmcloud",
        "account_id": "003e9bc3993aec710d30a5a719e57a80",
        "crn": "crn:v1:bluemix:public:compose-redis:us-south:a/003e9bc3993aec710d30a5a719e57a80:416d769b-682d-4833-8bd7-5ef8778e5b52",
        "resource_group_crn": "crn:v1:bluemix:public:resource-controller::a/003e9bc3993aec710d30a5a719e57a80::resource-group:b4570a825f7f4d57aa54e8e1d9507926",
        "target_crn": "crn:v1:bluemix:public:resource-catalog::a/e97a8c01ac694e308ef3ad7795c7cdb3::deployment:e62e2c19-0c3b-41e3-b8b3-c71762ecd489:us-south38399"
      },
      "parameters": {
        "location": "us-south",
        "optional-param":"parámetros que necesita el servicio"
      }
    }
```

### Visión general del parámetro {{site.data.keyword.Bluemix_notm}} `context`
{: #parameter}

En el ejemplo anterior, puede ver los metadatos que se devuelven en el parámetro `context`. El contexto de suministro de {{site.data.keyword.Bluemix_notm}} devuelve lo siguiente:

* **platform**: identifica la plataforma como "ibmcloud"

* **"account_id"**: devuelve el ID de la cuenta de {{site.data.keyword.Bluemix_notm}} que suministra la instancia del servicio.

* **crn**: cuando un cliente suministra su servicio en {{site.data.keyword.Bluemix_notm}}, se crea una instancia de servicio y esta instancia se identifica mediante su nombre de recurso de {{site.data.keyword.Bluemix_notm}} (CRN). El CRN se usa en todos los aspectos de la interacción con {{site.data.keyword.Bluemix_notm}}, incluidos suministro, enlace (creación de credenciales y puntos finales), medición, visualización del panel de control y control de acceso. Desde una perspectiva de proveedor de la oferta, el CRN se puede tratar en gran medida como una serie opaca que se utiliza con las API de {{site.data.keyword.Bluemix_notm}}. También se puede descomponer utilizando la estructura siguiente:

   ```
   crn:version:cname:ctype:service-name:location:scope:service-instance:resource-type:resource
   ```

   En el ejemplo de suministro, vemos que el CRN del servicio `compose-redis` es el siguiente:

   ```
   crn:v1:bluemix:public:compose-redis:us-south:a/46aa677e-e83f-4d17-a2b6-5b752564477c:416d769b-682d-4833-8bd7-5ef8778e5b52::
   ```

   En este ejemplo, la instancia de `compose-redis` forma parte de una cuenta de {{site.data.keyword.Bluemix_notm}} con ID. El ID único de la instancia es `416d769b-682d-4833-8bd7-5ef8778e5b52` y la instancia se aloja en la región `us-south` de {{site.data.keyword.Bluemix_notm}} público.

* **resource_group_crn**: Devuelve el grupo de recursos que contiene la instancia de servicio. Para obtener más información, consulte [Gestión de grupos de recursos](/docs/resources?topic=resources-rgs#rgs).

   Los proveedores de ofertas no se preocupan por `resource_group_crn`, excepto en casos muy específicos. Consulte a su representante de IBM antes de utilizar este campo.
   {: note}

