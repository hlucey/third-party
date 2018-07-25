---


copyright:
  years: 2018
lastupdated: "2018-06-28"


---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:download: .download}

# Visión general: desarrollo de un servicio de facturación integrado
{: #overview}

Este tema le guiará por los pasos a seguir para desarrollar y publicar un servicio de facturación integrado de terceros en {{site.data.keyword.Bluemix_notm}}. Cuando haya recibido aprobación para suministrar su oferta en el catálogo de {{site.data.keyword.Bluemix_notm}}, empezará a desarrollar su oferta en la consola de gestión de recursos (consola de gestión de recursos), una interfaz de usuario guiada. Dentro de la consola de gestión de recursos, diseñará los metadatos del catálogo, configurará los planes de precios del servicio y lo integrará con IBM Cloud Access Management (IAM). A continuación, fuera de la consola de gestión de recursos, realizará el desarrollo del código para crear y alojar un nuevo intermediario de servicio abierto (se proporcionarán ejemplos de intermediarios de inicio y documentación de API) y utilizará IAM para desarrollar un flujo de autenticación. Una vez que se hayan completado estos pasos, volverá a la consola de gestión de recursos para desplegar el servicio en el catálogo en una modalidad de visibilidad limitada que le permite probar y validar varios requisitos del servicio. Cuando esté listo y su oferta cumpla todos los requisitos, el servicio estará completamente visible en el catálogo de {{site.data.keyword.Bluemix_notm}}.


## ¿Qué tengo que suministrar en un servicio de facturación integrado?

Puede trabajar con PWB, la consola de gestión de recursos y el entorno de desarrollo que desee para lograr estos objetivos. Consulte la [lista de comprobación](/docs/third-party/checklist.html#checklist) como ayuda para seguir estos pasos.

En los pasos siguientes se resume el proceso de incorporación en nivel general:

En estos pasos se presupone que dispone de la aprobación para suministrar un servicio de facturación integrado. Si no ha realizado el proceso de registro y aprobación inicial en PWB, consulte [Cómo comenzar a publicar su oferta de terceros en {{site.data.keyword.Bluemix_notm}}](/docs/third-party/index.md)
{: tip}

1. [Crear: crear documentación del servicio y anuncio de marketing (PWB)](/docs/third-party/cis1-docs-marketing.html)
2. [Definir: definir su oferta en la consola de gestión de recursos {{site.data.keyword.Bluemix_notm}}](/docs/third-party/cis2-rmc-define.html)
3. [Desarrollar: desarrollar y alojar uno o varios intermediarios de servicio mediante la especificación de la API de Open Service Broker](/docs/third-party/cis3-broker.html)
4. [IAM: desarrollar un flujo de autenticación (OAuth), validar la autorización de usuario (v2/authz) y obtener el URI de redirección](/docs/third-party/cis5-iam.html)
5. [Publicar y probar: conectar OSB a la consola de gestión de recursos, publicar el servicio en modalidad de visibilidad limitada en el catálogo de {{site.data.keyword.Bluemix_notm}} y probar la oferta](/docs/third-party/cis4-rmc-publish.html).
6. [Solicitar aprobación para poner el servicio a disponibilidad general](/docs/third-party/cis6-ga.html)

## Soporte

Los servicios de facturación integrados requieren que los proveedores de servicios de terceros proporcionen su propio modelo de soporte.  El representante de IBM le ayudará a habilitar el modelo de soporte y a asegurarse de que si un usuario abre una incidencia con el equipo de soporte de {{site.data.keyword.Bluemix_notm}}, este direccionará la incidencia al sitio de soporte de terceros.

## Actualizaciones continuas

Después de publicar el servicio, puede seguir revisando y puede realizar actualizaciones trabajando directamente con el representante de {{site.data.keyword.Bluemix_notm}}.



