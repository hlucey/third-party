---

 
copyright:

  years: 2017, 2019

lastupdated: "2019-06-05" 

keywords: plans of the resource, use characters A, usage records, metered plans, submitting usage 

subcollection: third-party

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:tip: .tip}
{:new_window: target="_blank"}

# Enviando o uso para planos medidos
{: #submitusage}

É requerido que você envie o uso para todas as instâncias de serviço ativo a cada hora. Não relatar o uso pode levar
à perda de coleta de renda para a IBM, o que pode causar uma perda de compartilhamento de renda para os provedores da
oferta.
{:shortdesc}

## Como o processo funciona
{: #process-flow}

As etapas a seguir descrevem o processo para enviar o uso:

1. Envie um teste de uso inicial por meio da ferramenta API de REST de Envio de uso para validar que seus planos medidos estão configurados corretamente.
2. Automatize o envio contínuo por hora para a ferramenta API de Rest de Envio de uso para cada plano medido. Será possível hospedar esses envios automatizados sempre que você desejar, desde que a SSO padrão seja suportada.
3. Os registros de uso são agregados com base no modelo de medição e a quantidade total é exibida no Painel de uso no console do {{site.data.keyword.Bluemix_notm}}.
4. A quantidade da unidade agregada do processo de medição é usada, o custo é aplicado e a quantia que o usuário deve para a instância de serviço é calculada.
5. No término do mês, o custo calculado final é a quantia gerada para o usuário.

## Pré-requisito
{: #prereqs}

Revise os pré-requisitos a seguir para ativar a medição para seu serviço:

* O catálogo de precificação é atualizado com preços para todas as métricas debitáveis nos planos do recurso.
* As definições de medição e de classificação para todos os planos no recurso são verificadas e integradas.

## Diretrizes para enviar o uso 
{: #metering_guidelines}

### Diretrizes de envio
{: #submission-guidelines}

Consulte as diretrizes a seguir ao usar o serviço de medição do {{site.data.keyword.Bluemix_notm}} para enviar dados de uso de recurso:

* O horário de início e o horário de encerramento representam o intervalo de tempo durante o qual as medidas foram coletadas. Os horários não são dependentes do horário em que o registro de uso é enviado para as APIs de medição.
* Os registros de uso são fatos. Não atualize o registro de uso depois de criá-lo. Um local é especificado quando você cria com êxito um registro de uso. Se um código de erro for retornado, consulte os [Códigos de status e as ações necessárias](/docs/third-party?topic=third-party-submitusage#usage-records) que você pode ter que tomar.
* Um registro de uso é identificado com exclusividade pela assinatura ` account_id/resource_group_id/resource_instance_id/consumer_id/plan_id/region/start/end`. Quando um registro de uso é processado, qualquer outro registro de uso com a mesma assinatura é rejeitado como uma duplicata.
* Não combine a interação com o serviço de medição com quaisquer outros serviços. As solicitações devem ser tratadas
individualmente, mesmo caso a medição inicie e termine com o fornecimento e a remoção do fornecimento da instância.
* Os dados de uso do recurso devem ser enviados para o serviço de medição uma vez a cada 2 a 24 horas. A frequência com que você envia seus dados de uso depende da frequência com que suas métricas de uso mudam.
* Os registros de uso devem ser enviados dentro de dois dias a partir do momento da conclusão da medição. Os registros de uso mais antigos são rejeitados.
* Um envio bem-sucedido retorna um código de resposta de 201. Se qualquer outro código de resposta for retornado, atualize e reenvie os dados até que você receba o código 201.

A seguir estão as melhores práticas para enviar o uso:

* Recomenda-se que os provedores de serviços enviem o uso a cada 1 hora para que o usuário não veja um grande atraso entre o
horário do consumo do recurso e o horário no qual o custo é refletido nas contas.
* Somente tente novamente o envio dos registros de uso se ocorrer uma falha genuína com a
solicitação anterior. Não reenvie os registros de uso que foram aceitos com êxito.

### Diretrizes de ID do serviço
{: #id-guidelines}

  Deve-se seguir essas diretrizes ao especificar o ID do serviço usando o campo de ID na definição de recurso:
  * Inicie o ID com um caractere alfanumérico.
  * Use os caracteres A - Z, a - z e 0 - 9. Os únicos caracteres especiais que podem ser usados são hifens (-) e sublinhados (_).
  * Siga a convenção Camel Case se o ID contiver mais de uma palavra.
  * Assegure-se de que o comprimento máximo do ID seja 50 caracteres.

### Diretrizes de nome do recurso
{: #resource-name}

  Deve-se seguir estas diretrizes ao especificar o nome do recurso usando o campo resources.name na definição de recurso:

  * Use somente palavras que descrevam seus recursos. Por exemplo, **Storage** ou **ApiCalls**. 
  * Siga a convenção Camel Case se o nome contiver mais de uma palavra.
  * Altere para letras maiúsculas o primeiro caractere do nome.

### Diretrizes de nome da unidade de recurso
{: #resource-unti}

  Deve-se seguir estas diretrizes ao especificar o nome da unidade de recurso usando o campo resources.unit.name na definição do recurso:

  * Use uma palavra para o nome da unidade e use um sublinhado (_), em vez de um espaço, para separar as palavras. Por exemplo, especifique **API_CALL** em vez de **API CALL**.  
  * Altere para letras maiúsculas todas as letras do nome.
  
### Diretrizes de quantidade da unidade de recurso
{: #unit-quantity}

  Deve-se seguir estas diretrizes ao especificar o tipo de quantidade de recursos usando o campo resources.unit.quantityType na definição de recurso:
  
  * Use uma palavra para o tipo de quantidade.
  * Altere para letras maiúsculas todas as letras do tipo de quantidade.
  
### Diretrizes de ID de agregação
{: #aggregation}

  Deve-se seguir estas diretrizes ao especificar o ID de agregação usando o campo aggregations.id na definição de recurso:

  * Altere para letras maiúsculas todas as letras do tipo de quantidade.
  * Use um sublinhado (_), em vez de um espaço, para separar as palavras.
  * Assegure-se de que esse ID inicie com ou corresponda ao valor de aggregations.unit. Por exemplo, é possível especificar **API_CALLS_PER_MONTH** para aggregations.id e especificar **API_CALLS** para aggregations.unit.

### Diretrizes de unidade de agregação
{: #aggregation-unit}

  Deve-se seguir estas diretrizes ao especificar a unidade de agregação usando o campo aggregations.unit na definição de recurso:
   
  * Use formulário singular para o nome da unidade.
  * Altere para letras maiúsculas todas as letras do nome da unidade.
  * Assegure-se de que o nome da unidade especificado no campo aggregations.unit seja uma agregação do nome da unidade especificado no campo resources.unit.name.
  
### Diretrizes de grupo de agregação
{: #aggregation-group}

  Deve-se usar letras minúsculas para o campo aggregations.aggregationGroup na definição de recurso.
  
### Diretrizes de fórmula de agregação
{: #aggregation-formula}

  Para o campo aggregations.formula na definição de recurso, se você desejar usar operações aritméticas na fórmula, deve-se usar a unidade de recurso como um operando e usar uma expressão aritmética infix na função da fórmula. Por exemplo, é possível usar a fórmula a seguir para converter Bytes em Megabytes:
  ```
  SUM({BYTE}/1048576)
  ```

## API de REST de envio de uso
{: #RAPIusesubmit}

Os usuários do {{site.data.keyword.Bluemix_notm}} são cobrados com base na quantia de recursos que eles usam. Por exemplo, os usuários que usam serviços de banco de dados podem ser cobrados com base na quantia de armazenamento que os seus aplicativos usam.

Para usar o serviço de medição do {{site.data.keyword.Bluemix_notm}} para relatar dados de uso, implemente a API de serviço de medição para relatar os dados de uso de sua oferta. Consulte a [documentação da API pública](https://ibm-bluemix-docs.github.io/usage-submission/){: new_window} ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo") para obter mais detalhes.  

É necessário automatizar o envio de uso por hora usando a API de serviço de medição. É possível hospedar seu envio automatizado em qualquer terminal HTTPs válido que esteja acessível na Internet pública.
{: tip}

## Enviando registros de uso
{: #usage-records}

Os registros de uso são as menores entidades que contribuem para os valores agregados das métricas. A tabela a seguir fornece informações sobre os campos usados para construir um registro de uso:

| Nome | Descrição                                           |
| ------ | ---------------------------------------------------- |
| resource_instance_id |  O ID da instância de recurso.  |
| plan_id | O contrato pelo qual o registro de uso é agregado e taxado.   |
| start  | O tempo desde o qual o uso é medido, especificado em milissegundos, desde a época.  |
| end  | O tempo até o qual o uso é medido, especificado em milissegundos, desde a época.  |
| região  | A região do provedor de oferta no qual o uso é medido.  |
| measured_usage  | Uma matriz de medidas com valores.  |
| consumer_id | Opcional. Esse campo será obrigatório somente se a agregação for necessária em um nível do consumidor. Somente os provedores de oferta sabem o valor de consumer_id. |
{: caption="Tabela 1. Campos de um registro de uso" caption-side="top"}

É possível enviar múltiplos registros de uso usando a chamada API e é possível enviar um máximo de 100 registros de uso por chamada. O corpo de resposta inclui o status de aceitação de cada registro de uso. Qualquer status diferente de 201 é acompanhado por um código de erro e indica a razão pela qual o registro de uso não é aceito. A tabela a seguir lista os códigos de status e a ação necessária.

| Código de status | Ação necessária                                       |
| ------ | ---------------------------------------------------- |
| 500 |  Tente enviar o registro de uso novamente. Se o problema continuar, entre em contato com a equipe de medição BSS. |
| 400 |  O registro de uso não está no formato correto. A validação de esquema falhou, as medidas nos registros de uso estão
incorretas ou os horários de início e de encerramento não estão entre os horários de fornecimento e de remoção de
fornecimento. Atualize o registro de uso e envie-o novamente.   |
| 424  | Os metadados da instância de recurso têm alguns problemas. Atualize os detalhes da instância de recurso e envie o registro de uso novamente.  |
| 404  | A definição de medidor não estava embarcada. Trabalhe com a equipe de medição do BSS para verificar se o recurso está
integrado e envie o registro de uso novamente.  |
| 409  | O registro de uso é uma duplicata. Não tente submetê-lo novamente. |
{: caption="Tabela 2. Códigos de status e ações necessárias" caption-side="top"}
{: #actions}


  
