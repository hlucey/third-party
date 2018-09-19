---


copyright:
  years: 2018
lastupdated: "2018-08-31"


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

Cuando suministra su oferta de terceros como servicio de referencia, se dirige a los usuarios a su sitio web desde la página de detalles del catálogo de la consola de {{site.data.keyword.Bluemix_notm}}. Desde su sitio web, los usuarios crean cuentas y obtienen las credenciales adecuadas que se necesitan para conectar programáticamente su oferta de terceros a una app que están creando en {{site.data.keyword.Bluemix_notm}}.

## Comparación entre los distintos tipos de ofertas
{: #compare}

En la tabla siguiente se muestra una comparación detallada entre los tipos de oferta de terceros.

|  | Servicio de facturación integrado  | Servicio de referencia |
|---|---|---|
| **Incorporación** | La incorporación se gestiona mediante IBM Provider Workbench y la consola de gestión de recursos. El proveedor de la oferta es el responsable de desarrollar un Open Service Broker, de alojarlo, de probarlo y de publicar su oferta a través de una serie de pasos de autoservicio. | La incorporación se gestiona mediante Provider Workbench. El proceso de incorporación de autoservicio tarda unas dos semanas. |
| **Despliegue** | Lo suministra la plataforma {{site.data.keyword.Bluemix_notm}} | Solo servicios basados en API |
| **Facturación**  |  En el modelo de facturación integrada, el usuario recibe una sola factura correspondiente a la oferta de IBM y a la oferta de terceros integrada. | En el modelo de referencia, los proveedores facturan al usuario y retienen el 100% de los ingresos.  |
| **Ejemplo** | [PowerAI](https://console.bluemix.net/catalog/services/powerai) | [API Accern](https://console.bluemix.net/catalog/services/accern-api) |
{: caption="Tabla 1. Comparación entre los distintos tipos de ofertas de terceros" caption-side="top"}

