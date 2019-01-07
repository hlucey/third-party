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

# In che modo i servizi di fatturazione integrati utilizzano la piattaforma {{site.data.keyword.Bluemix_notm}}
{: #how-it-works}

I servizi di fatturazione integrati sono diversi dai servizi di riferimento. Un servizio di fatturazione integrato utilizza la piattaforma {{site.data.keyword.Bluemix_notm}} per l'autenticazione, l'accesso, il provisioning, la misurazione e la fatturazione. Questo argomento fornisce una panoramica di alto livello dei componenti della piattaforma che vengono utilizzati dal tuo servizio di fatturazione integrato.

## Livello di provisioning {{site.data.keyword.Bluemix_notm}}
{: #provisioning-layer}

Il livello di provisioning gestisce il ciclo di vita delle risorse {{site.data.keyword.Bluemix_notm}}. Il livello di provisioning è responsabile del controllo e della traccia del ciclo di vita delle risorse in un account del cliente. Le *risorse* sono componenti fisici o logici di cui è possibile eseguire il provisioning, o che possono essere riservati, per un'istanza dell'applicazione o del servizio. Esempi di risorse includono database, account, processore, memoria e limiti di archiviazione. In generale, è previsto che alle risorse tracciate dal livello di provisioning siano associate delle metriche di utilizzo e una fatturazione ma non è sempre così. In alcuni casi, la risorsa può essere associata al livello di provisioning per garantire che il ciclo di vita della risorsa possa essere gestito insieme al ciclo di vita dell'account.

### Gestione del ciclo di vita della risorsa
{: #lifecycle}

Il livello di provisioning fornisce delle API comuni per controllare il ciclo di vita delle risorse che va dal provisioning (creazione di un'istanza). all'esecuzione del bind (creazione delle credenziali di accesso), all'annullamento del bind (rimozione dell'accesso) e all'annullamento del provisioning (eliminazione di un'istanza). Inoltre, la piattaforma {{site.data.keyword.Bluemix_notm}} fornisce le CLI e una IU che possono gestire il ciclo di vita di queste risorse che non richiedono che tu crei delle tue funzioni.

Il livello di provisioning fornisce le API che ti aiutano a gestire i seguenti elementi del tuo ciclo di vita delle risorse:
* Provisioning
* Aggiornamento di un'istanza della risorsa
* Esecuzione del bind
* Chiavi di risorsa
* Annullamento del bind
* Annullamento del provisioning

## {{site.data.keyword.Bluemix_notm}} IAM (Identity and Access Management)
{: #iam}

IAM (Identity Access Management) ti consente di autenticare in modo sicuro gli utenti e controllare l'accesso a tutte le risorse cloud in modo congruente in tutto {{site.data.keyword.Bluemix_notm}}. Il livello di provisioning {{site.data.keyword.Bluemix_notm}} ha adottato IAM per l'autenticazione e l'autorizzazione delle azioni eseguite sul livello di provisioning. I provider di offerte di terze parti usano IAM per creare un flusso di autenticazione (OAuth). Per ulteriori informazioni, vedi [Cos'è IAM](/docs/iam/index.html#iamoverview)?

Se la tua offerta utilizza librerie OIDC (OpenID Connect), IAM supporta l'integrazione OIDC. OIDC è un livello di autenticazione in aggiunta a OAuth 2.0, un framework di autorizzazione, e può aiutare a semplificare il processo di onboarding. Per ulteriori informazioni su OIDC, vedi [Open ID Connect](http://openid.net/connect/){: new_window} ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno").

## Catalogo {{site.data.keyword.Bluemix_notm}}
{: #catalog}

Il catalogo {{site.data.keyword.Bluemix_notm}} archivia le definizioni di offerte (descrizione, funzioni, immagini, URL e così via) delle risorse visualizzate nella console{{site.data.keyword.Bluemix_notm}}. La console di gestione delle risorse viene utilizzata per definire tutti gli aspetti dei metadati obbligatori del servizio. Questi metadati vengono pubblicati nel catalogo e utilizzati per la visualizzazione nel catalogo. Puoi trovare informazioni dettagliate sui campi di metadati obbligatori e facoltativi nelle pagine **Offering** e **Plan** nella console di gestione delle risorse. Gli elementi chiave sono inclusi in questa sezione per consentirti di comprendere tutto in tempi più brevi

   * Service Name: nome tecnico per il tuo servizio. Il nome servizio è di importanza critica e deve essere definito correttamente. Devi fornire sia un nome servizio che viene utilizzato per identificare il servizio dalla piattaforma {{site.data.keyword.Bluemix_notm}} sia un nome di visualizzazione che i tuoi clienti vedono nel catalogo {{site.data.keyword.Bluemix_notm}}. Il tuo nome servizio non è il tuo nome di visualizzazione.
   * Service Display Name: nome descrittivo per il tuo servizio. Ad esempio, "Compose Redis"
   * Service ID: GUID per il tuo servizio utilizzato nelle chiamate API al tuo broker OSB. Questo valore deve essere univoco.
   * Service Icon: SVG con il tuo logo del servizio
   * Service Description: la descrizione della risorsa visualizzata quando passi il puntatore del mouse sull'icona della risorsa nell'interfaccia utente del catalogo {{site.data.keyword.Bluemix_notm}}. Puoi aggiungere una singola parola o frase per la descrizione.
   * Service Detailed Description: il primo paragrafo che compare nella pagina di elenco del catalogo. Valuta almeno due frasi per una descrizione dettagliata.
   * Documentation URL: un link alla tua documentazione {{site.data.keyword.Bluemix_notm}}. Eseguirai la creazione in PWB e il tuo valore url viene generato da PWB per te.
   * Terms URL: un link ai termini e alla condizioni per l'utilizzo del tuo servizio. Nota: ai fini del GDPR, non eseguire il collegamento ai termini e alle condizioni del tuo servizio di terze parti esistente. Devi invece fornire una pagina univoca per un servizio di fatturazione integrato.
   * Instructions URL: in modo analogo a Documentation URL, punterai alla tua documentazione {{site.data.keyword.Bluemix_notm}}; tuttavia, l'Instructions URL estrae dinamicamente la tua documentazione in una scheda Getting Started nel dashboard del tuo servizio.
   * Category: selezione delle categorie {{site.data.keyword.Bluemix_notm}} disponibili dove viene inserito il tuo servizio nel catalogo.
   * Bullets: brevi punti descrittivi relativi al tuo servizio
   * Media: acquisizioni di schermo e video relativi al tuo servizio
   * Service Plan Name: ogni piano ha un nome tecnico. Tutto in minuscole, senza spazi, può includere "-". Ad esempio, `gold`.
   * Service Plan Display Name: nome descrittivo per il piano. Ad esempio, `Gold`
   * Service Plan ID: GUID per il tuo piano del servizio utilizzato nelle chiamate API al tuo broker OSB. Questo valore deve essere univoco. La console di gestione delle risorse genera questo valore per te.
   * Service Plan Description: la descrizione del piano risorse. La descrizione viene visualizzata quando selezioni un piano nella pagina dei dettagli della risorsa nel catalogo IBM Cloud.
   * Service Plan Bullets: brevi punti descrittivi relativi al tuo piano di servizio.


## Open Service Broker
{: #open-service}

I broker dei servizi gestiscono il ciclo di vita dei servizi. La piattaforma {{site.data.keyword.Bluemix_notm}} interagisce con i broker dei servizi per eseguire il provisioning e la gestione delle istanze del servizio (un'istanziazione di un'offerta di servizi) e dei bind di servizio (la rappresentazione di un'associazione tra un'applicazione e un'istanza del servizio, che spesso include le credenziali che vengono utilizzate dall'applicazione per comunicare con l'istanza del servizio). Fornire dei valori di metadati validi crea una risposta API REST corretta quando viene eseguita una richiesta.

{{site.data.keyword.Bluemix_notm}} utilizza la specifica dell'API OSB (Open Service Broker) `versione 2.12`. Leggi attentamente e familiarizza con la [specifica API Open Broker](https://github.com/openservicebrokerapi/servicebroker/blob/v2.12/spec.md){: new_window} ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno") e utilizza il file readme come guida per saperne di più.

Quando il controller della risorsa riceve una richiesta di provisioning di una risorsa, richiama il tuo OSB per convalidare il tipo di servizio, l'offerta, i piani e la disponibilità delle regioni. Il controller della risorsa convalida anche la visibilità del piano associato all'account del cliente. {{site.data.keyword.Bluemix_notm}} fornisce degli esempi di broker e dei documenti API che estendono la specifica OSB. Puoi trovare ulteriori dettagli sullo sviluppo e sull'hosting del tuo broker man mano che affronti la dettagliata procedura di sviluppo dell'onboarding della fatturazione integrato.

## Servizio di misurazione {{site.data.keyword.Bluemix_notm}}
{: #metering-service}

Se un servizio offre un piano a consumo, l'addebito a carico degli utenti {{site.data.keyword.Bluemix_notm}} è basato sulla quantità di risorse da essi utilizzata. Ad esempio, l'addebito a carico degli utenti {{site.data.keyword.Bluemix_notm}} che utilizzano i servizi database potrebbe essere basato sulla quantità di archiviazione utilizzata dalle loro applicazioni. L'inoltro dell'utilizzo deve essere eseguito per consentire la conversione dell'utilizzo in un record addebitabile.

Tutti i servizi di fatturazione integrati che offrono un piano a consumo devono utilizzare il servizio di misurazione {{site.data.keyword.Bluemix_notm}} per notificare i dati di utilizzo.

Devi automatizzare l'inoltro dell'utilizzo orario utilizzando l'API di servizio di misurazione, se offri un piano a consumo.
{: important}

Per ulteriori informazioni sulla misurazione, vedi: [Integrazione della misurazione](/docs/third-party/metering.html#meteringintera). Per ulteriori informazioni sull'inoltro dell'utilizzo a consumo, vedi [Inoltro dell'utilizzo per i piani a consumo](/docs/third-party/submitusage.html#submitusage)

## Scenario di provisioning: assemblaggio di tutti i concetti

Mettiamo ora insieme tutti i concetti e guardiamo un esempio di come funziona la creazione di un'istanza del servizio utilizzando la piattaforma {{site.data.keyword.Bluemix_notm}}.

![Scenario di provisioning](images/flow-am.svg "Modo in cui la piattaforma gestisce la creazione dell'istanza del servizio")

Quando un utente desidera creare un'istanza del servizio, può farlo in uno dei seguenti due modi:
* **CLI**: utilizzando `ibmcloud cli [ ibmcloud resource service-instance-create NAME SERVICE_NAME SERVICE_PLAN_NAME LOCATION ]`
* **Console {{site.data.keyword.Bluemix_notm}}**: l'utente può selezionare il piano del servizio e utilizzare l'operazione **Crea**.

La piattaforma {{site.data.keyword.Bluemix_notm}} convalida che l'utente dispone dell'autorizzazione a creare l'istanza del servizio utilizzando {{site.data.keyword.Bluemix_notm}} IAM. Dopo l'esecuzione di tale convalida, viene avviato l'endpoint di provisioning del tuo broker dei servizi (PUT /v2/resource_instances/:resource_instance_id). Quando viene eseguito il provisioning, devono essere soddisfatte le seguenti regole:
* Il contesto {{site.data.keyword.Bluemix_notm}} è incluso nella variabile di contesto
* L'`X-Broker-API-Originating-Identity` ha l'ID IBM IAM dell'utente che ha avviato la richiesta
* La sezione parameters include l'ubicazione richiesta (e i parametri aggiuntivi richiesti dal tuo servizio).

Richiesta di provisioning di esempio:

```
    PUT /v2/service_instances/crn%3Av1%3Abluemix%3Apublic%3Acompose-redis%3Aus-south%3Aa%2F46aa677e-e83f-4d17-a2b6-5b752564477c%3A416d769b-682d-4833-8bd7-5ef8778e5b52?accepts_incomplete=true HTTP/1.1
    Host:  https://broker.compose.cloud.ibm.com
    Authorization: basic dXNlcjpwYXNzd29yZA==
    X-Broker-Api-Version: 2.12
    X-Broker-API-Originating-Identity: ibmcloud aWJtaWQtNDU2MzQ1WA==
    {
      "service_id": "0bc9d744-6f8c-4821-9648-2278bf6925bb", // il GUID del tuo servizio dall'onboarding
      "plan_id": "ecc19311-aba2-49f7-8198-1e450c8460d4", //il GUID del tuo piano dall'onboarding
      "context": {
        "platform": "ibmcloud",
        "account_id": "003e9bc3993aec710d30a5a719e57a80",
        "crn": "crn:v1:bluemix:public:compose-redis:us-south:a/003e9bc3993aec710d30a5a719e57a80:416d769b-682d-4833-8bd7-5ef8778e5b52",
        "resource_group_crn": "crn:v1:bluemix:public:resource-controller::a/003e9bc3993aec710d30a5a719e57a80::resource-group:b4570a825f7f4d57aa54e8e1d9507926",
        "target_crn": "crn:v1:bluemix:public:resource-catalog::a/e97a8c01ac694e308ef3ad7795c7cdb3::deployment:e62e2c19-0c3b-41e3-b8b3-c71762ecd489:us-south38399"
      },
      "parameters": {
        "location": "us-south",
        "optional-param":"parametro richiesto dal tuo servizio"
      }
    }
```

### Descrizione del parametro `context` di {{site.data.keyword.Bluemix_notm}}
{: #parameter}

Nell'esempio precedente, puoi vedere i metadati restituiti nel parametro `context`. Il contesto di provisioning per {{site.data.keyword.Bluemix_notm}} restituisce quanto segue:

* **platform**: identifica la piattaforma come "ibmcloud"

* **"account_id"**: restituisce l'ID dell'account in {{site.data.keyword.Bluemix_notm}} che sta eseguendo il provisioning dell'istanza del servizio.

* **crn**: quando un cliente esegue il provisioning del tuo servizio in {{site.data.keyword.Bluemix_notm}}, viene creata un'istanza del servizio e questa istanza è identificata dal suo {{site.data.keyword.Bluemix_notm}} Resource Name (CRN). Il CRN viene utilizzato in tutti gli aspetti dell'interazione con {{site.data.keyword.Bluemix_notm}} incluso il provisioning, il bind (creazione di credenziali e endpoint), la misurazione, la visualizzazione del dashboard e il controllo dell'accesso. Dalla prospettiva di un provider di offerte, il CRN può essere per lo più trattato come stringa opaca da utilizzare con le API {{site.data.keyword.Bluemix_notm}}. Può anche essere decomposto utilizzando la seguente struttura:

   ```
   crn:version:cname:ctype:service-name:location:scope:service-instance:resource-type:resource
   ```

   Nell'esempio di provisioning, vediamo che il CRN del servizio `compose-redis` è:

   ```
   crn:v1:bluemix:public:compose-redis:us-south:a/46aa677e-e83f-4d17-a2b6-5b752564477c:416d769b-682d-4833-8bd7-5ef8778e5b52::
   ```

   In questo esempio, questa istanza `compose-redis` fa parte dell'account {{site.data.keyword.Bluemix_notm}} con ID. L'ID univoco per l'istanza è `416d769b-682d-4833-8bd7-5ef8778e5b52` e l'istanza è ospitata nella regione `us-south` di {{site.data.keyword.Bluemix_notm}} pubblico.

* **resource_group_crn**: restituisce il gruppo di risorse che include l'istanza del servizio. Per ulteriori dettagli, vedi [Gestione dei gruppi di risorse](/docs/resources/resourcegroups.html).

   I provider di offerte non devono preoccuparsi del `resource_group_crn`, tranne in circostanze eccezionali. Consulta il tuo rappresentante IBM sul tuo caso di utilizzo prima di utilizzare tale campo.
   {: note}

