---

copyright:
  years: 2015, 2018
lastupdated: "2018-03-15"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:tip: .tip}
{:new_window: target="_blank"}

# FAQ
{: #3p-faqs}

Veja as Perguntas mais frequentes a seguir para esclarecimento sobre perguntas normalmente feitas.

## Quais são as diferentes opções de medição para planos?
{: #metering}

O {{site.data.keyword.Bluemix}} suporta múltiplos modelos para agregar o uso de oferta. Os provedores de ofertas medem várias métricas sobre as instâncias provisionadas e enviam essas medidas para o serviço de medição. O serviço de classificação agrega o uso enviado em diferentes depósitos (instância, grupo de recursos e conta) com base no modelo que os provedores de oferta escolhem. Os modelos de agregação e classificação para todas as métricas em um plano estão contidos nos documentos de definição de medição e classificação para o plano.

**Nota:** será necessário automatizar o envio de uso por hora usando a API de serviço de medição se você oferecer um plano medido.

Para obter mais informações sobre a medição, veja: [Integração de medição](/docs/third-party/metering.html#meteringintera).

Para obter mais informações sobre o envio de uso medido, veja: [Enviando uso para planos medidos](/docs/third-party/submitusage.html#submitusage)

## Eu perdi minha chave API do {{site.data.keyword.Bluemix_notm}} Identity and Access Management. Como posso gerar outro?
{: #iam-creds}

Você recebe sua Chave API ao **Ativar o IAM**. É crítico que você salve a Chave API. O valor não é mostrado novamente. Se você perder a sua Chave API, será possível excluir a chave e criar uma nova: [Gerenciar chaves API do ID do serviço](/docs/iam/serviceid_keys.html#serviceidapikeys)


