---

copyright:

  years: 2018, 2019 

lastupdated: "2019-03-28"

keywords: billing service, resource management console, pricing plans

subcollection: third-party

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:note: .note}
{:download: .download}

# Passo 2. Definisci la tua offerta nella console di gestione delle risorse
{: #step2-define}

La console di gestione delle risorse è uno strumento che ti assiste nella fornitura della tua offerta di terze parti nel catalogo {{site.data.keyword.Bluemix_notm}}.
Ora che è stato approvato che puoi fornire un servizio di fatturazione integrato, sei pronto ad utilizzare la console di gestione delle risorse per registrare il tuo servizio, iniziare a sviluppare e definire i tuoi piani dei prezzi. La console di gestione delle risorse è uno strumento basato sul web che ti assiste nella fornitura del tuo servizio di fatturazione integrato nel catalogo {{site.data.keyword.Bluemix_notm}}.
{:shortdesc}

## Prima di iniziare
{: #rmc-pre-reqs}

1. Assicurati di aver iniziato a lavorare sul [Passo 1: Crea i documenti e il comunicato di marketing del servizio (PWB)](/docs/third-party?topic=third-party-content-tasks#content-tasks).
2. Assicurati che sei registrato presso {{site.data.keyword.Bluemix_notm}}. In caso contrario, [esegui la registrazione](https://cloud.ibm.com/registration){: new_window} ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno") prima di procedere.
3. Assicurati di essere nell'account corretto quando inizi a lavorare nella console di gestione delle risorse.
4. Prepara il tuo nome servizio {{site.data.keyword.Bluemix_notm}}. Devi fornire sia un nome servizio che viene utilizzato per identificare il servizio dalla piattaforma {{site.data.keyword.Bluemix_notm}} sia un nome di visualizzazione che i tuoi clienti vedono nel catalogo {{site.data.keyword.Bluemix_notm}}.

  Quando registri la tua offerta presso la console di gestione delle risorse, tieni pronto il tuo nome servizio {{site.data.keyword.Bluemix_notm}}. Il tuo nome servizio non è il tuo nome di visualizzazione. Il tuo nome servizio deve rispettare le seguenti regole:
   - Deve essere tutto in minuscole
   - Non può includere spazi ma può includere trattini (`-`)
   - Deve essere di meno di 32 caratteri

   Il tuo nome servizio deve includere il nome della tua azienda. Se la tua azienda ha più di una singola offerta, il tuo nome servizio deve includere sia l'azienda che l'offerta come parte del nome. Ad esempio l'azienda Compose ha offerte per Redis ed Elasticsearch. I nomi servizio di esempio su {{site.data.keyword.Bluemix_notm}} per tali offerte sarebbero `compose-redis` e `compose-elasticsearch`. Entrambi questi nomi servizio hanno dei nomi di visualizzazione associati che sono mostrati nel catalogo {{site.data.keyword.Bluemix_notm}}: *Compose Redis* e *Compose Elasticsearch*. Un'altra azienda (ad esempio, FastJetMail) può avere solo la singola offerta JetMail, nel qual caso il nome servizio deve essere `fastjetmail`.

## Registra la tua offerta
{: #register}

Per iniziare, esegui l'accesso e registra la tua offerta:

1. Accedi a [{{site.data.keyword.Bluemix_notm}}](https://cloud.ibm.com){: new_window} ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno") con il tuo ID {{site.data.keyword.Bluemix_notm}}.
   **Avvertenza**: è di importanza critica che tu sia nell'account {{site.data.keyword.Bluemix_notm}} corretto. Se hai più di un account, assicurati di passare a quello corretto.
2. Vai al [dashboard della console di gestione delle risorse](https://cloud.ibm.com/onboarding/dashboard){: new_window} ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno").
3. Fai clic su **New Resource** per aggiungere la tua risorsa.
4. Aggiungi il tuo nome risorsa (**Resource name**). Questo valore è il tuo nome servizio {{site.data.keyword.Bluemix_notm}} univoco che hai derivato nella sezione precedente.
5. Non prevediamo che tu abbia un broker dei servizi ospitato esistente; seleziona **No** per il campo **Is your broker ready for import?**. Ti assisteremo nella creazione di un broker nei passi successivi e ritornerai alla console di gestione delle risorse per importare il tuo broker dopo che è stato sviluppato e ospitato.
7. Dopo che hai eseguito l'inoltro, vieni portato alla pagina **Summary**. Completa gli eventuali valori *obbligatori* aggiuntivi e fai clic su **Save**.

Puoi salvare il tuo avanzamento nella console di gestione delle risorse e tornare successivamente per aggiungere ulteriori informazioni. La console di gestione delle risorse è progettata per aiutarti a gestire il ciclo di vita del tuo servizio. Non ci sono problemi se non disponi immediatamente di tutte le risposte per tutti i campi.
{: tip}

## Immetti i metadati della tua offerta
{: #offering-metadata}

Nella pagina **Catalog Listing**, fornisci i valori dei metadati che sono archiviati nel catalogo {{site.data.keyword.Bluemix_notm}}. Inoltre, alcuni di questi valori devono essere esportati e archiviati nel tuo broker dei servizi dove vengono utilizzati per il provisioning e restituiti come parte della risposta di `catalog (GET)`. Utilizza questi valori come ausilio per iniziare rapidamente a sviluppare un broker dei servizi nei passi successivi.

1. Dalla console di gestione delle risorse, fai clic sulla pagina **Catalog Listing** e fai clic sulla scheda **Listing Page**. **Listing Page** definisce i metadati visualizzati nel dashboard dei servizi della tua offerta {{site.data.keyword.Bluemix_notm}}. Completa tutti i valori obbligatori e fai clic su **Save**. La console di gestione delle risorse esegue una registrazione iniziale del tuo servizio presso {{site.data.keyword.Bluemix_notm}} IAM (Identity and Access Management). Viene visualizzata una notifica che il tuo servizio è stato registrato presso IAM. Puoi eseguire ulteriori operazioni con IAM successivamente.
2. Dalla pagina **Catalog Listing**, fai clic sulla scheda **Settings**.
   1. Specifica se la tua offerta consente le modifiche di piano (**Plan changes supported?**). Il valore predefinito è **No**. Se specifichi **Yes**, devi estendere il tuo Open Service Broker per supportare le modifiche di piano per le istanze di cui è stato eseguito il provisioning. Se la tua offerta supporta molti piani, e desideri che gli utenti possano modificare i piani per un'istanza di cui è stato eseguito il provisioning esistente, devi abilitare la capacità degli utenti di aggiornare la loro istanza del servizio. Per ulteriori dettagli, vedi l'endpoint `/v2/service_instances/{instance_id} PATCH` nella [API Open Service Broker v2.12](https://github.com/openservicebrokerapi/servicebroker/blob/v2.12/spec.md#updating-a-service-instance){: new_window} ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")
   2. Specifica se per il tuo servizio può essere eseguito il bind (**Bindable**). Il valore predefinito è **No**. Seleziona **Yes** se è possibile eseguire il bind del tuo servizio alle applicazioni in {{site.data.keyword.Bluemix_notm}}. Se è possibile eseguirne il bind, deve restituire le credenziali e gli endpoint API ai tuoi consumatori del servizio. Quando sviluppi un servizio di cui è possibile eseguire il bind, devi utilizzare le [operazioni di cui è possibile eseguire il bind nella API Open Service Broker v2.12](https://github.com/openservicebrokerapi/servicebroker/blob/v2.12/spec.md#binding){: new_window} ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")
   3. Completa i campi obbligatori aggiuntivi e fai clic su **Save**.
3. La pagina Offering presenta ora un segno di spunta nella navigazione, che indica che hai soddisfatto i requisiti minimi per completare questa pagina. Se la pagina è ancora contrassegnata come incompleta, devi riaprire la pagina e controllare la presenza di eventuali campi *obbligatori* incompleti.

La tua lettera di offerta iniziale include un URL di documentazione di servizio che era stato generato dal workbench Provider. Devi immettere tale URL nei campi **Documentation URL** e **Instructions URL**
{: tip}

## Esegui la registrazione presso IAM
{: #reg-iam}

IAM è obbligatorio per tutti i servizi d cui viene eseguito l'onboarding in {{site.data.keyword.Bluemix_notm}}. Vedi [ Cos'è IAM?](/docs/iam?topic=iam-iamoverview#iamoverview) per ulteriori informazioni sui concetti e i requisiti di IAM.

La console di gestione delle risorse genera i seguenti valori IAM:
   - ID servizio (generato e archiviato)
   - Chiave API (generata, non archiviata - visualizzata una sola volta)
   - ID client (generato e archiviato)
   - Segreto client (generato, non archiviato)

Il provider di servizi deve fornire:
   - URI di reindirizzamento (ritornerai alla console di gestione delle risorse dopo aver sviluppato il tuo OSB. Deriva l'URI di reindirizzamento dall'ubicazione del broker dei servizi ospitato).

1. Dalla console di gestione delle risorse, fai clic sulla pagina **Access Management**.
2. Fai clic su **Enable IAM**. La console di gestione delle risorse registra il tuo servizio presso IAM, crea il tuo ID e la tua politica di servizio e crea una chiave API per te. Crea inoltre un segreto e un ID client incompleti. L'ID client deve essere aggiornato con il tuo URI di reindirizzamento dopo che ne disporrai.
3. Fai clic su **Status** per vedere lo stato corrente della tua abilitazione IAM.

Devi tornare alla pagina IAM successivamente per fornire il tuo URI di reindirizzamento (`Redirect URI`). Non disporrai di questo valore finché non eseguirai dello sviluppo aggiuntivo per creare un flusso di autenticazione. I passi successivi ti aiuteranno nella procedura di discernimento del tuo valore di URI di reindirizzamento.
{: note}

Ti viene data la tua chiave API quando abiliti IAM (**Enable IAM**). È fondamentale che salvi la chiave API. Il valore non viene visualizzato nuovamente. Se perdi la tua chiave API, puoi eliminare la chiave e crearne una nuova: [Gestione delle chiavi API di un ID servizio](/docs/iam?topic=iam-serviceidapikeys#serviceidapikeys).
{: tip}

## Sviluppa un piano di prezzi
{: #pricing-plan}

Quando esegui l'onboarding del tuo servizi in {{site.data.keyword.Bluemix_notm}}, devi definire un piano di prezzi. Se hai una conoscenza dettagliata del modo in cui vuoi addebitare agli utenti il tuo servizio, puoi fornire tali informazioni nel tuo piano. Tuttavia, se non hai definito un piano a pagamento, puoi iniziare abilitando un piano gratuito e tornare quindi successivamente a configurare un piano a pagamento.

1. Dalla console di gestione delle risorse, fai clic sulla pagina **Pricing**.
2. Fai clic su **Add plan** per creare una nuova voce di piano e fai clic su **Edit plan** per modificare il piano.
   * **Free plan**: tutte le offerte possono avere un piano Lite che è gratuito, consentendo agli utenti di provare il tuo servizio. I piani gratuiti utilizzano *Lite* per **Display Name** e *lite* per **Programmatic Name**. Specifica **Yes** per **Is this plan free?**. Fai clic su **Save**. Il tuo piano viene pubblicato nel catalogo {{site.data.keyword.Bluemix_notm}}.
   * **Subscription plan**: specifica **No** per **Is this plan free?**. Completa i campi obbligatori. Lascia la metrica **Pricing metrics** predefinita. Questa metrica predefinita ti viene fornita perché tu possa utilizzarla per addebitare agli utenti una tariffa mensile una tantum. Fai clic su **Save**. Il tuo piano viene pubblicato nel catalogo {{site.data.keyword.Bluemix_notm}}. Salva il comando curl di esempio per inoltrare l'utilizzo.
   * **Metered plan**: specifica **No** per **Is this plan free?**. Completa i campi obbligatori. Elimina (*Delete*) la metrica di sottoscrizione **Pricing metrics**. Fai clic su **Add another metric**, completa la pagina **Add pricing metric** e fai clic su **Add metric**. Fai clic su **Save**. Il tuo piano viene pubblicato nel catalogo {{site.data.keyword.Bluemix_notm}}. Salva il comando curl di esempio per inoltrare l'utilizzo. Per assistenza nella selezione delle metriche corrette, vedi [Integrazione della misurazione](/docs/third-party?topic=third-party-content-tasks#content-tasks).
3. La pagina **Pricing** deve ora essere contrassegnata come completa, a indicare che hai soddisfatto i requisiti minimi per completare questa pagina.

I provider di servizi devono anche automatizzare l'inoltro dell'utilizzo orario per tutti i piani a consumo. Per ulteriori informazioni, vedi: [Inoltro dell'utilizzo per i piani a consumo](/docs/third-party?topic=third-party-submitusage#submitusage).
{: tip}

## Esporta i tuoi metadati come JSON
{: #export-metadata}

Ora che hai definito il tuo servizio nella console di gestione delle risorse, puoi scaricare un file catalog.json e utilizzarlo per informare lo sviluppo del tuo Open Service Broker. Il catalog.json ha i metadati che devono essere ospitati nel tuo broker. Questi valori definiscono il contratto tra il broker e la piattaforma {{site.data.keyword.Bluemix_notm}} per i servizi e i piani supportati dal broker. Tutti i metadati del catalogo aggiuntivi che non sono richiesti per il provisioning sono memorizzati nel catalogo {{site.data.keyword.Bluemix_notm}}. Gli eventuali aggiornamenti ai valori di visualizzazione del catalogo utilizzati per riprodurre il tuo dashboard, come link, icone e metadati tradotti in i18n, sono aggiornati nella console di gestione delle risorse. Non sono ospitati nel tuo broker. Nessuno dei metadati archiviati nel tuo broker viene visualizzato nella console {{site.data.keyword.Bluemix_notm}} o nella CLI {{site.data.keyword.Bluemix_notm}}. La console e la CLI restituiscono quello che era stato impostato nella console di gestione delle risorse e archiviato nel catalogo {{site.data.keyword.Bluemix_notm}}.

1. Dalla console di gestione delle risorse, apri la pagina **Deployments**.
2. Fai clic su **Manage**.
3. Fai clic su **Download Definitions**.

Salva il tuo file `catalog.json`. Lo utilizzerai per sviluppare il tuo Open Service Broker nella prossima sezione.

## Passi successivi
{: #cis2-next-steps}

Ben fatto. Hai definito la tua offerta di servizio aggiungendo i metadati di visualizzazione del catalogo, eseguendo la registrazione presso IAM e creando uno o più piani di prezzi. Puoi quindi prendere il tuo JSON esportato e iniziare a sviluppare un broker dei servizi. Vedi [Passo 3: Sviluppa e ospita i broker di servizi](/docs/third-party?topic=third-party-step3-osb#step3-osb).
