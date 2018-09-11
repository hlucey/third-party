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

# FAQ
{: #3p-faqs}

## Quais são as diferentes opções de medição para planos?
{: #metering}

O {{site.data.keyword.Bluemix}} suporta múltiplos modelos para agregar o uso de oferta. Os provedores de ofertas medem várias métricas sobre as instâncias provisionadas e enviam essas medidas para o serviço de medição. O serviço de classificação agrega o uso enviado em diferentes depósitos (instância, grupo de recursos e conta) com base no modelo que os provedores de oferta escolhem. Os modelos de agregação e classificação para todas as métricas em um plano estão contidos nos documentos de definição de medição e classificação para o plano.

**Nota:** será necessário automatizar o envio de uso por hora usando a API de serviço de
medição se você oferecer um plano medido.

Para obter mais informações sobre medição, veja [Integração de medição](/docs/third-party/metering.html#meteringintera). 
Para obter mais informações sobre o envio de uso medido, consulte
[Enviando o uso para planos medidos](/docs/third-party/submitusage.html#submitusage).

## Como posso gerar uma nova chave API do {{site.data.keyword.Bluemix_notm}} Identity and Access Management?
{: #iam-creds}

Você terá a chave API quando ativar o IAM. É crítico que você salve a Chave API. O valor não é mostrado novamente. Se você perder a sua Chave API, será possível excluir a chave e criar uma nova. 
Para obter mais informações, consulte [Gerenciar chaves API do ID de
serviço](/docs/iam/serviceid_keys.html#serviceidapikeys). 


