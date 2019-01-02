---


copyright:
  years: 2018
lastupdated: "2018-11-29"


---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:note: .note}
{:download: .download}

# Etapa 3. Desenvolvendo e hospedando os brokers de serviço
{: #step3-osb}

Ao usar os metadados exportados do console de gerenciamento de recurso, é possível construir um ou mais novos
brokers de serviço na linguagem de programação de sua escolha.
{:shortdesc}

Os brokers de serviço gerenciam o ciclo de vida de serviços. A plataforma {{site.data.keyword.Bluemix_notm}} interage com brokers de serviço para provisionar e gerenciar as instâncias de serviço e as ligações de serviço. É possível fornecer valores de metadados válidos para criar uma Resposta de API RESTful bem-sucedida quando uma Solicitação é executada.

É possível construir seu broker usando uma combinação dos metadados exportados do console de gerenciamento de recursos, nossas amostras do broker de serviço público do {{site.data.keyword.Bluemix_notm}} e a documentação da API do Broker de Recurso.

## Antes de começar
{: #pre-reqs}

Assegure-se de iniciar a etapa 1 e concluir a etapa 2:
1. [ Anúncios de serviço de autor e anúncio de marketing ](/docs/third-party/cis1-docs-marketing.html).
2. [Defina sua oferta no console de gerenciamento de recurso](/docs/third-party/cis2-rmc-define.html).


## Visualize o cenário de fornecimento de plataforma do  {{site.data.keyword.Bluemix_notm}}
{: #scenario}

Você está desenvolvendo um Open Service Broker que trabalha com a plataforma {{site.data.keyword.Bluemix_notm}}. Veja nosso [Cenário de fornecimento](/docs/third-party/platform.html#provisioning-scenario-pulling-it-all-together) para obter um entendimento de como a criação de recursos funciona.

## Familiarize-se com a especificação do OSB
{: #learn-osb}

O {{site.data.keyword.Bluemix_notm}} usa a especificação do Open Service Broker API (OSB) `versão 2.12`. Leia e familiarize-se com a [Especificação do Open Broker API](https://github.com/openservicebrokerapi/servicebroker/blob/v2.12/spec.md){: new_window} ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo") e use o arquivo leia-me como um guia para saber mais.

## Visualize nossas amostras do  {{site.data.keyword.Bluemix_notm}}  broker
{: #samples}

[https://github.com/IBM/sample-resource-service-brokers](https://github.com/IBM/sample-resource-service-brokers){: new_window} ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")

Nem todos os idiomas são representados por uma amostra. Se for necessário um broker Python de amostra, por exemplo, será possível localizar uma amostra do Cloud Foundry procurando o Google. Talvez seja necessário ajustar essa amostra para atender aos requisitos do OSB.
{: note}

## Visualize nossa documentação do Open Service Broker API do {{site.data.keyword.Bluemix_notm}}
{: #docs}

Os brokers de serviço podem ser desenvolvidos com um entendimento da [API do Open Service Broker do {{site.data.keyword.Bluemix_notm}}](https://{DomainName}/apidocs/ibm-cloud-osb-api){: new_window}![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo"). Familiarize-se com a API do Broker e como ela interage com os seus brokers.

O Open Service Broker do {{site.data.keyword.Bluemix_notm}} estende a especificação do Open Service Broker 2.12.
{: tip}

### Lógica de terminal necessária para todos os brokers de serviço

Os brokers de serviço devem fornecer um conjunto padrão de valores de metadados que são consumidos pelas APIs REST, e os brokers do {{site.data.keyword.Bluemix_notm}} devem ter lógica para os terminais/caminhos da API REST a seguir:

<dl>
  <dt>catálogo (GET)</dt>
  <dd>Retorna os metadados do catálogo incluídos em seu broker. Muitos valores de metadados do catálogo extras não são retornados - esses valores são incluídos exclusivamente dentro do console de gerenciamento de recurso e armazenados no Catálogo do {{site.data.keyword.Bluemix_notm}}.</dd>
  <dt>instâncias de recurso (PUT)</dt>
  <dd>Provisionar sua instância de serviço</dd>
  <dt>instâncias de recurso (DELETE)</dt>
  <dd>Desprovisões sua instância de serviço.</dd>
  <dt>instâncias de recurso (PATCH)</dt>
  <dd>Atualiza sua instância de serviço.</dd>
</dl>

**Nota sobre catálogo (GET)**: esse terminal define o contrato entre o broker e a plataforma {{site.data.keyword.Bluemix_notm}} para os serviços e planos suportados pelo broker. Esse terminal retorna os metadados do catálogo armazenados em seu broker. Esses valores definem o contrato de fornecimento mínimo entre seu serviço e a plataforma {{site.data.keyword.Bluemix_notm}}. Todos os metadados do catálogo adicionais que não são necessários para fornecimento são armazenados no catálogo do {{site.data.keyword.Bluemix_notm}}. Quaisquer atualizações nos valores de exibição do catálogo que são usados para renderizar seus painéis, como links, ícones e metadados convertidos do i18n, devem ser atualizadas no console de gerenciamento de recursos e não hospedadas no broker. Nenhum dos metadados armazenados em seu broker é exibido no console do {{site.data.keyword.Bluemix_notm}} ou na CLI do {{site.data.keyword.Bluemix_notm}}. O console e a CLI retornam o que foi configurado dentro do console de gerenciamento de recursos e armazenado no catálogo do {{site.data.keyword.Bluemix_notm}}. A seção a seguir mostra os valores mínimos necessários que o catálogo (GET)
retornará:

```
{
       "services": [{
           "id": "ibmcloud-link",
           "name": "ibmcloud-link",
           "description": "An IBM provided service that enables aliasing to service instances in the {{site.data.keyword.Bluemix_notm}}.",
           "bindable": true,
           "plan_updateable": false,
           "plans": [
               {
                   "id": "ibmcloud-link-alias",
                   "name": "ibmcloud-alias",
                   "free": true,
                   "description": "The {{site.data.keyword.Bluemix_notm}} alias plan used for linking."
               }
               ]
       }]
}
```

### Lógica de terminais necessários para serviços ligáveis

Se seu serviço puder ser ligado a aplicativos no {{site.data.keyword.Bluemix_notm}}, ele deverá retornar terminais e credenciais de API para seus consumidores de serviço. Um serviço bindable deve usar as operações ligáveis na especificação do Open Service Broker e implementar os terminais/caminhos a seguir:

<dl>
  <dt>ligações e credenciais (PUT)</dt>
  <dd>Liga sua instância de serviço a um aplicativo.</dd>
  <dt>ligações e credenciais (DEL)</dt>
  <dd>Desvincula sua instância de serviço de um aplicativo.</dd>
</dl>

### Terminais de extensão  {{site.data.keyword.Bluemix_notm}}  necessários

A especificação do OSB não* suporta um estado de instância desativado, mas ainda não excluiu o estado da instância. Para que o {{site.data.keyword.Bluemix_notm}} suporte clientes que possam sofrer um lapso de faturamento ou outras situações que resultem em uma suspensão de conta (mas ainda não um cancelamento), o {{site.data.keyword.Bluemix_notm}} definiu os terminais de API estendidos que permitem que instâncias de serviço sejam desativadas e reativadas. As extensões de terminal a seguir são **necessárias**:

<dl>
  <dt>ativar e desativar instâncias (GET)</dt>
  <dd>Status - retorna o estado de sua instância de serviço.</dd>
  <dt>ativar e desativar instâncias (PUT)</dt>
  <dd>Permite ativar ou desativar uma instância de serviço.</dd>
</dl>

É responsabilidade do provedor de serviços desativar o acesso à instância de serviço quando o terminal de desativação se inicia e reativar esse acesso quando o terminal de ativação é iniciado.
{: note}

## Aprenda como usar os metadados exportados para guiar seu desenvolvimento do broker
{: #use-metadata}

Os metadados que você exportou do console de gerenciamento de recurso podem ser usados como um guia para desenvolver seu próprio broker. Nem todos os valores inseridos no console de gerenciamento de recurso são necessários para provisionar um serviço. Os metadados exportados do console de gerenciamento de recurso definem o contrato de fornecimento mínimo entre seu serviço e a plataforma {{site.data.keyword.Bluemix_notm}}. Seu JSON exportado fornece os valores a seguir:

```
{
services :
            [
                {
                    bindable         : true,
                    description      : "Test Node Resource Service Broker Description",
                    // TODO - GUID generated by http://www.guidgenerator.com
                    // TODO - This service id must be unique within an IBM Cloud environment's set of service offerings
                    id               : "df35cab6-347b-4ba5-8f39-e9c23a237f5b",
                    metadata         :
                    {
                        displayName         : "Test Node Resource Service Broker Display Name",
                        documentationUrl    : baseMetadataUrl + "documentation.html",
                        imageUrl            : baseMetadataUrl + "services.svg", // Copied from https://github.com/carbon-design-system/carbon-icons/blob/master/src/svg/services.svg
                        instructionsUrl     : baseMetadataUrl + "instructions.html",
                        longDescription     : "Test Node Resource Service Broker Long Description",
                        providerDisplayName : "Company Name",
                        supportUrl          : baseMetadataUrl + "support.html",
                        termsUrl            : baseMetadataUrl + "terms.html"
                    },
                    name             : SERVICE_NAME,
                    // TODO - Ensure this value is accurate for your service. Requires PATCH of /v2/service_instances/:instance_id below if true
                    plan_updateable  : true,
                    tags             : ["lite", "tag1a", "tag1b"],
                    plans            :
                    [
                        {
                            bindable    : true,
                            description : "Test Node Resource Service Broker Plan Description",
                            free        : true,
                            // TODO - GUID generated by http://www.guidgenerator.com
                            // TODO - This service plan id must be unique within an IBM Cloud environment's set of service plans
                            id          : "2a1d139b-1b05-4e33-b72e-a1f8c14be559",
                            metadata    :
                            {
                                bullets     : ["Test bullet 1", "Test bullet 2"],
                                displayName : "Lite"
                            },
                            // TODO - This service plan name must be unique within the containing service definition
                            name        : "lite"
                        }
                    ]
                }
            ]
}
```


Sua matriz de serviços OSB deve ser a mesma que os metadados da oferta que você incluiu no console de gerenciamento de recursos. Para assegurar uma paridade de um para um entre o OSB e o console de gerenciamento de recursos, é crítico que você compare a matriz de serviços em `catalog.json` que você transferiu por download do console de gerenciamento de recursos com a matriz de serviços real em seu broker. Todos os IDs e nomes de serviço e plano devem corresponder.
{: tip}

## Informações do broker fornecidas pela plataforma  {{site.data.keyword.Bluemix_notm}}
{: #broker info}

Seu broker ou brokers de serviço recebem as informações a seguir da plataforma {{site.data.keyword.Bluemix_notm}}:

### X-Broker-API-Originating-Identity

O **cabeçalho de identidade do usuário** é fornecido por meio de um cabeçalho de identidade de origem de API. Esse cabeçalho de solicitação inclui a Identidade do IAM do {{site.data.keyword.Bluemix_notm}} do usuário. A Identidade do IAM é codificada em base64. O {{site.data.keyword.Bluemix_notm}}  suporta uma região de autenticação única:  ` IBMid `. A região `IBMid` usa um IBMid Unique ID (IUI) para identificar a identidade do usuário no {{site.data.keyword.Bluemix_notm}}. Esse IUI é uma sequência opaca para o provedor de serviços.

Exemplo:

```
X-Broker-API-Originating-Identity: ibmcloud eyJpYW1faWQiOiJJQk1pZC01MEdOUjcxN1lFIn0=
Decoded:
{"iam_id":"IBMid-50GNR717YE"}
```

### Versão de cabeçalho da API

O **cabeçalho da versão da API** é
[2.12](https://github.com/openservicebrokerapi/servicebroker/blob/v2.12/spec.md){: new_window}
![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo"). Por exemplo: ` X-Broker-Api-Version: 2.12`.

### Instância de recurso (PUT) body.context e instância de recurso (PATCH) body.context

`PUT /v2/service_instances/:resource_instance_id` e `PATCH /v2/service_instances/:resource_instance_id` recebem o valor a seguir em **body.context**: `{ "platform": "ibmcloud", "account_id": "tracys-account-id", "crn": "resource-instance-crn" }`.

## Recomendações adicionais do broker
{: #more-info}

### Recomendações sobre o uso assíncrono em vez de operações síncronas

O OSB API suporta os modos síncrono e assíncrono de operação. Se suas operações forem levar menos de 10 segundos, as respostas síncronas serão recomendadas. Caso contrário, deve-se usar o modo assíncrono da operação. Mais informações estão contidas na especificação do OSB.

Se a sua operação assíncrona levar menos de 10 segundos quando você estiver provisionando uma instância, a plataforma atingirá o tempo limite.
{: tip}

### Recomendações para gerenciar brokers em locais

É importante que os usuários entendam o local de seus serviços de nuvem para latência, disponibilidade e residência de dados.

Quando você está provisionando instâncias de serviço no {{site.data.keyword.Bluemix_notm}}, um dos parâmetros necessários que seus usuários fornecem é o local em que eles desejam que a instância de serviço seja provisionada. Alguns serviços podem suportar o fornecimento em vários locais. Por exemplo, um serviço de banco de dados pode suportar ser provisionado em todas as regiões do {{site.data.keyword.Bluemix_notm}} ou pode suportar um subconjunto.

Se seu serviço baseado em API de terceiros for implementado em outra nuvem e exposto no {{site.data.keyword.Bluemix_notm}}, o local indicará o local do serviço na outra nuvem.

Quando você se integra ao {{site.data.keyword.Bluemix_notm}}, deve implementar pelo menos um broker do OSB. É possível ter mais de um broker, dependendo de sua estratégia de implementação e dos locais que deseja suportar para seu serviço. Na ferramenta do console de gerenciamento de recursos, você estabeleceu o mapeamento entre a tupla de serviço/plano/local e o broker que atende as operações para
essa tupla. As opções típicas seriam definir um único broker para atender a todos os locais para seu serviço ou definir um broker por local; essa opção cabe ao provedor de serviços.

Para obter uma lista de locais disponíveis, consulte os [Locais do catálogo global da IBM](https://resource-catalog.bluemix.net/search?q=kind:geography){: new_window} ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo"). Se seu serviço precisar que locais adicionais sejam definidos no Catálogo Global, consulte a equipe de migração do {{site.data.keyword.Bluemix_notm}}.


## Hospeda seus brokers
{: #host}

Seu broker deve ser hospedado como parte de um aplicativo que pode responder às chamadas API de REST. E seu local hospedado deve atender às diretrizes de segurança do {{site.data.keyword.Bluemix_notm}}. Você pode ser hospedado no {{site.data.keyword.Bluemix_notm}} ou pode ser hospedado externamente, se ele estiver publicamente acessível por meio do próprio {{site.data.keyword.Bluemix_notm}}.

Para hospedar seu broker fora da IBM, deve-se assegurar de que ele atenda às diretrizes de segurança a seguir:
- Deve seguir o protocolo de Segurança da Camada de Transporte (TLS) versão 1.2
- Deve ser hospedado em um terminal HTTPs válido que esteja acessível na Internet pública

Se desejar hospedar no {{site.data.keyword.Bluemix_notm}}, será possível localizar informações sobre a criação de um app usando Contêineres (Kubernetes) aqui: [Adotantes internos - Informações de uso](/docs/containers/cs_internal.html#cs_internal).

Será necessário o local hospedado de seu broker de serviço para concluir a próxima etapa. Tenha a URL e as credenciais que estão associadas ao seu aplicativo prontas quando for para a próxima etapa.
{: tip}

## Como testar o broker do seu serviço
{: #test}

Deve-se validar seu broker executando comandos curl nos diferentes terminais que você está ativando. O arquivo leia-me de amostra fornece uma excelente orientação para curling de seus terminais do OSB: [https://github.com/IBM/sample-resource-service-brokers/blob/master/README.md](https://github.com/IBM/sample-resource-service-brokers/blob/master/README.md){: new_window} ![Ícone do link externo](../icons/launch-glyph.svg "Ícone do link externo")

### Como curl o broker do seu serviço
{: #curl-broker}
Use o exemplo a seguir para testar sua resposta de curl dos brokers:

```
curl -X PUT  https://<sample-service-broker>/v2/service_instances/<encoded-resource-crn> \
     -u '<your broker user>:<your broker password>' \
     -H 'content-type: application/json' \
      -d '{ "context": {"platform": "ibmcloud", \
                        "account_id": "34ff5928-c3c7-4d46-bbf6-1a5628c325d1", \
                        "resource_group_crn": "crn:v1:bluemix:public:resource-controller::a/003e9bc3993aec710d30a5a719e57a80::resource-group:b4570a825f7f4d57aa54e8e1d9507926", \
                        "crn": "<resource-crn>", \
                        "target_crn": "<target_crn>"}, \
            "service_id": "a07f025c-90db-4652-afd1-cf4adfac93c8", \
            "plan_id": "fe442cec-2eef-41fe-9f92-58d6c094584f"}'
```

## Próximas Etapas
{: #next-steps}

Você tem algumas habilidades sérias! Você construiu e hospedou um broker de serviço que atende à especificação OSB. Consulte [Etapa 4: Desenvolvendo um fluxo de autenticação](/docs/third-party/cis5-iam.html).
