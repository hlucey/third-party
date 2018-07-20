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

# Domande frequenti
{: #3p-faqs}

Consulta le seguenti Domande frequenti (FAQ) per chiarimenti sulle domande più comuni.

## Quali sono le diverse opzioni di misurazione per i piani?
{: #metering}

{{site.data.keyword.Bluemix}} supporta più modelli per aggregare l'utilizzo delle offerte. I provider dell'offerta misurano varie metriche sulle istanze fornite e le inviano al servizio di misurazione. Il servizio di classificazione aggrega l'utilizzo inviato in bucket differenti (istanza, gruppo di risorse e account) in base al modello che i provider dell'offerta scelgono. I modelli di aggregazione e di classificazione di tutte le metriche in un piano sono contenuti nei documenti di definizione di misurazione e classificazione per il piano.

**Nota:** ti viene richiesto di automatizzare l'inoltro dell'utilizzo orario utilizzando l'API del servizio di misurazione se offri un piano a consumo.

Per ulteriori informazioni sulla misurazione, vedi: [Integrazione della misurazione](/docs/third-party/metering.html#meteringintera).

Per ulteriori informazioni sull'inoltro dell'utilizzo a consumo, vedi: [Inoltro dell'utilizzo per i piani a consumo](/docs/third-party/submitusage.html#submitusage)

## Ho smarrito la mia chiave API {{site.data.keyword.Bluemix_notm}} Identity and Access Management. Come posso generarne un'altra?
{: #iam-creds}

Ti viene fornita la chiave API quando **Abiliti IAM**. È molto importante che salvi la chiave API. Il valore non viene mostrato nuovamente. Se smarrisci la tua chiave API, puoi eliminarla e crearne una nuova: [Gestione delle chiavi API dell'ID servizio](/docs/iam/serviceid_keys.html#serviceidapikeys)


