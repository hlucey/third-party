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
{:important: .important}
{:download: .download}

# Como os serviços de faturamento integrado usam a plataforma {{site.data.keyword.Bluemix_notm}}
{: #how-it-works}

Os serviços de faturamento integrado são diferentes dos serviços de indicação. Um serviço de faturamento integrado usa a plataforma {{site.data.keyword.Bluemix_notm}} para autenticação, acesso, fornecimento, medição e faturamento. Esse tópico fornece uma visão geral resumida dos componentes de plataforma usados pelo serviço de faturamento integrado.

## A camada de fornecimento do  {{site.data.keyword.Bluemix_notm}}
{: #provisioning-layer}

A camada de fornecimento gerencia o ciclo de vida de recursos do {{site.data.keyword.Bluemix_notm}}. A camada de fornecimento é responsável por controlar e rastrear o ciclo de vida de recursos em uma conta do cliente. *Recursos* são componentes físicos ou lógicos que podem ser provisionados ou reservados para um aplicativo ou instância de serviço. Os exemplos de recursos incluem os bancos de dados, as contas, o processador, a memória e os limites de armazenamento. Em geral, os
recursos controlados pela camada de fornecimento destinam-se a associar as métricas de uso e o faturamento, mas esse nem sempre é o
caso. Em alguns casos, o recurso pode ser associado à camada de fornecimento para assegurar que o ciclo de vida de recurso possa ser gerenciado junto com o ciclo de vida da conta.

### Gerenciamento de ciclo de vida de recurso
{: #lifecycle}

A camada de fornecimento fornece APIs comuns para controlar o ciclo de vida de recursos do fornecimento (criando uma instância) à vinculação (criando credenciais de acesso) à desvinculação (removendo o acesso) à remoção de provisão (excluindo uma instância). Além disso, a plataforma {{site.data.keyword.Bluemix_notm}} fornece CLIs e uma IU que pode gerenciar o ciclo de vida desses recursos que não requerem a criação de seus próprios recursos.

A camada de fornecimento fornece APIs para ajudá-lo a gerenciar os elementos a seguir de seu ciclo de vida de recurso:
* Fornecimento
* Atualizando uma instância de recurso
* Ligação
* Chaves de recursos
* Desvinculando
* Desprovimento

## {{site.data.keyword.Bluemix_notm}}  Identity and Access Management (IAM)
{: #iam}

O Identity Access Management (IAM) permite que você autentique os usuários com segurança e controle o acesso a todos os recursos em nuvem de forma consistente no {{site.data.keyword.Bluemix_notm}}. A camada de fornecimento do {{site.data.keyword.Bluemix_notm}} adotada pelo IAM para a autenticação e a autorização de ações
que são tomadas com relação à camada de fornecimento. Os provedores de ofertas de terceiros usam o IAM para criar um fluxo de autenticação (OAuth). Para obter mais informações, consulte [O que é IAM](/docs/iam/index.html#iamoverview)?

Se sua oferta usa bibliotecas do OpenID Connect (OIDC), o IAM suporta a integração OIDC. OIDC é uma camada de autenticação em cima do OAuth 2.0, uma estrutura de autorização e pode ajudar a simplificar o processo de integração. Para obter mais informações sobre OIDC, veja [Open ID Connect](http://openid.net/connect/){: new_window} ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo").

## Catálogo do {{site.data.keyword.Bluemix_notm}}
{: #catalog}

O catálogo do {{site.data.keyword.Bluemix_notm}} armazena as definições de oferta (descrição, recursos, imagens, URLs e assim por diante) dos recursos que são exibidos no console do {{site.data.keyword.Bluemix_notm}}. O console de gerenciamento de recurso é usado para definir todos os aspectos dos metadados necessários de seu serviço. Esses metadados são publicados no catálogo e usados para exibição no catálogo. É possível localizar informações detalhadas sobre os campos de metadados obrigatórios e opcionais nas páginas **Oferta** e **Plano** no console de gerenciamento de recurso. Os itens chave são incluídos aqui para acelerar o entendimento.

   * Nome do serviço: nome técnico para seu serviço. O nome do serviço é crítico e deve ser definido corretamente. Deve-se fornecer um nome de serviço que seja usado para identificar o serviço pela plataforma {{site.data.keyword.Bluemix_notm}} e um nome de exibição que seus clientes veem no catálogo do {{site.data.keyword.Bluemix_notm}}. O nome do serviço não é o nome de exibição.
   * Nome de exibição de serviço: nome fácil e simples para o serviço. Por exemplo, "Compose Redis"
   * ID do serviço: GUID para o serviço que é usado em chamadas API para o broker OSB. Esse valor deve ser exclusivo.
   * Ícone de serviço: SVG com seu logotipo de serviço
   * Descrição do serviço: a descrição do recurso que é exibido quando você passa o mouse sobre o ícone de recurso na interface com o usuário do catálogo do {{site.data.keyword.Bluemix_notm}}. É possível incluir uma única sentença ou frase para a descrição.
   * Descrição detalhada do serviço: o primeiro parágrafo que aparece na página de listagem do catálogo. Considere pelo menos duas sentenças para obter uma descrição detalhada.
   * URL da documentação: um link para sua documentação do {{site.data.keyword.Bluemix_notm}}. Você criará no PWB e o
valor da URL será gerado pelo PWB para você.
   * URL de termos: um link para os termos e condições de seu serviço para uso. Para propósitos de GDPR, não vincule aos termos e condições de seu serviço de terceiro existente. Em vez disso, deve-se fornecer uma página exclusiva para um serviço de faturamento integrado.
   * URL de instruções: similar à URL de documentação, você apontará para a sua documentação do
{{site.data.keyword.Bluemix_notm}}; no entanto, a URL de instruções puxará dinamicamente a documentação para uma guia
Introdução no painel do serviço.
   * Categoria: seleção das categorias do {{site.data.keyword.Bluemix_notm}} disponíveis em que o serviço é colocado no catálogo.
   * Marcadores: lampejos descritivos curtos sobre seu serviço
   * Mídia: capturas de tela e vídeos sobre seu serviço
   * Nome do plano de serviço: cada plano tem um nome técnico. Todo em minúsculas, sem espaços, pode incluir "-". Por exemplo,  ` gold `.
   * Nome de exibição do plano de serviço: nome fácil e simples para o plano. Por exemplo,  ` Gold `
   * ID do plano de serviço: GUID para o plano de serviço usado em chamadas API para o broker OSB. Esse valor deve ser exclusivo. O console de gerenciamento de recurso gera esse valor para você.
   * Descrição do plano de serviço: a descrição do plano de recursos. A descrição é exibida depois que você seleciona um plano na página de detalhes do recurso no catálogo do IBM Cloud
   * Marcadores do plano de serviço: lampejos descritivos curtos sobre o plano de serviço


## Open Service Broker
{: #open-service}

Os Brokers de serviço gerenciam o ciclo de vida de serviços. A plataforma {{site.data.keyword.Bluemix_notm}} interage
com os brokers de serviço para fornecer e gerenciar as instâncias de serviços (uma instanciação de uma oferta de serviços) e
as ligações de serviços (a representação de uma associação entre um aplicativo e uma instância de serviços, que geralmente incluem
as credenciais que o aplicativo usa para se comunicar com a instância de serviços). O fornecimento de valores de metadados
válidos cria uma resposta da API de REST bem-sucedida quando uma solicitação é executada.

O {{site.data.keyword.Bluemix_notm}} usa a especificação do Open Service Broker API (OSB) `versão 2.12`. Leia e familiarize-se com a [Especificação do Open Broker API](https://github.com/openservicebrokerapi/servicebroker/blob/v2.12/spec.md){: new_window} ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo") e use o arquivo leia-me como um guia para saber mais.

Quando o controlador de recurso recebe uma solicitação para provisionar um recurso, ele chama o seu OSB para validar o tipo de serviço, a oferta, os planos e a disponibilidade de regiões. O controlador de recurso também valida a visibilidade do plano associado à conta do cliente. O {{site.data.keyword.Bluemix_notm}} fornece amostras do broker e docs de API que ampliam a especificação de OSB. É possível localizar mais detalhes sobre como desenvolver e hospedar seu broker à medida que você percorre as etapas detalhadas de desenvolvimento integrado do faturamento integrado.

## {{site.data.keyword.Bluemix_notm}} Serviço de medição
{: #metering-service}

Se um serviço oferece um plano medido, os usuários do {{site.data.keyword.Bluemix_notm}} são cobrados com base na quantia de recursos que eles usam. Por exemplo, os usuários do {{site.data.keyword.Bluemix_notm}} que usam serviços de banco de dados podem ser cobrados com base na quantia de armazenamento que seus aplicativos usam. O envio de uso deve ocorrer para que o uso seja convertido em um registro debitável.

Todos os serviços de faturamento integrado que oferecem um plano medido devem usar o serviço de medição do {{site.data.keyword.Bluemix_notm}} para relatar dados de uso.

Será necessário automatizar o envio de uso por hora usando a API de serviço de medição, se você oferecer um plano medidor.
{: important}

Para obter mais informações sobre a medição, consulte: [Integração da medição](/docs/third-party/metering.html#meteringintera). Para obter mais informações sobre como enviar o uso medido, consulte: [Enviando o uso para os planos medidos](/docs/third-party/submitusage.html#submitusage)

## Cenário de Provisão: Puxando tudo junto

Agora, vamos reunir todos os conceitos e ver um exemplo de como a criação da instância de serviço funciona usando a plataforma {{site.data.keyword.Bluemix_notm}}.

![Cenário de fornecimento](images/flow-am.svg "Como a plataforma manipula a criação de instância de serviço")

Quando um usuário deseja criar uma instância de serviço, ele pode criá-lo de uma de duas maneiras:
* **CLI**: usando `ibmcloud cli [ ibmcloud resource service-instance-create NAME SERVICE_NAME SERVICE_PLAN_NAME LOCATION ]`
* **Console do {{site.data.keyword.Bluemix_notm}}**: o usuário pode selecionar o serviço, planejar e usar a operação **Criar**.

A plataforma {{site.data.keyword.Bluemix_notm}} valida se o usuário tem permissão para criar a instância de serviço
usando o {{site.data.keyword.Bluemix_notm}} IAM. Depois que essa validação ocorrer, o terminal de provisão do broker de
serviço (PUT /v2/resource_instances/:resource_instance_id) será iniciado. Quando o fornecimento ocorre, as regras a seguir devem ser atendidas:
* O contexto do {{site.data.keyword.Bluemix_notm}} é incluído na variável de contexto
* O `X-Broker-API-Originating-Identity` tem o ID do IBM IAM do usuário que iniciou a solicitação
* A seção de parâmetros inclui o local solicitado (e mais parâmetros que são requeridos pelo serviço).

Exemplo de solicitação de provisão:

```
    PUT /v2/service_instances/crn%3Av1%3Abluemix%3Apublic%3Acompose-redis%3Aus-south%3Aa%2F46aa677e-e83f-4d17-a2b6-5b752564477c%3A416d769b-682d-4833-8bd7-5ef8778e5b52?accepts_incomplete=true HTTP/1.1
    Host:  https://broker.compose.cloud.ibm.com
    Authorization: basic dXNlcjpwYXNzd29yZA==
    X-Broker-Api-Version: 2.12
    X-Broker-API-Originating-Identity: ibmcloud aWJtaWQtNDU2MzQ1WA==
    {
      "service_id": "0bc9d744-6f8c-4821-9648-2278bf6925bb", // your service's GUID from onboarding
      "plan_id": "ecc19311-aba2-49f7-8198-1e450c8460d4", //your plan's GUID from onboarding
      "context": {
        "platform": "ibmcloud",
        "account_id": "003e9bc3993aec710d30a5a719e57a80",
        "crn": "crn:v1:bluemix:public:compose-redis:us-south:a/003e9bc3993aec710d30a5a719e57a80:416d769b-682d-4833-8bd7-5ef8778e5b52",
        "resource_group_crn": "crn:v1:bluemix:public:resource-controller::a/003e9bc3993aec710d30a5a719e57a80::resource-group:b4570a825f7f4d57aa54e8e1d9507926",
        "target_crn": "crn:v1:bluemix:public:resource-catalog::a/e97a8c01ac694e308ef3ad7795c7cdb3::deployment:e62e2c19-0c3b-41e3-b8b3-c71762ecd489:us-south38399"
      },
      "parameters": {
        "location": "us-south",
        "optional-param":"parameter required by your service"
      }
    }
```

### Entendendo o parâmetro  {{site.data.keyword.Bluemix_notm}}  ` context `
{: #parameter}

No exemplo anterior, é possível ver os metadados retornados no parâmetro `context`. O contexto de provisão para o {{site.data.keyword.Bluemix_notm}} retorna o seguinte:

* ** platform **: Identifica a plataforma como "ibmcloud"

* **"account_id"**: retorna o ID da conta no {{site.data.keyword.Bluemix_notm}} que está provisionando a instância de serviço.

* **crn**: quando um cliente provisiona seu serviço no {{site.data.keyword.Bluemix_notm}}, uma instância de serviço é criada e essa instância é identificada por seu Nome do Recurso (CRN) do {{site.data.keyword.Bluemix_notm}}. O CRN é usado em todos os aspectos da interação com o {{site.data.keyword.Bluemix_notm}} incluindo o
fornecimento, a ligação (criando as credenciais e os terminais), a medição, a exibição de painel e o controle de acesso. De uma perspectiva do provedor de oferta, o CRN pode ser tratado em grande parte como uma sequência opaca a ser usada com as APIs do {{site.data.keyword.Bluemix_notm}}. Ele também pode ser decomposto usando a estrutura a seguir:

   ```
   crn:version:cname:ctype:service-name:location:scope:service-instance:resource-type:resource
   ```

   Na amostra de fornecimento, vemos que o CRN do serviço `compose-redis` é:

   ```
   crn:v1 :bluemix:public:compose-redis:us-south:a/46aa677e-e83f-4d17-a2b6-5b752564477c: 416d769b-682d-4833-8bd7-5ef8778e5e5b52:::
   ```

   Nessa amostra, essa instância de `compose-redis` faz parte da conta do {{site.data.keyword.Bluemix_notm}} com o ID. O ID exclusivo para a instância é `416d769b-682d-4833-8bd7-5ef8778e5b52` e a instância está hospedada na região `us-south` do {{site.data.keyword.Bluemix_notm}} público.

* **resource_group_crn**: retorna o grupo de recursos que inclui a instância de serviço. Para obter mais detalhes, veja [Gerenciando grupos de recursos](/docs/resources/resourcegroups.html).

   Os provedores de ofertas não estão preocupados com o `resource_group_crn`, exceto em circunstâncias exclusivas. Consulte seu representante IBM sobre seu caso de uso antes de usar esse campo.
   {: note}

