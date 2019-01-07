---


copyright:
  years: 2018
lastupdated: "2018-11-14"


---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:download: .download}

# Panoramica: sviluppo di un servizio di fatturazione integrato
{: #overview}

Questo argomento ti presenta i passi necessari per sviluppare e pubblicare il tuo servizio di fatturazione integrato di terze parti in {{site.data.keyword.Bluemix}}. 
{:shortdesc}

Dopo che hai ricevuto l'approvazione a distribuire la tua offerta nel catalogo di {{site.data.keyword.Bluemix_notm}}, inizi a sviluppare la tua offerta nella console di gestione delle risorse, un'esperienza IU guidata. Progetti i tuoi metadati del catalogo, configuri i piani di prezzi dei servizi ed esegui l'integrazione con {{site.data.keyword.Bluemix_notm}} IAM (Identity and Access Management). 

Successivamente, al di fuori della console di gestione delle risorse, esegui lo sviluppo del codice per creare e ospitare un nuovo OSB (Open Service Broker). Sono forniti documenti API ed esempi del broker iniziali e utilizzi IAM per sviluppare un flusso di autenticazione. Dopo che hai completato questa procedura, ritorni alla console di gestione delle risorse per distribuire il tuo servizio al catalogo in una modalità di visibilità limitata dove puoi verificare e convalidare i requisiti distribuibili. Quando sei pronto, e la tua offerta soddisfa tutti i requisiti, il tuo servizio diventa completamente visibile nel catalogo di {{site.data.keyword.Bluemix_notm}}!


## Come funziona il processo
{: #process}

Per fornire un servizio di fatturazione integrato, utilizzi il workbench Provider, la console di gestione delle risorse e l'ambiente di sviluppo di tua scelta. Consulta l'[elenco di controllo](/docs/third-party/checklist.html#checklist) per tracciare questa procedura.

Questi passi presuppongono che tu abbia ricevuto l'approvazione per fornire un servizio di fatturazione integrato. Se non hai completato la registrazione e l'approvazione iniziali in PWB, vedi [Introduzione alla pubblicazione della tua offerta di terze parti in {{site.data.keyword.Bluemix_notm}}](/docs/third-party/index.md)
{: tip}

1. [Crea la tua documentazione e il tuo comunicato di marketing](/docs/third-party/cis1-docs-marketing.html).
2. [Definisci la tua offerta nella console di gestione delle risorse{{site.data.keyword.Bluemix_notm}}](/docs/third-party/cis2-rmc-define.html).
3. [Sviluppa e ospita i tuoi broker dei servizi](/docs/third-party/cis3-broker.html).
4. [Sviluppa un flusso di autenticazione](/docs/third-party/cis5-iam.html).
5. [Verifica il tuo servizio](/docs/third-party/cis4-rmc-publish.html).
6. [Rilascia pubblicamente il tuo servizio](/docs/third-party/cis6-ga.html).

## Supporto
{: #support}

I servizi di fatturazione integrati richiedono che i provider di offerte di terze parti forniscano un loro modello di supporto. Il tuo rappresentante IBM puoi aiutarti ad abilitare il tuo modello di supporto e a garantire che, se un utente apre un ticket con il supporto {{site.data.keyword.Bluemix_notm}}, tale ticket venga instradato al sito di supporto di terze parti.

## Aggiornamenti continui
{: #maintain}

Dopo che il tuo servizio è stato rilasciato, puoi continuare a ripetere ed apportare gli aggiornamenti collaborando direttamente con il tuo rappresentante di {{site.data.keyword.Bluemix_notm}}.



