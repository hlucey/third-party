---

copyright:

  years: 2015, 2019

lastupdated: "2019-02-25"

keywords: IBM Cloud, different metering options, new IBM Cloud Identity, faqs 

subcollection: third-party

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:tip: .tip}
{:new_window: target="_blank"}
{:faq: data-hd-content-type="faq"}
{:note: .note}

# FAQ
{: #3p-faqs}

## Quais são as diferentes opções de medição para planos?
{: #metering}
{: faq}

O {{site.data.keyword.Bluemix}} suporta múltiplos modelos para agregar o uso de oferta. Os provedores de ofertas medem várias métricas sobre as instâncias provisionadas e enviam essas medidas para o serviço de medição. O serviço de classificação agrega o uso enviado em diferentes depósitos (instância, grupo de recursos e conta) com base no modelo que os provedores de oferta escolhem. Os modelos de agregação e classificação para todas as métricas em um plano estão contidos nos documentos de definição de medição e classificação para o plano.

É necessário automatizar o envio de uso por hora usando a API de serviço de medição, se você oferecer um plano medidor.
{: note}

Para obter mais informações sobre medição, veja [Integração de medição](/docs/third-party?topic=third-party-meteringintera#meteringintera). Para obter mais informações sobre o envio de uso medido, consulte
[Enviando o uso para planos medidos](/docs/third-party?topic=third-party-submitusage#submitusage).

## Como posso gerar uma nova chave API do {{site.data.keyword.Bluemix_notm}} Identity and Access Management?
{: #iam-creds}
{: faq}

Você terá a chave API quando ativar o IAM. É crítico que você salve a Chave API. O valor não é mostrado novamente. Se você perder a sua Chave API, será possível excluir a chave e criar uma nova. Para obter mais informações, consulte [Gerenciar chaves API do ID de
serviço](/docs/iam?topic=iam-serviceidapikeys#serviceidapikeys). 


