---


copyright:

  years: 2017, 2018

lastupdated: "2018-08-28"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}
{:tip: .tip}

# Integração de medição
{: #meteringintera}

O {{site.data.keyword.Bluemix}} suporta múltiplos modelos para agregar o uso de oferta. Os provedores de ofertas medem várias métricas sobre as instâncias provisionadas e enviam essas medidas para o serviço de medição. O serviço de classificação agrega o uso enviado em diferentes depósitos (instância, grupo de recursos e conta) com base no modelo que os provedores de oferta escolhem. Os modelos de agregação e classificação para todas as métricas em um plano estão contidos nos documentos de definição de medição e classificação para o plano.
{:shortdesc}

A lista a seguir descreve as expectativas para rastreamento e envio de uso:

*	Os provedores de oferta de terceiro não precisam enviar o uso para os planos grátis.
*	Os provedores de oferta de terceiro não precisam enviar o uso para os planos de assinatura mensais.
*	Para planos medidos, todos os provedores de oferta devem enviar o uso por hora (os planos Lite devem ser enviados a cada 15 minutos até 1 hora).
*	O provedor de oferta é responsável por automatizar o envio de uso, incluindo a automação que tenta respostas de falha novamente. 
O {{site.data.keyword.Bluemix_notm}} não fornece uma função de nova tentativa para envios com falha. Para obter mais
informações, consulte os códigos de status e a tabela de ações em
[Enviando registros de uso](/docs/third-party/submitusage.html#submitting-usage-records).
*	Os registros de uso do mês atual devem ser enviados, o mais tardar, até o dia 2 do mês seguinte.
*	O {{site.data.keyword.Bluemix_notm}} é configurado para um ciclo de faturamento mensal e o horário é representado em
Hora Universal Coordenada (UTC).
*  Os provedores de ofertas devem testar o envio de uso e validar seus resultados para informar como o ciclo de faturamento mensal é calculado.

Para obter informações gerais sobre precificação, consulte
[Como calcular os custos](https://console.bluemix.net/docs/billing-usage/estimating_costs.html#cost). 

## Propriedades de Configuração
{: #configure}

As propriedades a seguir definem como os envios de uso para os planos de oferta são medidos e taxados:

<dl>
<dt>Unidade</dt>
<dd>Métricas a serem medidas, por exemplo, ApiCall, Bytes, Horas, Instâncias e Nós.</dd>
<dt>Agregação</dt>
<dd>Como os dados de unidade medidos são compilados, por exemplo, INSTANCES_BY_MONTH ou ACTIVE_HOURS_BY_MONTH.</dd>
<dt>Modelo de medição</dt>
<dd>Como os dados de envio de uso são processados, como mostrado na tabela a seguir.</dd>
<dt>Nome do recurso</dt>
<dd>O nome do recurso que está sendo medido, por exemplo, armazenamento, instância, servidor virtual ou bytes transmitidos.</dd>
<dt>Nome da unidade</dt>
<dd>O nome descritivo da unidade se o nome padrão não for relevante para a oferta.</dd>
</dl>

## Tipos de modelo de medição
{: #metermodel}

A tabela a seguir mostra os modelos de medição disponíveis.

|  Tipo | Descrição  |
|-----|-----|
| standard_add | Incluir quantidade de todos os registros de uso enviados por um mês. | 
| standard_max  | Quantidade máxima de todos os registros de uso enviados por um mês. | 
| standard_avg | Quantidade média de todos os registros de uso enviados por um mês. |
| dailyateation_max | Máximo calculado diariamente. Somar todos os dias para o mês. | 
| dailyateation_avg | Média diária calculada. Somar todos os dias para o mês. |
| monthlyproration | Calculado semelhantemente ao rateio diário, mas o preço usado é o preço do plano que é dividido pelo número
total de dias para o mês (preço diário). |
{: caption="Tabela 1. Modelo de medição" caption-side="top"}

### Exemplos
Observe que a quantidade no painel em cada um dos exemplos a seguir é antes que o próximo uso seja enviado, mas depois que o uso atual for processado.

#### Inclusão padrão
Calcule os usos para o mês inteiro.

Fórmula: ADD (usos)

| Horário            | Uso Enviado | Cálculo | Quantidade no Painel |
|-----------------|:-------------:| ----------- |:---------------------:|
| Dia 1 (manhã) | 5             | 5           | 5                     |
| Dia 1 (noite)   | 5             | 5 + 5       | 10                    |
| Dia 2 (manhã) | 5             | 10 + 5      | 15                    |
| Dia 3 (manhã) | 5             | 15 + 5      | 20                    |
| Dia 4 (noite)   | 5             | 20 + 5      | 25                    |

#### Média padrão
Calcule a média dos usos para o mês inteiro. Observe que enviar um uso zero também conta para a média.

Fórmula: AVG (usos)

| Horário            | Uso Enviado | Cálculo             | Quantidade no Painel |
|-----------------|:-------------:| ----------------------- |:---------------------:|
| Dia 1 (manhã) | 4             | 4 / 1                   | 4                     |
| Dia 1 (noite)   | 0             | (4 + 0) / 2             | 2                     |
| Dia 2 (manhã) | 5             | (4 + 0 + 5) / 3         | 3                     |
| Dia 3 (manhã) | 3             | (4 + 0 + 5 + 3) / 4     | 3                     |
| Dia 4 (noite)   | 3             | (4 + 0 + 5 + 3 + 3) / 5 | 3                     |

#### Máximo padrão
Calcule o máximo dos usos para o mês inteiro.

Fórmula: MAX (usos)

| Horário            | Uso Enviado  | Cálculo  | Quantidade no Painel |
|-----------------|:--------------:| ------------ |:---------------------:|
| Dia 1 (manhã) | 5              | MAX (5)       | 5                     |
| Dia 1 (noite)   | 10             | MAX (5, 10)   | 10                    |
| Dia 2 (manhã) | 0              | MAX (10, 0)   | 10                    |
| Dia 3 (manhã) | 15             | MAX (10, 15)  | 15                    |
| Dia 4 (noite)   | 1              | MAX(15, 1)   | 15                    |

#### Média de rateio diária
Calcule o uso médio para cada dia e calcule a média para o mês. A média de cada dia é somada e dividida pelo número de dias atualmente passados (em UTC).

Fórmula: adição (média diária) / Número de dias passados no período de faturamento

Observe que a quantidade pode mudar durante todo o mês, mas o que é taxado é o uso médio por dia.

Dado um mês de 30 dias:

| Horário               | Uso Enviado    | Média diária | Cálculo                            | Quantidade no Painel *                           |
| ------------------ | :--------------: | ------------- | ------------------                     | :----------------------------------------------: |
| Dia 1 (manhã)    | 8                | 8 / 1         | 8 / 1                                  | 8                                                |
| Dia 1 (noite)      | 3                | (8 + 3) / 2   | 5,5 / 1                                | 5,5 (No dia 1 EOD)                               |
| Dia 2 (manhã)    | 2                | 2 / 1         | (5,5 + 2) / 2                          | 3,75                                             |
| Dia 2 (noite)      | 5                | (2 + 5) / 2   | (5.5 + 3.5) / 2                        | 4.5 (No Dia 2 EOD)                               |
| Dia 3 ao Dia 15    | 1                | 1 / 1         | (5,5 + 3,5 + (1 + 13)  / 15            | 1.4666 (No Dia 15 EOD)                          |
| Dia 15 ao Dia 30   | 0                | 0 / 1         | (5,5 + 3,5 + (1 \* 12) + (0  \* 15) / 30 | 0,7333  (no dia 30 - final do dia)                          |

\* Conforme visto no mesmo dia que o momento em que o uso foi enviado.

#### Máximo de rateio Diário
Calcule o uso máximo por dia e calcule a média para o mês. O máximo de cada dia é somado e dividido pelo número de dias atualmente passados (em UTC).

Fórmula: adição (máximo diário)/número de dias passados no período de faturamento

Observe que a quantidade pode mudar ao longo do mês, mas o que é taxado é o uso máximo por dia.

Dado um mês de 30 dias:

| Horário             | Uso Enviado  | Máximo Diário | Cálculo                    | Quantidade no Painel * |
|------------------|:--------------:| --------- | ------------------------------ |:----------------------:|
| Dia 1 (manhã)  | 0              | MAX (0)    | 0 / 1                          | 0                      |
| Dia 1 (noite)    | 1              | MAX (0, 1) | 1 / 1                          | 1                      |
| Dia 2 ao Dia 15  | 1              | MAX (1)    | (1 + 1 +...) / day            | 1                      |
| Dia 15 ao Dia 30 | 0              | MAX (0)    | (1 + (1 * 14) + 0 + ...) / day | < 1                    |

\* Conforme visto no mesmo dia que o momento em que o uso foi enviado.

## Exemplos de escala de medição e classificação
{: #scale-examples}

É possível usar a configuração de ajuste de escala para compilar a quantidade de unidade de forma diferente do que é enviado
em envios de uso para o que é exibido no Painel de uso e o que é usado para os cálculos de classificação e de custo. Os exemplos a seguir demonstram esses cenários:

### Você deseja mais granularidade do que os usuários veem
Você deseja enviar usos a um nível mais granular, mas deseja mostrar aos clientes um número mais legível.

Por exemplo, você pode desejar medir o tráfego de uma instância em bytes e desejar os valores agregados em megabytes. Para fazer isso, inclua um `scale` de 1024 na configuração de **medição**.

### Você deseja mais granularidade do que a sua configuração de precificação tem
Você precifica suas métricas como US$ X/gigabyte, mas deseja enviá-las em megabytes. Se a métrica for precificada em
US$ 1/gigabyte, mas um usuário usar 0,5 megabytes, será cobrado US$ 1 porque a precificação é por gigabyte. Você inclui um `scale` de 1024 na configuração de **classificação** e configura `clip` como `true`.

Isso retém true caso sua métrica também seja precificada como US$ X por 100 chamadas API (ou algum outro tamanho de pacote).

### Você deseja escalar os níveis de medição e de classificação
É possível incluir o ajuste de escala nas configurações de medição e de classificação. Se desejar enviar em bytes, mas mostrar megabytes para o usuário, você configurará a escala de medição para 1024. Se o preço da métrica estiver em gigabytes, você também configurará a escala de classificação para 1024.

## Modelos de precificação
{: #pricing}

A tabela a seguir fornece informações detalhadas sobre os modelos de precificação que estão disponíveis. Para muitas das métricas disponíveis, você seleciona um modelo de precificação associado.

| Modelo          | Descrição | Cálculo | Exemplo (5000 quantity) |
|:-----------------|:-------------|:----------- |:---------------------|
| Linear         | Multiplique o preço unitário por recurso (P) pela quantidade de uso (Q) para obter a quantia total (T)  | P*Q    | P=$1 T = 1 * 5000 = $5000        |
| Rateio      | Multiplique o preço unitário diário por recurso (P) pela quantidade de uso diário (Q) para obter a quantia diária total. 
O total de encargos envolve o acúmulo dos encargos para todos os dias do mês.         | T = (pd * Q1) + ... + (Pd *Qn)     | <ul><li>P = US$ 30</li><li>Pd (preço diário) = US$ 30/30 = US$ 1 (supondo 30 dias em um mês)</li><li>T1 = US$ 1 * 1 = US$ 1</li><li>T2 = US$ 1 * 0 = US$ 0</li><li>Tn = 1 * 1 = US$ 1</li><li>T = US$ 1 + US$ 0 +...+US$ 1 = US$ 5000</li></ul>     |
| Camada simples (camada granular)  | Um modelo P*Q no qual o preço unitário para todo o consumo é determinado pela
camada em que a quantidade se encaixa. | <ul><li>Se Q for <=Q1, T=P1*Q</li><li>Se Q1 < Q <=Q2, T=P2*Q</li><li>Se Q2 < Q <=Q3, T=P3*Q</li></ul>     |   <ul><li>Q1 = 1000, P1 = US$ 1</li><li>Q2 = 2500, P2 = US$ 0,9</li><li>Q3 = 10000, P3 = US$ 0,75</li><li>T = US$ 0,75 * 5000 = US$ 3750</li></ul>              |
| Camada graduada (camada da etapa)   | O preço por unidade varia conforme a quantidade consumida se move para diferentes camadas predefinidas. O encargo total envolve acumular os encargos das camadas anteriores           | <ul><li>T1=P1*Q (0 < Q</li><li>Se Q1 < Q <=Q2, T=T2</li><li>Se Q2 < Q <=Q3, T=T3</li></ul>     | <ul><li>Q1 = 1000, P1 = US$ 1, T1 = 1*1000</li><li>Q2 = 1500, P2 = US$ 0,9, T2 = 0,9*1500</li><li>Q3 = 10000, P3 = US$ 0,75, T3 = 0,75*2500</li><li>T = 1000 + 1350 + 1875 = US$ 4225</li></ul>          |
| Camada de bloco (até)           | A quantia total cobrada é estabelecida por uma quantidade "até" que não varia dentro do bloco | <ul><li>Se Q for <=Q1, T=T1</li><li>Se Q1 < Q <=Q2, T=T2</li><li>Se Q2 < Q <=Q3, T=T3</li></ul>    |  <ul><li>Q1 = 1000, T1 = US$ 0</li><li>Q2 = 2500, T2 = 2500</li><li>Q3 = 10000, T3 = US$ 4500</li><li>T = US$ 4500</li></ul>            |


