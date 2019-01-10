---


copyright:
  years: 2018
lastupdated: "2018-11-29"


---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:note: .note}
{:download: .download}

# Paso 2. Definición de la oferta en la consola de gestión de recursos
{: #step2-define}

La consola de gestión de recursos es una herramienta que le ayuda en el proceso de suministro de su oferta de terceros en el catálogo de {{site.data.keyword.Bluemix_notm}}.
Ahora que tiene la aprobación para suministrar un servicio de facturación integrado, está listo para utilizar la consola de gestión de recursos para registrar el servicio, iniciar el desarrollo y definir los planes de precios. La consola de gestión de recursos es una herramienta basada en web que le ayuda en el proceso de suministro del servicio de facturación integrado en el catálogo de {{site.data.keyword.Bluemix_notm}}.
{:shortdesc}

## Antes de empezar
{: #pre-reqs}

1. Asegúrese de que empieza trabajando en [Paso 1: Crear documentación del servicio y anuncio de marketing (PWB)](/docs/third-party/cis1-docs-marketing.html).
2. Asegúrese de que está registrado con {{site.data.keyword.Bluemix_notm}}. Si no lo está, [regístrese](https://cloud.ibm.com/registration){: new_window} ![Icono de enlace externo](../icons/launch-glyph.svg "Icono de enlace externo") antes de continuar.
3. Asegúrese de que está en la cuenta correcta cuando empiece a trabajar en la consola de gestión de recursos.
4. Prepare su nombre de servicio de {{site.data.keyword.Bluemix_notm}}. Debe proporcionar un nombre de servicio, que se utiliza para identificar el servicio en la plataforma {{site.data.keyword.Bluemix_notm}}, y un nombre de visualización, que es el que ven los clientes en el catálogo de {{site.data.keyword.Bluemix_notm}}.

  Cuando registre la oferta con la consola de gestión de recursos, tenga preparado el nombre de servicio de {{site.data.keyword.Bluemix_notm}}. El nombre de servicio no es el nombre de visualización. El nombre de servicio debe seguir estas reglas:
   - Debe estar en minúsculas
   - No puede incluir espacios, pero se puede incluir guiones (`-`)
   - Debe tener menos de 32 caracteres

   El nombre de servicio debe incluir el nombre de la empresa. Si su empresa tiene más de una oferta, el nombre de servicio debe incluir tanto la empresa como la oferta como parte del nombre. Por ejemplo, suponga que la empresa Compose tiene ofertas para Redis y Elasticsearch. Los nombres de servicio de ejemplo en {{site.data.keyword.Bluemix_notm}} para estas ofertas serían `compose-redis` y `compose-elasticsearch`. Ambos nombres de servicio incluyen nombres de visualización asociados que se muestran en el catálogo de {{site.data.keyword.Bluemix_notm}}: *Compose Redis* y *Compose Elasticsearch*. Otra empresa (por ejemplo, FastJetMail) podría tener una única oferta JetMail, en cuyo caso el nombre de servicio debe ser `fastjetmail`.

## Registre la oferta
{: #register}

Para empezar, inicie una sesión y registre su oferta.

1. Inicie una sesión en [{{site.data.keyword.Bluemix_notm}}](https://cloud.ibm.com){: new_window} ![Icono de enlace externo](../icons/launch-glyph.svg "Icono de enlace externo") con su ID de {{site.data.keyword.Bluemix_notm}}.
   **Aviso**: es muy importante que esté en la cuenta de {{site.data.keyword.Bluemix_notm}} correcta. Si tiene más de una cuenta, asegúrese de que está en la correcta.
2. Vaya al [panel de control de la consola de gestión de recursos](https://cloud.ibm.com/onboarding/dashboard){: new_window} ![Icono de enlace externo](../icons/launch-glyph.svg "Icono de enlace externo").
3. Pulse **Nuevo recurso** para añadir el recurso.
4. Añada el **Nombre de recurso**. Este valor es el nombre de servicio de {{site.data.keyword.Bluemix_notm}} exclusivo que ha obtenido en la sección anterior.
5. No se espera que tenga un intermediario de servicio alojado; seleccione **No** en el campo **¿Está el intermediario preparado para la importación?** . Le guiaremos por el proceso de creación de un intermediario en pasos posteriores, y volverá a la consola de gestión de recursos para importar el intermediario después de que se haya desarrollado y alojado.
7. Después de enviarlo, aparecerá la página **Resumen**. Complete los valores *obligatorios* adicionales y pulse **Guardar**.

Puede guardar el progreso en la consola de gestión de recursos y volver más tarde para añadir más información. La consola de gestión de recursos está diseñada para ayudarle a gestionar el ciclo de vida de su servicio. No pasa nada si no tiene todas las respuestas para todos los campos de inmediato.
{: tip}

## Especifique los metadatos de la oferta
{: #offering-metadata}

En la página **Oferta**, especifique los valores de metadatos que están almacenados en el catálogo de {{site.data.keyword.Bluemix_notm}}. Además, algunos de estos valores se tienen que exportar y almacenar en el intermediario de servicio, donde se utilizan para el suministro y se devuelven como parte de la respuesta de `catalog (GET)`. Utilice estos valores para ayudar a iniciar el desarrollo de un intermediario de servicio en pasos posteriores.

1. En la consola de gestión de recursos, pulse la página **Oferta** y pulse el separador **Página de listado**. La **Página de listado** define
los metadatos que se muestran en el panel de control del servicio de la oferta de {{site.data.keyword.Bluemix_notm}}. Complete todos los valores necesarios y pulse **Guardar**. La consola de gestión de recursos hace un registro inicial de su servicio con {{site.data.keyword.Bluemix_notm}} Identity and Access Management (IAM). Se mostrará una notificación que indica que el servicio se ha registrado con IAM. Más adelante volverá a trabajar con IAM.
2. En la página Oferta, pulse el separador **Valores**.
   1. Especifique si su oferta **permite cambios de plan**. El valor predeterminado es **No**. Si especifica **Sí**, debe ampliar Open Service Broker para que dé soporte a cambios de plan para las instancias suministradas. Si la oferta da soporte a varios planes y desea que los usuarios cambien sus planes para una instancia suministrada, deberá habilitar la capacidad de los usuarios para actualizar su instancia de servicio. Para ver más detalles, consulte el punto final `/v2/service_instances/{instance_id} PATCH` en la [API de Open Service Broker v2.12](https://github.com/openservicebrokerapi/servicebroker/blob/v2.12/spec.md#updating-a-service-instance){: new_window} ![Icono de enlace externo](../icons/launch-glyph.svg "Icono de enlace externo")
   2. Especifique si el servicio se puede **Enlazar**. El valor predeterminado es **No**. Seleccione **Sí** si el servicio se puede enlazar a aplicaciones en {{site.data.keyword.Bluemix_notm}}. Si se puede enlazar, debe devolver los puntos finales de API y las credenciales a los consumidores del servicio. Cuando se desarrolla un servicio enlazable, se deben utilizar las [operaciones enlazables en la API de Open Service Broker v2.12](https://github.com/openservicebrokerapi/servicebroker/blob/v2.12/spec.md#binding){: new_window}![Icono de enlace externo](../icons/launch-glyph.svg "Icono de enlace externo")
   3. Complete los campos necesarios adicionales y pulse **Guardar**.
3. Ahora la página Oferta tiene una marca de selección en la navegación, lo que indica que ha pasado los requisitos mínimos para completar esta página. Si la página aún está marcada como incompleta, debe volver a abrir la página y comprobar si hay campos *obligatorios* incompletos.

La carta de la oferta inicial incluye un URL de documentación del servicio que genera el entorno de trabajo de Provider. Debe especificar dicho URL en los campos **URL de documentación** y **URL de instrucciones**
{: tip}

## Regístrese con IAM
{: #reg-iam}

IAM es necesario para todos los servicios que se han incorporado a {{site.data.keyword.Bluemix_notm}}. Consulte [¿Qué es IAM?](/docs/iam/index.html#what-is-cloud-iam-) para obtener más información sobre los conceptos y los requisitos de IAM.

La consola de gestión de recursos genera los siguientes valores de IAM:
   - ID de servicio (generado y almacenado)
   - Clave de API (generada, no almacenada; se muestra una vez)
   - ID de cliente (generado y almacenado)
   - Secreto de cliente (generado, no almacenado)

El proveedor de servicios tiene que proporcionar:
   - URI de redirección (volverá a la consola de gestión de recursos después de haber desarrollado su OSB. Obtenga el URI de redirección a partir de la ubicación del intermediario de servicio alojado).

1. En la consola de gestión de recursos, pulse la página **Gestión de acceso**.
2. Pulse **Habilitar IAM**. La consola de gestión de recursos registra el servicio con IAM, crea el ID de servicio y la política y crea una clave de API. También crea un ID de cliente y secreto incompletos. El ID de cliente se debe actualizar con el URI de redirección después de que lo obtenga.
3. Pulse **Estado** para ver el estado actual de la habilitación de IAM.

Tendrá que volver a la página de IAM más adelante para especificar el `URI de redirección`. No tendrá este valor hasta que lleve a cabo ciertos pasos adicionales de desarrollo para crear un flujo de autenticación. En pasos siguientes se le ayudará a obtener el valor del URI de redirección.
{: note}

Se le proporciona una clave de API cuando **Habilita IAM**. Es muy importante que guarde la clave de API. El valor no se vuelve a mostrar. Si pierde la clave de API, puede suprimir la clave y crear una nueva: [Gestión de claves de API de ID de servicio](/docs/iam/serviceid_keys.html#serviceidapikeys)
{: tip}

## Desarrollo de un plan de precios
{: #pricing-plan}

Cuando incorpore el servicio en {{site.data.keyword.Bluemix_notm}}, debe definir un plan de precios. Si sabe con detalles cómo desea facturar a los usuarios por su servicio, puede especificar dicha información en el plan. Sin embargo, si aún no ha definido un plan de pago, puede empezar por habilitar un plan gratuito y configurar un plan de pago posteriormente.

1. En la consola de gestión de recursos, pulse la página **Precios**.
2. Pulse **Añadir plan** para crear una nueva entrada de plan y pulse **Editar plan** para editar el plan.
   * **Plan gratuito**: todas las ofertas pueden tener un plan Lite gratuito, que permite a los usuarios probar el servicio de forma gratuita. Los planes gratuitos utilizan el valor *Lite* para el **Nombre de visualización** y *lite* para el **Nombre programático**. Especifique **Sí** en **¿Este plan es gratuito?**. Pulse **Guardar**. El plan se publica en el catálogo de {{site.data.keyword.Bluemix_notm}}.
   * **Plan de suscripción**: especifique **No** en **¿Este plan es gratuito?**. Complete los campos obligatorios. Deje las **Medidas de precios** predeterminadas. Se ofrecen estas medidas predeterminadas para que cobre a los usuarios una tarifa mensual única. Pulse **Guardar**. El plan se publica en el catálogo de {{site.data.keyword.Bluemix_notm}}. Guarde el mandato curl de ejemplo para enviar datos sobre uso.
   * **Plan de medición**: especifique **No** en **¿Este plan es gratuito?**. Complete los campos obligatorios. *Suprima* la medida de suscripción de **Métricas de precios** predeterminada. Pulse **Añadir otra métrica**, complete la página **Añadir métrica de precios** y pulse **Añadir métrica**. Pulse **Guardar**. El plan se publica en el catálogo de {{site.data.keyword.Bluemix_notm}}. Guarde el mandato curl de ejemplo para enviar datos sobre uso. Para obtener ayuda para seleccionar las métricas correctas, consulte [Integración de mediciones](/docs/third-party/metering.html).
3. Ahora la página **Precios** está marcada como completada, lo que indica que ha pasado los requisitos mínimos para completar esta página.

Los proveedores de servicios deben automatizar el envío de datos de uso por hora para todos los planes de medición. Para obtener más información, consulte [Envío de datos sobre uso para planes de medición](/docs/third-party/submitusage.html)
{: tip}

## Exporte los metadatos como JSON
{: #export-metadata}

Ahora que ha definido el servicio dentro de la consola de gestión de recursos, puede descargar un archivo catalog.json y utilizarlo para informar sobre el desarrollo de su OSB (Open Service Broker). El archivo catalog.json contiene metadatos que deben alojarse en el intermediario. Estos valores definen el contrato entre el intermediario y la plataforma {{site.data.keyword.Bluemix_notm}} para los servicios y planes a los que da soporte el intermediario. Todos los metadatos de catálogo adicionales que no son necesarios para el suministro se almacenan en el catálogo de {{site.data.keyword.Bluemix_notm}}. Las actualizaciones de los valores de visualización del catálogo que se utilizan para representar el panel de control como enlaces, iconos y metadatos convertidos i18n se actualizan en la consola de gestión de recursos. No se alojan en el intermediario. Ninguno de los metadatos almacenados en el intermediario se muestra en la consola de {{site.data.keyword.Bluemix_notm}} ni en la CLI de {{site.data.keyword.Bluemix_notm}}. La consola y la CLI devuelven lo que se ha definido en la consola de gestión de recursos y almacenado en el catálogo de {{site.data.keyword.Bluemix_notm}}.

1. En la consola de gestión de recursos, abra la página **Despliegues**.
2. Pulse **Gestionar**.
3. Pulse **Descargar definiciones**.

Guarde el archivo `catalog.json`. Lo utilizará para desarrollar Open Service Broker en la sección siguiente.

## Pasos siguientes
{: #next-steps}

Va por buen camino. Ha definido la oferta de servicio añadiendo metadatos de visualización de catálogo, registrándose con IAM y creando uno o varios planes de precios. A continuación, con el JSON exportado, puede empezar a desarrollar un intermediario de servicio. Consulte el [Paso 3: Desarrollo y alojamiento de intermediarios de servicio](/docs/third-party/cis3-broker.html).
