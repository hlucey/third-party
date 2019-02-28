---


copyright:

  years: 2017, 2019

lastupdated: "2019-01-30"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}
{:tip: .tip}

# Integración de mediciones
{: #meteringintera}

{{site.data.keyword.Bluemix}} da soporte a varios modelos para calcular el uso de la oferta. Los proveedores de la oferta miden varias métricas en las instancias suministradas y envían dichas medidas al servicio de medición. El servicio de evaluación agrega el uso enviado en diferentes grupos (instancia, grupo de recursos y cuenta) en función del modelo que eligen los proveedores de la oferta. Los modelos de agregación y de evaluación para todas las métricas de un plan están contenidos en los documentos de definición de medición y evaluación del plan.
{:shortdesc}

En la lista siguiente se describen las expectativas para el seguimiento y el envío del uso:

*	No es necesario que los proveedores de la oferta (terceros) envíen datos sobre uso para planes gratuitos.
*	No es necesario que los proveedores de la oferta (terceros) envíen datos sobre uso para planes de suscripción mensual.
*	Para los planes de medición, todos los proveedores de la oferta deben enviar datos sobre uso cada hora (para los planes Lite se deben enviar entre cada 15 minutos y 1 hora).
*	El proveedor de la oferta es el responsable de automatizar el envío de datos sobre uso, incluida la automatización que intenta de nuevo las respuestas de error. {{site.data.keyword.Bluemix_notm}} no proporciona una función de reintento para envíos fallidos. Para obtener más información, consulte los códigos de estado y la tabla de acciones en [Envío de registros de uso](/docs/third-party?topic=third-party-submitusage#usage-records).
*	Los registros de uso correspondientes al mes actual se deben enviar, a más tardar, el segundo día del mes siguiente.
*	{{site.data.keyword.Bluemix_notm}} está configurado para un ciclo de facturación mensual y el tiempo está representado en UTC (Hora Universal Coordinada).
*  Los proveedores de la oferta deben probar el envío de datos sobre uso y validar sus resultados para informar sobre cómo se calcula el ciclo de facturación mensual.

Para obtener información general sobre los precios, consulte [Cómo calcular los costes](/docs/billing-usage?topic=billing-usage-cost#cost). 

## Propiedades de configuración
{: #configure}

Las siguientes propiedades definen cómo se miden y se evalúan los envíos de datos sobre uso para los planes de la oferta:

<dl>
<dt>Unidad</dt>
<dd>Métricas que se deben medir, por ejemplo, Llamada a API, Bytes, Horas, Instancias y Nodos.</dd>
<dt>Agregación</dt>
<dd>Cómo se compilan los datos de las unidades medidas, por ejemplo INSTANCES_BY_MONTH o ACTIVE_HOURS_BY_MONTH.</dd>
<dt>Modelo de medición</dt>
<dd>Cómo se procesan los datos del envío de datos sobre uso, tal como se muestra en la tabla siguiente.</dd>
<dt>Nombre del recurso</dt>
<dd>El nombre del recurso que se mide, por ejemplo almacenamiento, instancia, servidor virtual o bytes transmitidos.</dd>
<dt>Nombre de unidad</dt>
<dd>El nombre descriptivo de la unidad, si el nombre predeterminado no es relevante para la oferta.</dd>
</dl>

## Tipos de modelos de medición
{: #metermodel}

En la tabla siguiente se muestran los modelos de medición disponibles.

|  Tipo | Descripción  |
|-----|-----|
| standard_add | Suma de cantidades de todos los registros de uso enviados durante un mes. | 
| standard_max  | Cantidad máxima de todos los registros de uso enviados durante un mes. | 
| standard_avg | Cantidad media de todos los registros de uso enviados durante un mes. |
| dailyproration_max | Máximo diario calculado. Se suman todos los días del mes. | 
| dailyproration_avg | Promedio diario calculado. Se suman todos los días del mes. |
| monthlyproration | Se calcula de forma similar al prorrateo diario, pero el precio utilizado es el precio del plan dividido por el número total de días del mes (precio diario). |
{: caption="Tabla 1. Modelo de medición" caption-side="top"}

### Ejemplos
{: #examples}

Observe que la cantidad que aparece en el panel de control de cada uno de los siguientes ejemplos es anterior a que se envíen los siguientes datos de uso, pero posterior a que se procesen los datos de uso actual.

#### Suma estándar
{: #standard-add}

Calcular los datos de uso de todo el mes.

Fórmula: ADD(datos uso)

| Momento            | Datos uso enviados | Cálculo | Cantidad en panel de control |
|-----------------|:-------------:| ----------- |:---------------------:|
| Día 1 (mañana) | 5             | 5           | 5                     |
| Día 1 (noche)   | 5             | 5 + 5       | 10                    |
| Día 2 (mañana) | 5             | 10 + 5      | 15                    |
| Día 3 (mañana) | 5             | 15 + 5      | 20                    |
| Día 4 (noche)   | 5             | 20 + 5      | 25                    |
{: caption="Tabla 2. Cálculos de uso mensual" caption-side="top"}

#### Promedio estándar
{: #standard-average}

Calcular el promedio de los datos de uso de todo el mes. Tenga en cuenta que el envío de un uso cero también cuenta en el promedio.

Fórmula: AVG(datos uso)

| Momento            | Datos uso enviados | Cálculo             | Cantidad en panel de control |
|-----------------|:-------------:| ----------------------- |:---------------------:|
| Día 1 (mañana) | 4             | 4 / 1                   | 4                     |
| Día 1 (noche)   | 0             | (4 + 0) / 2             | 2                     |
| Día 2 (mañana) | 5             | (4 + 0 + 5) / 3         | 3                     |
| Día 3 (mañana) | 3             | (4 + 0 + 5 + 3) / 4     | 3                     |
| Día 4 (noche)   | 3             | (4 + 0 + 5 + 3 + 3) / 5 | 3                     |
{: caption="Tabla 3. Cálculos de uso mensual promedio" caption-side="top"}

#### Máximo estándar
{: #standard-max}

Calcular el máximo de los datos de uso de todo el mes.

Fórmula: MAX(datos uso)

| Momento            | Datos uso enviados  | Cálculo  | Cantidad en panel de control |
|-----------------|:--------------:| ------------ |:---------------------:|
| Día 1 (mañana) | 5              | MAX(5)       | 5                     |
| Día 1 (noche)   | 10             | MAX(5, 10)   | 10                    |
| Día 2 (mañana) | 0              | MAX(10, 0)   | 10                    |
| Día 3 (mañana) | 15             | MAX(10, 15)  | 15                    |
| Día 4 (noche)   | 1              | MAX(15, 1)   | 15                    |
{: caption="Tabla 4. Cálculos de uso mensual máximo" caption-side="top"}

#### Promedio de prorrateo diario
{: #proration-average}

Calcular el uso promedio de cada día y calcular el promedio del mes. El promedio de cada día se suma y se divide por el número de días que han pasado (en UTC).

Fórmula: Suma(promedio diario) / Número de días que han pasado del periodo de facturación

Tenga en cuenta que la cantidad puede cambiar a lo largo del mes, pero lo que se evalúa es el uso promedio por día.

En el caso de un mes de 30 días:

| Momento               | Datos uso enviados    | Promedio diario | Cálculo                            | Cantidad en panel de control*                           |
| ------------------ | :--------------: | ------------- | ------------------                     | :----------------------------------------------: |
| Día 1 (mañana)    | 8                | 8 / 1         | 8 / 1                                  | 8                                                |
| Día 1 (noche)      | 3                | (8 + 3) / 2   | 5,5 / 1                                | 5,5 (Día 1 EOD)                               |
| Día 2 (mañana)    | 2                | 2 / 1         | (5,5 + 2) / 2                          | 3,75                                             |
| Día 2 (noche)      | 5                | (2 + 5) / 2   | (5,5 + 3,5) / 2                        | 4,5 (Día 2 EOD)                               |
| Día 3 a Día 15    | 1                | 1 / 1         | (5,5 + 3,5 + (1 + 13)  / 15            | 1,4666  (Día 15 EOD)                          |
| Día 15 a Día 30   | 0                | 0 / 1         | (5,5 + 3,5 + (1 \* 12) + (0  \* 15) / 30 | 0,7333  (Día 30 EOD)                          |
{: caption="Tabla 5. Cálculos de uso promedio al día y de promedio mensual" caption-side="top"}

\* Datos observados en el mismo día que cuando se enviaron los datos de uso.

#### Máximo de prorrateo diario
{: #daily-proration}

Calcular el uso máximo de cada día y calcular el promedio correspondiente al mes. El máximo de cada día se suma y se divide por el número de días que han pasado (en UTC).

Fórmula: Suma(máximo diario) / Número de días que han pasado del periodo de facturación

Tenga en cuenta que la cantidad puede cambiar a lo largo del mes, pero lo que se evalúa es el uso máximo por día.

En el caso de un mes de 30 días:

| Momento             | Datos uso enviados  | Máx. diario | Cálculo                    | Cantidad en panel de control* |
|------------------|:--------------:| --------- | ------------------------------ |:----------------------:|
| Día 1 (mañana)  | 0              | MAX(0)    | 0 / 1                          | 0                      |
| Día 1 (noche)    | 1              | MAX(0, 1) | 1 / 1                          | 1                      |
| Día 2 a Día 15  | 1              | MAX(1)    | (1 + 1 + ...) / día            | 1                      |
| Día 15 a Día 30 | 0              | MAX(0)    | (1 + (1 * 14) + 0 + ...) / día | < 1                    |
{: caption="Tabla 6. Cálculos de uso máximo al día y de promedio mensual" caption-side="top"}

\* Datos observados en el mismo día que cuando se enviaron los datos de uso.

## Ejemplos de escalas de medición y evaluación
{: #scale-examples}

Puede utilizar la configuración de escalado para compilar la cantidad de la unidad de forma distinta entre lo que se envía en envíos de datos de uso, lo que se muestra en el panel de control de uso, y lo que se utiliza para evaluar y calcular los costes. En los ejemplos siguientes se muestran estos casos de ejemplo:

### Desea más granularidad de la que ven los usuarios
{: #users}

Desea enviar datos de uso a un nivel más granular, pero desea mostrar a los clientes un número más legible.

Por ejemplo, supongamos que desea medir el tráfico de la instancia en bytes y desea sumar los valores en megabytes. Para ello, añada una `escala` de 1024 a la configuración de la **medición**.

### Desea más granularidad de la que ofrece la configuración de precios
{: #pricing-configuration}

El precio de la métrica se calcula como X $ / gigabyte, pero desea enviarlo en megabytes. Si el precio de la métrica es de 1 $ / gigabyte, pero un usuario utiliza 0,5 megabytes, se le cobra 1 $, ya que el precio es por gigabyte. Puede añadir una escala (`scale`) de 1024 a la configuración de evaluación (**rating**) y definir `clip` como `true`.

Esto también se aplica si el precio de la métrica es de X $ por 100 llamadas a API (u otro tamaño de paquete).

### Desea escalar a nivel de medición y de evaluación
{: #metering-rating}

Puede añadir escalado a las configuraciones de medición y de evaluación. Si desea enviar los datos en bytes pero mostrarlos en megabytes al usuario, configure la escala de medición de 1024. Si el precio de la métrica está en gigabytes, también puede configurar la escala de evaluación para que sea 1024.

## Modelos de precios
{: #pricing}

En la tabla siguiente se proporciona información detallada sobre los modelos de precios que están disponibles. Para muchas de las métricas disponibles, debe seleccionar un modelo de precios asociado.

| Modelo          | Descripción | Cálculo | Ejemplo (cantidad de 5000) |
|:-----------------|:-------------|:----------- |:---------------------|
| Lineal         | Multiplique el precio unitario por recurso (P) por la cantidad de uso (Q) para obtener la cantidad total (T)  | P*Q    | P=1 $ T=1*5000 =5000 $        |
| Prorrateo      | Multiplique el precio unitario diario por recurso (P) por la cantidad de uso diario (Q) para obtener la cantidad diaria total. El cargo total implica sumar los cargos correspondientes a todos los días del mes.         | T= (pd * Q1) + ...+(Pd *Qn)     | <ul><li>P= 30 $</li><li>Pd (precio diario) =30/30 $=1 $ (suponiendo que el mes tiene 30 días)</li><li>T1= 1 $ * 1 =1 $</li><li>T2 = 1 $ * 0 =0 $</li><li>Tn = 1 * 1 =1 $</li><li>T = 1 $ + 0 $ +...+1 $ = 5000 $</li></ul>     |
| Nivel simple (nivel granular)  | Modelo A P*Q en el que el precio unitario de todo el consumo se determina según el nivel al que pertenece la cantidad.           | <ul><li>Si Q es <=Q1, T=P1*Q</li><li>Si Q1 < Q <=Q2, T=P2*Q</li><li>Si Q2 < Q <=Q3, T=P3*Q</li></ul>     |   <ul><li>Q1=1000, P1=1 $</li><li>Q2=2500, P2=0,9 $</li><li>Q3=10000, P3=0,75 $</li><li>T=0,75 $*5000=3750 $</li></ul>              |
| Nivel graduado (nivel de paso)   | El precio por unidad varía a medida que la cantidad consumida se mueve entre diferentes niveles predefinidos. El cargo total implica sumar los cargos correspondientes a los niveles anteriores           | <ul><li>T1=P1*Q (0 < Q</li><li>Si Q1 < Q <=Q2, T=T2</li><li>Si Q2 < Q <=Q3, T=T3</li></ul>     | <ul><li>Q1=1000, P1=$1, T1=1*1000</li><li>Q2=1500, P2=0,9 $, T2=0,9*1500</li><li>Q3=10000, P3=0,75 $, T3=0,75*2500</li><li>T=1000 +1350+1875=4225 $</li></ul>          |
| Nivel de bloque (hasta)           | La cantidad total facturada se establece mediante una cantidad "hasta" que no varía dentro del bloque     | <ul><li>Si Q es <=Q1, T=T1</li><li>Si Q1 < Q <=Q2, T=T2</li><li>Si Q2 < Q <=Q3, T=T3</li></ul>    |  <ul><li>Q1=1000, T1=0 $</li><li>Q2=2500, T2=2500</li><li>Q3=10000, T3=4500 $</li><li>T=4500 $</li></ul>            |
{: caption="Tabla 7. Modelos de precios" caption-side="top"}

