---

copyright:

  years: 2018, 2019

lastupdated: "2019-02-25"

keywords: party offering types, third-party offering, billing service

subcollection: third-party

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:tip: .tip}
{:new_window: target="_blank"}

# Tipos de ofertas de terceros
{: #offering-types}

Puede suministrar su oferta de terceros en {{site.data.keyword.Bluemix}} como un servicio de facturación integrado o como un servicio de referencia.
{:shortdesc}

Suministrar su oferta de terceros como un servicio de facturación integrado significa que los usuarios pueden elegir entre los distintos planes de precios de IBM que se muestran en la página de detalles del catálogo en la consola de {{site.data.keyword.Bluemix_notm}}. Además, los usuarios pueden crear automáticamente una instancia de su oferta de terceros.

Cuando suministra su oferta de terceros como servicio de referencia, se dirige a los usuarios a su sitio web desde la página de detalles del catálogo de la consola de {{site.data.keyword.Bluemix_notm}}. Desde su sitio web, los usuarios crean cuentas y obtienen las credenciales adecuadas. Las credenciales se necesitan para conectar programáticamente su oferta de terceros a una app que están creando en {{site.data.keyword.Bluemix_notm}}.

## Comparación entre los distintos tipos de ofertas
{: #compare}

En la tabla siguiente se muestra una comparación detallada entre los tipos de oferta de terceros.

|  | Servicio de facturación integrado  | Servicio de referencia |
|---|---|---|
| **Incorporación** | La incorporación se gestiona mediante el entorno de trabajo de IBM Provider y la consola de gestión de recursos. El proveedor de la oferta desarrolla un Open Service Broker, lo aloja, lo prueba y publica su oferta a través de una serie de pasos de autoservicio. | La incorporación se gestiona mediante el entorno de trabajo de Provider. El proceso de incorporación de autoservicio tarda unas dos semanas. |
| **Despliegue** | Lo crea la plataforma {{site.data.keyword.Bluemix_notm}} | Solo servicios basados en API |
| **Facturación**  |  En el modelo de facturación integrada, el usuario recibe una sola factura correspondiente a la oferta de IBM y a la oferta de terceros integrada. | En el modelo de referencia, los proveedores facturan al usuario y retienen el 100% de los ingresos.  |
| **Ejemplo** | [PowerAI](https://{DomainName}/catalog/services/powerai){: new_window} ![Icono de enlace externo](../icons/launch-glyph.svg "Icono de enlace externo") | [API de Accern](https://{DomainName}/catalog/services/accern-api){: new_window} ![Icono de enlace externo](../icons/launch-glyph.svg "Icono de enlace externo") |
{: caption="Tabla 1. Comparación entre los distintos tipos de ofertas de terceros" caption-side="top"}

