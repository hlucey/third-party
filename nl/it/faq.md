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
{:faq: data-hd-content-type="faq"}
{:note: .note}

# FAQ
{: #3p-faqs}

## Quali sono le diverse opzioni di misurazione per i piani?
{: #metering}
{: #faq}

{{site.data.keyword.Bluemix}} supporta più modelli per aggregare l'utilizzo delle offerte. I provider dell'offerta misurano varie metriche sulle istanze fornite e le inviano al servizio di misurazione. Il servizio di classificazione aggrega l'utilizzo inviato in bucket differenti (istanza, gruppo di risorse e account) in base al modello che i provider dell'offerta scelgono. I modelli di aggregazione e di classificazione di tutte le metriche in un piano sono contenuti nei documenti di definizione di misurazione e classificazione per il piano.

Devi automatizzare l'inoltro dell'utilizzo orario utilizzando l'API di servizio di misurazione, se offri un piano a consumo.
{: note}

Per ulteriori informazioni sulla misurazione, vedi [Integrazione della misurazione](/docs/third-party/metering.html#meteringintera). Per ulteriori informazioni sull'inoltro dell'utilizzo a consumo, vedi [Inoltro dell'utilizzo per i piani a consumo](/docs/third-party/submitusage.html#submitusage).

## Come posso generare una nuova chiave API {{site.data.keyword.Bluemix_notm}} Identity and Access Management?
{: #iam-creds}
{: #faq}

Ti viene fornita la chiave API quando abiliti IAM. È molto importante che salvi la chiave API. Il valore non viene mostrato nuovamente. Se perdi la tua chiave API, puoi eliminarla e crearne una nuova. Per ulteriori informazioni, vedi [Gestione delle chiavi API di un ID servizio](/docs/iam/serviceid_keys.html#serviceidapikeys). 


