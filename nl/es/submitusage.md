---

 
copyright:

  years: 2017, 2018

lastupdated: "2018-06-21" 

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:tip: .tip}
{:new_window: target="_blank"}

# Envío de datos de uso para planes de medición
{: #submitusage}

Es necesario que envíe datos de uso correspondientes a todas las instancias de servicio activas cada hora. El hecho de no informar sobre el uso podría suponer una pérdida de ingresos para IBM, lo que a su vez provocaría la pérdida de ingresos para los proveedores de la oferta.
{:shortdesc}

## Cómo funciona el proceso
{: #process-flow}

En los pasos siguientes se describe el proceso para enviar datos sobre uso:

1. Envíe una prueba de uso inicial a través de la herramienta de la API REST de envío de uso para validar que los planes de medición están configurados correctamente.
2. Automatice el envío continuo cada hora a la herramienta de la API REST de envío de uso para cada plan de medición. Puede alojar estos envíos automatizados donde desee, siempre que se dé soporte a SSO estándar.
2. Los registros de uso se agregan en función del modelo de medición, y la cantidad total se muestra en el panel de control de uso en la consola de {{site.data.keyword.Bluemix_notm}}.
3. Se utiliza la cantidad de unidad agregada del proceso de medición, se aplica el coste y se calcula la cantidad que debe el usuario por la instancia de servicio.
4. Al final del mes, el coste final calculado es la cantidad que se genera para el usuario.

## Requisitos previos
{: #prereqs}

Revise los siguientes requisitos previos para habilitar la medición del servicio:

* El catálogo de precios se actualiza con los precios de todas las mediciones sujetas a cargos de los planes del recurso.
* Las definiciones de las mediciones y calificaciones de todos los planes del recurso se verifican y se incorporan.

## Directrices para enviar datos sobre uso 
{: #metering_guidelines}

### Directrices de envío

Consulte las directrices siguientes cuando utilice el servicio de medición de {{site.data.keyword.Bluemix_notm}} para enviar datos de uso del recurso:

* La hora de inicio y la hora de finalización representan el intervalo de tiempo durante el que se han recopilado las mediciones. Los tiempos no dependen de la hora en la que se envía el registro de uso a las API de medición.
* Los registros de uso representan hechos. No actualice el registro de uso después de crearlo. Se especifica una ubicación cuando se crea correctamente un registro de uso. Si se devuelve un código de error, consulte las [acciones](#actions) que es posible que tenga que llevar a cabo.
* Un registro de uso se identifica de forma exclusiva mediante la firma `account_id/resource_group_id/resource_instance_id/consumer_id/plan_id/region/start/end`. Cuando se procesa un registro de uso, cualquier otro registro de uso con la misma firma se rechaza como duplicado.
* Las interacciones con el servicio de medición no se deben combinar con ningún otro servicio. Las solicitudes se deben manejar individualmente, aunque la medición se inicie y finalice con el suministro y el cese de suministro de la instancia.
* Los datos de uso del recurso deben enviarse al servicio de medición una vez cada 2-24 horas. La frecuencia con la que envíen datos de uso dependerá de la frecuencia con la que cambian las métricas de uso.
* Los registros de uso se deben enviar en un plazo de dos días desde el momento en que se ha completado la medición. Los registros de uso más antiguos se rechazan.
* Un envío correcto devuelve el código de respuesta 201. Si se devuelve algún otro código de respuesta, actualice y vuelva a enviar los datos hasta que reciba el código 201.

Estas son las prácticas recomendadas para enviar el uso:

* Se recomienda que los proveedores de servicio envíen datos de uso cada hora para que el usuario final no vea un retraso enorme entre el momento en que se ha consumido el recurso y el momento en el que el coste se ve reflejado en su cuenta.
* Vuelva a intentar el envío de registros de uso únicamente si se ha producido una anomalía real en la solicitud anterior. No vuelva a enviar registros de uso que se hayan aceptado correctamente.

### Directrices sobre ID de servicio

  Debe seguir estas directrices cuando especifique el ID de servicio utilizando el campo de ID en la definición del recurso:
  * El ID debe comenzar por un carácter alfanumérico.
  * Utilice los caracteres A-Z, a-z y 0-9. Los únicos caracteres especiales que puede utilizar son los guiones (-) y los guiones de subrayado (_).
  * Siga el convenio de bicapitalización si el ID contiene más de una palabra.
  * Asegúrese de que la longitud máxima del ID sea de 50 caracteres.

### Directrices sobre el nombre del recurso

  Debe seguir estas directrices cuando especifique el nombre del recurso utilizando el campo resources.name en la definición del recurso:

  * Utilice únicamente palabras que describan sus recursos. Por ejemplo, **Almacenamiento** o **LlamadasApi**. 
  * Siga el convenio de bicapitalización si el nombre contiene más de una palabra.
  * El primer carácter del nombre debe estar en mayúsculas.

### Directrices sobre el nombre de la unidad del recurso

  Debe seguir estas directrices cuando especifique el nombre de la unidad del recurso utilizando el campo resources.unit.name en la definición del recurso:

  * Utilice una palabra para el nombre de la unidad y utilice un signo de subrayado (_), en lugar de un espacio, para separar palabras. Por ejemplo, especifique **LLAMADA_API** en lugar de **LLAMADA API**.  
  * Especifique en mayúsculas todas las letras del nombre.
  
### Directrices sobre la calidad de la unidad del recurso

  Debe seguir estas directrices cuando especifique del tipo de cantidad del recurso utilizando el campo resources.unit.quantityType en la definición del recurso:
  
  * Utilice una palabra para el tipo de cantidad.
  * Especifique en mayúsculas todas las letras del tipo de cantidad.
  
### Directrices sobre el ID de agregación

  Debe seguir estas directrices cuando especifique el ID de agregación utilizando el campo aggregations.id en la definición del recurso:

  * Especifique en mayúsculas todas las letras del tipo de cantidad.
  * Utilice signo de subrayado (_), en lugar de un espacio, para separar palabras.
  * Asegúrese de que este ID comienza por el valor de aggregations.unit o que coincide con el mismo. Por ejemplo, puede especificar **LLAMADAS_API_AL_MES** para aggregations.id y especificar **LLAMADAS_API** para aggregations.unit.

### Directrices sobre la unidad de agregación

  Debe seguir estas directrices cuando especifique la unidad de agregación utilizando el campo aggregations.unit en la definición del recurso:
   
  * Utilice la forma singular para el nombre de la unidad.
  * Especifique en mayúsculas todas las letras del nombre de la unidad.
  * Asegúrese de que el nombre de unidad que especifique en el campo aggregations.unit sea un agregado del nombre de unidad que especifique en el campo resources.unit.name.
  
### Directrices sobre el grupo de agregación

  Debe utilizar letras minúsculas para el campo aggregations.aggregationGroup en la definición del recurso.
  
### Directrices sobre la fórmula de agregación

  Para el campo aggregations.formula de la definición del recurso, si desea utilizar operaciones aritméticas en la fórmula, debe utilizar la unidad de recurso como un operando y una expresión aritmética infix en la función de la fórmula. Por ejemplo, puede utilizar la fórmula siguiente para convertir Bytes a Megabytes:
  ```
  SUM({BYTE}/1048576)
  ```

## API REST de envío de datos de uso
{: #RAPIusesubmit}

Se factura a los usuarios de {{site.data.keyword.Bluemix_notm}} en función de la cantidad de recursos que utilicen. Por ejemplo, se puede facturar a los usuarios que utilizan servicios de base de datos en función de la cantidad de almacenamiento que utilizan sus aplicaciones.

Para utilizar el servicio de medición de {{site.data.keyword.Bluemix_notm}} para informar sobre los datos de uso, implemente la API del servicio de medición para informar sobre los datos de uso de la oferta. Consulte la [documentación de la API pública](https://ibm-bluemix-docs.github.io/usage-submission/) para ver más detalles.  

Debe automatizar el envío de uso por hora utilizando la API del servicio de medición. Puede alojar su envío automatizado en cualquier punto final de HTTPs válido que sea accesible en Internet público.
{: tip}

## Envío de registros de uso
{: #usage-records}

Los registros de uso son las entidades más pequeñas que contribuyen a los valores agregados de las métricas. Un registro de uso se construye mediante los campos siguientes:

| Nombre | Descripción                                           |
| ------ | ---------------------------------------------------- |
| resource_instance_id |  El ID de la instancia del recurso.  |
| plan_id | El contrato por el que se agrega y se califica el registro de uso.   |
| start  | Hora a partir de la que se mide el uso, especificada en milisegundos desde epoch.  |
| end  | Hora hasta la cual se mide el uso, especificada en milisegundos desde epoch.  |
| region  | La región del proveedor de la oferta en la que se mide el uso.  |
| measured_usage  | Una matriz de medidas con valores.  |
| consumer_id | Opcional. Este campo solo es necesario si se necesita la agregación a nivel de consumidor. Solo los proveedores de la oferta conocen el valor de consumer_id. |
{: caption="Tabla 1. Campos de un registro de uso" caption-side="top"}

Puede enviar varios registros de uso utilizando la llamada de API, y puede enviar un máximo de 100 registros de uso por llamada. El cuerpo de la respuesta incluye el estado de aceptación de cada registro de uso. Cualquier estado distinto de 201 viene acompañado de un código de error e indica por qué no se acepta el registro de uso. En la tabla siguiente se muestran los códigos de estado y la acción necesaria.

| Código de estado | Acción necesaria                                       |
| ------ | ---------------------------------------------------- |
| 500 |  Intente enviar de nuevo el registro de uso. Si el problema continúa, póngase en contacto con el equipo de medición de BSS. |
| 400 |  El registro de uso no tiene el formato correcto. Es posible que haya fallado la validación del esquema, que las medidas de los registros de uso sean incorrectas o que las horas de inicio y de finalización no estén dentro de las horas de suministro y de cese del suministro. Actualice el registro de uso y envíelo de nuevo.   |
| 424  | Los metadatos de la instancia del recurso tienen algunos problemas. Actualice los detalles de la instancia del recurso y vuelva a enviar el registro de uso.  |
| 404  | La definición de medición no se ha incorporado. Trabaje con el equipo de medición de BSS para comprobar si el recurso está incorporado y vuelva a enviar el registro de uso.  |
| 409  | El registro de uso es un duplicado. No intente volver a enviarlo de nuevo. |
{: caption="Tabla 2. Códigos de estado y acciones necesarias" caption-side="top"}
{: #actions}


  
