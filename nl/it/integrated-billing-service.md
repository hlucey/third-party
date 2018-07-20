---


copyright:
  years: 2018
lastupdated: "2018-06-28"


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

Questo argomento è progettato per guidarti attraverso i passi necessari a sviluppare e pubblicare il tuo servizio di fatturazione integrato di terze parti in {{site.data.keyword.Bluemix_notm}}. Dopo che hai ricevuto l'approvazione a distribuire la tua offerta nel catalogo di {{site.data.keyword.Bluemix_notm}}, inizierai a sviluppare la tua offerta nella console di gestione delle risorse (console di gestione delle risorse), un'esperienza IU guidata. All'interno della console di gestione delle risorse, progetti i metadati del catalogo, configuri i piani dei prezzi del servizio e esegui l'integrazione con IBM Cloud Access Management (IAM). Successivamente, al di fuori della console di gestione delle risorse, eseguirai lo sviluppo del codice per creare e ospitare un nuovo Open Service Broker (saranno forniti documenti API ed esempi del broker iniziale) e utilizzerai IAM per sviluppare un flusso di autenticazione. Dopo aver completato questa procedura, ritornerai alla console di gestione delle risorse per distribuire il tuo servizio nel catalogo in una modalità di visibilità limitata che ti consente di verificare e convalidare più requisiti distribuibili. Quando sei pronto e la tua offerta rispetta tutti i requisiti, il tuo servizio diventerà completamente visibile nel catalogo di {{site.data.keyword.Bluemix_notm}}!


## Cosa devo fare per distribuire un servizio di fatturazione integrato?

Dovrai utilizzare PWB, la console di gestione delle risorse e l'ambiente di sviluppo di tua scelta per distribuire questi obiettivi. Consulta l'[elenco di controllo](/docs/third-party/checklist.html#checklist) per tracciare questa procedura.

La seguente procedura riepiloga il processo di onboarding a un livello elevato:

Questa procedura presuppone che hai ricevuto l'approvazione a distribuire un servizio di fatturazione integrato. Se non hai completato la registrazione iniziale e l'approvazione in PWB, consulta: [Pubblicazione iniziale della tua offerta di terze parti in {{site.data.keyword.Bluemix_notm}}](/docs/third-party/index.md)
{: tip}

1. [Crea: Crea i documenti e il comunicato di marketing del servizio (PWB)](/docs/third-party/cis1-docs-marketing.html)
2. [Definisci: Definisci la tua offerta nella console di gestione delle risorse {{site.data.keyword.Bluemix_notm}}](/docs/third-party/cis2-rmc-define.html)
3. [Sviluppa: Sviluppa e ospita uno o più broker di servizi utilizzando la specifica API Open Service Broker](/docs/third-party/cis3-broker.html)
4. [IAM: Sviluppa un flusso di autenticazione (OAuth), convalida l'autorizzazione utente (v2/authz) e ricava il tuo URI di reindirizzamento](/docs/third-party/cis5-iam.html)
5. [Pubblica e verifica: Collega il tuo OSB alla console di gestione delle risorse, pubblica il tuo servizio nella modalità di visibilità limitata nel catalogo di {{site.data.keyword.Bluemix_notm}} e verifica la tua offerta](/docs/third-party/cis4-rmc-publish.html).
6. [Richiedi l'approvazione per la conversione alla GA del tuo servizio](/docs/third-party/cis6-ga.html)

## Supporto

I servizi di fatturazione integrati richiedono che i provider del servizio di terze parti forniscano il proprio modello di supporto.  Il tuo rappresentante di IBM ti aiuterà ad abilitare il tuo modello di supporto e a garantire che se un utente apre un ticket con il supporto di {{site.data.keyword.Bluemix_notm}}, il supporto di {{site.data.keyword.Bluemix_notm}} lo instraderà al sito di supporto di terze parti.

## Aggiornamenti continui

Dopo che il tuo servizio è stato rilasciato, puoi continuare a ripetere ed apportare gli aggiornamenti collaborando direttamente con il tuo rappresentante di {{site.data.keyword.Bluemix_notm}}.



