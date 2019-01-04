---


copyright:
  years: 2018
lastupdated: "2018-11-14"


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

En este tema se presentan los pasos necesarios para desarrollar y publicar el servicio de facturación integrado de terceros en {{site.data.keyword.Bluemix}}. 
{:shortdesc}

Cuando haya recibido aprobación para suministrar su oferta en el catálogo de {{site.data.keyword.Bluemix_notm}}, empezará a desarrollar su oferta en la consola de gestión de recursos, una experiencia de IU guiada. Diseñe los metadatos de catálogo, configure los planes de precios de servicio e intégrese con {{site.data.keyword.Bluemix_notm}} Identity and Access Management (IAM). 

A continuación, fuera de la consola de gestión de recursos, realice el desarrollo del código para crear y alojar un nuevo intermediario de servicio abierto. Se proporcionan ejemplos de intermediarios de inicio y documentación de API, y utilice IAM para desarrollar un flujo de autenticación. Después de completar estos pasos, vuelva a la consola de gestión de recursos para desplegar el servicio en el catálogo en una modalidad de visibilidad limitada, donde puede probar y validar los requisitos de los entregables. Cuando esté listo y su oferta cumpla todos los requisitos, el servicio estará completamente visible en el catálogo de {{site.data.keyword.Bluemix_notm}}.


## Cómo funciona el proceso
{: #process}

Para entregar un servicio de facturación integrado, puede trabajar con el entorno de trabajo del componente Provider, con la consola de gestión de recursos y con el entorno de desarrollo de su elección. Consulte la [lista de comprobación](/docs/third-party/checklist.html#checklist) como ayuda para seguir estos pasos.

En este paso se presupone que se ha aprobado que suministre un servicio de facturación integrado. Si no ha completado el proceso de registro y aprobación inicial en PWB, consulte: [Cómo comenzar a publicar su oferta de terceros en {{site.data.keyword.Bluemix_notm}}](/docs/third-party/index.md)
{: tip}

1. [Crear su documentación y su anuncio de marketing](/docs/third-party/cis1-docs-marketing.html).
2. [Definir su oferta en la consola de gestión de recursos{{site.data.keyword.Bluemix_notm}}](/docs/third-party/cis2-rmc-define.html).
3. [Desarrollar y alojar sus intermediarios de servicio](/docs/third-party/cis3-broker.html).
4. [Desarrollar un flujo de autenticación](/docs/third-party/cis5-iam.html).
5. [Probar el servicio](/docs/third-party/cis4-rmc-publish.html).
6. [Publicar el servicio a nivel público](/docs/third-party/cis6-ga.html).

## Soporte
{: #support}

Los servicios de facturación integrados requieren que los proveedores de ofertas de terceros proporcionen su propio modelo de soporte. Su representante de IBM puede ayudarle a habilitar el modelo de soporte y a asegurarse de que si un usuario abre una incidencia con el equipo de soporte de {{site.data.keyword.Bluemix_notm}}, la incidencia se direcciona al sitio de soporte de terceros.

## Actualizaciones continuas
{: #maintain}

Después de publicar el servicio, puede seguir revisando y puede realizar actualizaciones trabajando directamente con el representante de {{site.data.keyword.Bluemix_notm}}.



