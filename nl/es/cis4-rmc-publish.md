---


copyright:
  years: 2018, 2019 
lastupdated: "2019-01-30"


---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:download: .download}

# Paso 5. Publicación y prueba del servicio
{: #step5-pubtest}

Ahora que tiene el intermediario o intermediarios alojados que cumplen la especificación OSB, puede volver a la consola de gestión de recursos para publicar el servicio en el catálogo de {{site.data.keyword.Bluemix_notm}}. 
{:shortdesc}

## Antes de empezar
{: #service-pre-reqs}

En este paso se presupone que se ha aprobado que suministre un servicio de facturación integrado. Si no ha completado el registro y aprobación iniciales en el entorno de trabajo de Provider, consulte la [guía de aprendizaje de iniciación](/docs/third-party/index.md?topic=third-party-get-started#get-started).
{: tip}

Asegúrese de que ha iniciado el paso 1 y completado los pasos 2, 3 y 4:
1. [Crear documentación del servicio y anuncio de marketing](/docs/third-party?topic=third-party-content-tasks#content-tasks).
2. [Definir su oferta en la consola de gestión de recursos](/docs/third-party?topic=third-party-step2-define#step2-define).
3. [Desarrollar y alojar sus intermediarios de servicio](/docs/third-party?topic=third-party-step3-osb#step3-osb).
3. [Desarrollar un flujo de autenticación](/docs/third-party?topic=third-party-step4-iam#step4-iam).

## Publique su servicio en {{site.data.keyword.Bluemix_notm}}
{: #publish}

1. En la consola de gestión de recursos, pulse la página **Despliegues**.
2. Pulse el separador **Intermediarios** y pulse **Añadir intermediario**.
3. Pulse **Gestionar** para abrir la página Configuración del intermediario de servicios.
4. Añada su intermediario alojado y pulse **Registrar intermediario**.
5. Después de registrarlo correctamente, vaya al separador **Despliegues del catálogo**.
6. Pulse **Añadir despliegue** y seleccione el plan y el intermediario que desea desplegar.
7. Seleccione la región y el centro de datos en los que desea desplegar el servicio y pulse **Añadir**.
8. En la página **Despliegues**, revise el despliegue no publicado y pulse **Publicar**.
9. En la página **Publicar en el catálogo**, revise los detalles del despliegue y pulse **Publicar**.

La página Despliegues debería estar marcada como completada en el área de navegación, lo que indica que ha superado los requisitos mínimos.

¿Se ha quedado estancado en un error de despliegue? Póngase en contacto con el representante de IBM para obtener ayuda.
{: tip}

## Pruebe la oferta desplegada 
{: #publish-test}

Como ha realizado el despliegue en modalidad de visibilidad limitada, solo puede ver la oferta en el catálogo de {{site.data.keyword.Bluemix_notm}}. Con la lista de comprobación de la siguiente sección, inicie una sesión en {{site.data.keyword.Bluemix_notm}} y siga los pasos de los criterios de prueba.

1. Inicie una sesión en [{{site.data.keyword.Bluemix_notm}}](https://cloud.ibm.com){: new_window} ![Icono de enlace externo](../icons/launch-glyph.svg "Icono de enlace externo") con su IBMid.
2. Asegúrese de que está en la cuenta correcta (la misma cuenta que ha utilizado para crear el servicio)
3. Pulse el enlace **Catálogo** en la cabecera y busque la oferta.
4. A continuación, utilice la lista de comprobación de la sección siguiente para validar el servicio.

### Lista de comprobación - Probar el servicio
{: #test-your-service}

1. Valide la autenticación en el panel de control de la instancia de servicio
2. El catálogo se visualiza correctamente (Importar desde intermediario se muestra correctamente en la consola de gestión de recursos)
3. El suministro funciona - puede crear una instancia de servicio en el plan que desee
4. La anulación de suministro funciona - puede suprimir una instancia de servicio.
5. El enlace funciona - puede pulsar **Conexiones** y conectar el servicio a otra aplicación
6. La opción de desenlazar funciona - puede desconectar el servicio y suprimir la conexión.
7. Crear clave de servicio / Suprimir clave de servicio - puede pulsar **Credenciales** y generar una clave de servicio, y luego suprimir dicha clave.
8. Pruebe `plan_changeable` si da soporte a varios planes. Si habilita esta opción (la establece en Sí), tendrá que ampliar Open Service Broker para que dé soporte a cambios en el plan para las instancias suministradas. Si la oferta da soporte a varios planes y desea que los usuarios cambien sus planes para una instancia suministrada, deberá habilitar la capacidad de los usuarios para actualizar su instancia de servicio. Para ver más información, compruebe que el punto final /v2/service_instances/{instance_id} PATCH de Open Service Broker API v2.12  - Parche - muestra que el usuario puede cambiar el plan en la instancia suministrada. Para probarlo, conmute el plan en una instancia de servicio suministrada existente.
9. La especificación OSB no da soporte a un estado de instancia inhabilitada, pero aún no suprimida. Para que IBM Cloud dé soporte a los clientes que pueden experimentar un vencimiento de facturación u otra situación que pueda dar lugar a la suspensión de la cuenta (pero no cancelación), IBM Cloud define puntos finales de API ampliados que permiten inhabilitar y volver a habilitar instancias de servicio. Las siguientes extensiones de punto final son **OBLIGATORIAS**. Trabaje con su representante de IBM para que compruebe que puede habilitar e inhabilitar puntos finales:
   - habilitar e inhabilitar instancias (GET): estado - devuelve el estado de la instancia de servicio.
   - habilitar e inhabilitar (PUT): le permite habilitar o inhabilitar una instancia de servicio.
10. Pruebe el envío de datos uso si da soporte a planes de medición. Para cualquier plan con uso medido, debe validar lo siguiente:
   - Puede utilizar la API de uso y devolver correctamente precios precisos en función del uso.
   - Puede demostrar que ha habilitado el envío automatizado por hora para el uso, dando soporte a todos los usuarios que suministran una instancia de su servicio.

Si no pasa todas las pruebas, repita los pasos anteriores para publicar el servicio y probar de nuevo y repita el proceso hasta que pase todas las pruebas correctamente.


## Pasos siguientes
{: #release}

Ahora que tiene un servicio funcional en el catálogo, puede crear una demostración y solicitar aprobación para publicar su servicio a nivel público. Consulte [Paso 6: Publicación del servicio a nivel público](/docs/third-party?topic=third-party-public-releasing#public-releasing).
