---

copyright:
  years: 2015, 2018
lastupdated: "2018-08-28"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:tip: .tip}
{:new_window: target="_blank"}
{:faq: data-hd-content-type="faq"}
{:note: .note}

# Preguntas más frecuentes
{: #3p-faqs}

## ¿Cuáles son las distintas opciones de medición para los planes?
{: #metering}
{: faq}

{{site.data.keyword.Bluemix}} da soporte a varios modelos para calcular el uso de la oferta. Los proveedores de la oferta miden varias métricas en las instancias suministradas y envían dichas medidas al servicio de medición. El servicio de evaluación agrega el uso enviado en diferentes grupos (instancia, grupo de recursos y cuenta) en función del modelo que eligen los proveedores de la oferta. Los modelos de agregación y de evaluación para todas las métricas de un plan están contenidos en los documentos de definición de medición y evaluación del plan.

Es necesario automatizar el envío de uso por hora utilizando la API de servicio de medición si ofrece un plan de medición.
{: note}

Para obtener más información sobre la medición, consulte [Integración de mediciones](/docs/third-party/metering.html#meteringintera). Para obtener más información sobre el envío de datos de uso de medición, consulte [Envío de datos de uso para planes de medición](/docs/third-party/submitusage.html#submitusage).

## ¿Cómo puedo generar una nueva clave de API de {{site.data.keyword.Bluemix_notm}} Identity and Access Management?
{: #iam-creds}
{: faq}

Se le proporciona una clave de API cuando se habilita IAM. Es esencial que guarde bien la clave de API. El valor no se muestra de nuevo. Si pierde la clave de API, puede suprimir la clave y crear una nueva. Para obtener más información, consulte [Gestión de claves de API de ID de servicio](/docs/iam/serviceid_keys.html#serviceidapikeys). 


