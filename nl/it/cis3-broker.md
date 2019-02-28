---


copyright:
  years: 2018, 2019
lastupdated: "2019-02-20"


---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:note: .note}
{:download: .download}

# Passo 3. Sviluppa e ospita i tuoi broker dei servizi
{: #step3-osb}

Utilizzando i metadati che hai esportato dalla console di gestione delle risorse, puoi creare uno o più nuovi broker dei servizi nel linguaggio di programmazione che preferisci.
{:shortdesc}

I broker dei servizi gestiscono il ciclo di vita dei servizi. La piattaforma {{site.data.keyword.Bluemix_notm}} interagisce con i broker di servizio per eseguire il provisioning e la gestione delle istanze del servizio e delle associazioni mediante bind del servizio. Puoi fornire dei valori di metadati validi per creare una risposta API RESTful con esito positivo quando viene effettuata una richiesta.

Puoi creare il tuo broker utilizzando una combinazione dei metadati che hai esportato dalla console di gestione delle risorse, i nostri esempi di broker dei servizi {{site.data.keyword.Bluemix_notm}} pubblici e la documentazione dell'API Resource Broker.

## Prima di iniziare
{: #broker-pre-reqs}

Assicurati di aver iniziato il passo 1 e completato il passo 2:
1. [Crea i documenti e il comunicato di marketing del servizio](/docs/third-party?topic=third-party-content-tasks#content-tasks).
2. [Definisci la tua offerta nella console di gestione delle risorse](/docs/third-party?topic=third-party-step2-define#step2-define).


## Visualizza il nostro scenario di provisioning della piattaforma {{site.data.keyword.Bluemix_notm}}
{: #scenario}

Stai sviluppando un OSB (Open Service Broker) che funziona con la piattaforma {{site.data.keyword.Bluemix_notm}}. Vedi il nostro [Scenario di provisioning](/docs/third-party?topic=third-party-how-it-works#provision2) per comprendere come funziona la creazione delle risorse.

## Acquisisci familiarità con la specifica OSB
{: #learn-osb}

{{site.data.keyword.Bluemix_notm}} utilizza la specifica dell'API OSB (Open Service Broker) `versione 2.12`. Leggi attentamente e familiarizza con la [specifica API Open Broker](https://github.com/openservicebrokerapi/servicebroker/blob/v2.12/spec.md){: new_window} ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno") e utilizza il file readme come guida per saperne di più.

## Visualizza i nostri esempi di broker {{site.data.keyword.Bluemix_notm}}
{: #samples}

[https://github.com/IBM/sample-resource-service-brokers](https://github.com/IBM/sample-resource-service-brokers){: new_window} ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")

Non tutti i linguaggi sono rappresentati da un esempio. Se hai bisogno di un broker Python di esempio, puoi trovare un esempio di Cloud Foundry cercando su Google. Potresti dover adattare questo esempio per soddisfare i requisiti OSB.
{: note}

## Visualizza la nostra documentazione API {{site.data.keyword.Bluemix_notm}} Open Service Broker
{: #docs}

I broker dei servizi possono essere sviluppati avendo già una conoscenza dell'[API {{site.data.keyword.Bluemix_notm}} Open Service Broker](https://{DomainName}/apidocs/ibm-cloud-osb-api){: new_window} ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno"). Acquisisci familiarità con l'API Broker e scopri in che modo interagisce con i tuoi broker.

L'{{site.data.keyword.Bluemix_notm}} Open Service Broker estende la specifica di Open Service Broker 2.12.
{: tip}

### Logica dell'endpoint richiesta per tutti i broker dei servizi
{: #endpoint-sb}

I broker dei servizi devono fornire un insieme standard di valori di metadati che vengono utilizzati dalle API REST e i broker {{site.data.keyword.Bluemix_notm}} devono avere la logica per i seguenti endpoint o percorsi dell'API REST:

<dl>
  <dt>catalog (GET)</dt>
  <dd>Restituisce i metadati del catalogo inclusi nel tuo broker. Molti valori di metadati del catalogo supplementari non vengono restituiti - questi valori vengono aggiunti esclusivamente all'interno della console di gestione delle risorse e memorizzati nel catalogo {{site.data.keyword.Bluemix_notm}}.</dd>
  <dt>resource instances (PUT)</dt>
  <dd>Esegue il provisioning della tua istanza del servizio.</dd>
  <dt>resource instances (DELETE)</dt>
  <dd>Annulla il provisioning della tua istanza del servizio.</dd>
  <dt>resource instances (PATCH)</dt>
  <dd>Aggiorna la tua istanza del servizio.</dd>
</dl>

**Nota su catalog (GET)**: questo endpoint definisce il contratto tra il broker e la piattaforma {{site.data.keyword.Bluemix_notm}} per i servizi e i piani supportati dal broker. Questo endpoint restituisce i metadati del catalogo memorizzati all'interno del tuo broker. Questi valori definiscono il contratto di provisioning minimo tra il tuo servizio e la piattaforma {{site.data.keyword.Bluemix_notm}}. Tutti i metadati del catalogo aggiuntivi che non sono richiesti per il provisioning sono memorizzati nel catalogo {{site.data.keyword.Bluemix_notm}}. Gli eventuali aggiornamenti ai valori di visualizzazione del catalogo utilizzati per riprodurre il tuo dashboard come link, icone e metadati tradotti in i18n devono essere aggiornati nella console di gestione delle risorse e non ospitati nel tuo broker. Nessuno dei metadati archiviati nel tuo broker viene visualizzato nella console {{site.data.keyword.Bluemix_notm}} o nella CLI {{site.data.keyword.Bluemix_notm}}. La console e la CLI restituiscono quello che era stato impostato nella console di gestione delle risorse e archiviato nel catalogo {{site.data.keyword.Bluemix_notm}}. La seguente sezione mostra i valori minimi richiesti restituiti da catalog (GET):

```
{
       "services":[
   {
           "id": "ibmcloud-link",
           "name": "ibmcloud-link",
           "description": "An IBM provided service that enables aliasing to service instances in the {{site.data.keyword.Bluemix_notm}}.",
           "bindable": true,
           "plan_updateable": false,
           "plans": [
               {
                   "id": "ibmcloud-link-alias",
                   "name": "ibmcloud-alias",
                   "free": true,
                   "description": "The {{site.data.keyword.Bluemix_notm}} alias plan used for linking."
               }
               ]
       }]
}
```

### Logica di endpoint richiesta per i servizi associabili
{: #bindable}

Se il tuo servizio può essere associato alle applicazioni in {{site.data.keyword.Bluemix_notm}}, deve restituire credenziali ed endpoint API agli utenti del tuo servizio. Un servizio associabile deve utilizzare le operazioni associabili nella specifica Open Service Broker e implementare i seguenti endpoint o percorsi:

<dl>
  <dt>bindings and credentials (PUT)</dt>
  <dd>Esegue il bind della tua istanza del servizio a un'applicazione.</dd>
  <dt>bindings and credentials (DEL)</dt>
  <dd>Annulla il bind della tua istanza del servizio da un'applicazione.</dd>
</dl>

### Endpoint di estensione {{site.data.keyword.Bluemix_notm}} richiesti
{: #extension} 

La specifica OSB non* supporta uno stato di istanza disabilitata ma non ancora eliminata. Affinché {{site.data.keyword.Bluemix_notm}} supporti i clienti che potrebbero subire un'interruzione della fatturazione o altre situazioni che comportano la sospensione dell'account (ma non ancora l'annullamento), {{site.data.keyword.Bluemix_notm}} ha definito endpoint API estesi che consentono di disabilitare e riabilitare le istanze del servizio. Le seguenti estensioni dell'endpoint sono **obbligatorie**:

<dl>
  <dt>enable and disable instances (GET)</dt>
  <dd>Stato - restituisce lo stato della tua istanza del servizio.</dd>
  <dt>enable and disable instances (PUT)</dt>
  <dd>Ti consente di abilitare o disabilitare un'istanza del servizio.</dd>
</dl>

È responsabilità del provider di servizi disabilitare l'accesso all'istanza del servizio quando viene avviato l'endpoint di disabilitazione e riabilitare tale accesso quando viene avviato l'endpoint di abilitazione.
{: note}

## Scopri come utilizzare i metadati esportati per guidare lo sviluppo del tuo broker
{: #use-metadata}

I metadati che hai esportato dalla console di gestione delle risorse possono essere utilizzati come guida per lo sviluppo del tuo broker. Non tutti i valori immessi nella console di gestione delle risorse sono necessari per eseguire il provisioning di un servizio. I metadati esportati dalla console di gestione delle risorse definiscono il contratto di provisioning minimo tra il tuo servizio e la piattaforma {{site.data.keyword.Bluemix_notm}}. Il tuo JSON esportato fornisce i seguenti valori:

```
{
services :
            [
                {
                    bindable         : true,
                    description      : "Test Node Resource Service Broker Description",
                    // TODO - GUID generated by http://www.guidgenerator.com
                    // TODO - This service id must be unique within an IBM Cloud environment's set of service offerings
                    id               : "df35cab6-347b-4ba5-8f39-e9c23a237f5b",
                    metadata         :
                    {
                        displayName         : "Test Node Resource Service Broker Display Name",
                        documentationUrl    : baseMetadataUrl + "documentation.html",
                        imageUrl            : baseMetadataUrl + "services.svg", // Copied from https://github.com/carbon-design-system/carbon-icons/blob/master/src/svg/services.svg
                        instructionsUrl     : baseMetadataUrl + "instructions.html",
                        longDescription     : "Test Node Resource Service Broker Long Description",
                        providerDisplayName : "Company Name",
                        supportUrl          : baseMetadataUrl + "support.html",
                        termsUrl            : baseMetadataUrl + "terms.html"
                    },
                    name             : SERVICE_NAME,
                    // TODO - Ensure this value is accurate for your service. Requires PATCH of /v2/service_instances/:instance_id below if true
                    plan_updateable  : true,
                    tags             : ["lite", "tag1a", "tag1b"],
                    plans            :
                    [
                        {
                            bindable    : true,
                            description : "Test Node Resource Service Broker Plan Description",
                            free        : true,
                            // TODO - GUID generated by http://www.guidgenerator.com
                            // TODO - This service plan id must be unique within an IBM Cloud environment's set of service plans
                            id          : "2a1d139b-1b05-4e33-b72e-a1f8c14be559",
                            metadata    :
                            {
                                bullets     : ["Test bullet 1", "Test bullet 2"],
                                displayName : "Lite"
                            },
                            // TODO - This service plan name must be unique within the containing service definition
                            name        : "lite"
                        }
                    ]
                }
            ]
}
```


Il tuo array di servizi OSB deve essere uguale ai metadati dell'offerta che hai aggiunto alla console di gestione delle risorse. Per garantire la parità uno a uno tra l'OSB e la console di gestione delle risorse, è fondamentale confrontare l'array di servizi nel `catalog.json` scaricato dalla console di gestione delle risorse con l'effettivo array di servizi nel tuo broker. Tutti i nomi e gli ID dei servizi e dei piani devono corrispondere.
{: tip}

## Informazioni del broker fornite dalla piattaforma {{site.data.keyword.Bluemix_notm}}
{: #broker info}

Il tuo broker dei servizi riceve le seguenti informazioni dalla piattaforma {{site.data.keyword.Bluemix_notm}}:

### X-Broker-API-Originating-Identity
{: #x-broker}

L'**intestazione dell'identità utente** viene fornita tramite un'intestazione di identità di origine API. Questa intestazione di richiesta include l'identità {{site.data.keyword.Bluemix_notm}} IAM dell'utente. L'identità IAM è codificata in base64. {{site.data.keyword.Bluemix_notm}} supporta un'unica area di autenticazione: `IBMid`. L'area di autenticazione `IBMid` utilizza un IUI (IBMid Unique ID) per identificare l'identità dell'utente in {{site.data.keyword.Bluemix_notm}}. Questo IUI è una stringa opaca per il provider di servizi.

Esempio:

```
X-Broker-API-Originating-Identity: ibmcloud eyJpYW1faWQiOiJJQk1pZC01MEdOUjcxN1lFIn0=
Decoded:
{"iam_id":"IBMid-50GNR717YE"}
```

### Versione dell'intestazione API
{: #api-header}

L'**intestazione della versione API** è [2.12](https://github.com/openservicebrokerapi/servicebroker/blob/v2.12/spec.md){: new_window} ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno"). Ad esempio: `X-Broker-Api-Version: 2.12`.

### resource instance (PUT) body.context and resource instance (PATCH) body.context
{: #put}

`PUT /v2/service_instances/:resource_instance_id` e `PATCH /v2/service_instances/:resource_instance_id` ricevono il seguente valore all'interno di **body.context**: `{ "platform": "ibmcloud", "account_id": "tracys-account-id", "crn": "resource-instance-crn" }`.

## Ulteriori suggerimenti sul broker
{: #more-info}

### Suggerimenti sull'utilizzo delle operazioni asincrone invece di quelle sincrone
{: #asynch-ops}

L'API OSB supporta entrambe le modalità di operazione sincrone e asincrone. Se le tue operazioni richiedono meno di 10 secondi, sono consigliate le risposte sincrone. In caso contrario, devi utilizzare la modalità di operazione asincrona. Ulteriori informazioni sono disponibili nella specifica OSB.

Se l'operazione asincrona impiega meno di 10 secondi quando stai eseguendo il provisioning di un'istanza, la piattaforma andrà in timeout.
{: tip}

### Suggerimenti per la gestione dei broker nelle diverse ubicazioni
{: #managing-broker}

È importante che gli utenti comprendano l'ubicazione dei loro servizi cloud per la latenza, la disponibilità e la residenza dei dati.

Quando si esegue il provisioning delle istanze del servizio su {{site.data.keyword.Bluemix_notm}}, uno dei parametri obbligatori che gli utenti forniscono è l'ubicazione in cui desiderano che venga eseguito il provisioning dell'istanza del servizio. Alcuni servizi possono supportare il provisioning in più ubicazioni. Ad esempio, un servizio di database può supportare il provisioning in tutte le regioni {{site.data.keyword.Bluemix_notm}} o in un sottoinsieme.

Se il tuo servizio basato su API di terze parti è implementato in un altro cloud ed esposto in {{site.data.keyword.Bluemix_notm}}, l'ubicazione indica l'ubicazione del servizio nell'altro cloud.

Durante l'onboarding in {{site.data.keyword.Bluemix_notm}}, devi implementare almeno un broker OSB. Puoi avere più di un broker in base alla tua strategia di distribuzione e alle ubicazioni che desideri supportare per il tuo servizio. All'interno dello strumento della console di gestione delle risorse, hai stabilito l'associazione tra la tua tupla di servizio/piano/ubicazione e il broker che gestisce le operazioni per tale tupla. Le scelte tipiche sono quelle di definire un singolo broker per servire tutte le ubicazioni per il tuo servizio o di definire un broker per ogni ubicazione; questa scelta spetta al provider di servizi.

Per un elenco di ubicazioni disponibili, vedi [IBM Global Catalog Locations](https://globalcatalog.cloud.ibm.com//search?q=kind:geography){: new_window} ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno"). Se il tuo servizio richiede più ubicazioni da definire nel catalogo globale, consulta il team di onboarding {{site.data.keyword.Bluemix_notm}}.


## Ospita i tuoi broker
{: #host}

Il tuo broker deve essere ospitato come parte di un'applicazione in grado di rispondere alle chiamate API REST. Inoltre, la tua ubicazione ospitata deve soddisfare le linee guida di sicurezza di {{site.data.keyword.Bluemix_notm}}. Può essere ospitato in {{site.data.keyword.Bluemix_notm}} oppure esternamente, se è pubblicamente accessibile da {{site.data.keyword.Bluemix_notm}} stesso.

Per ospitare il tuo broker al di fuori di IBM, devi assicurarti che soddisfi le seguenti linee guida di sicurezza:
- Deve seguire il protocollo TLS (Transport Layer Security) versione 1.2
- Deve essere ospitato su un endpoint HTTPs valido accessibile sull'internet pubblico

Se vuoi ospitarlo in {{site.data.keyword.Bluemix_notm}}, puoi trovare informazioni sulla creazione di un'applicazione utilizzando i contenitori (Kubernetes) al seguente link: [Internal Adopters - Usage information](/docs/containers?topic=containers-cs_internal#cs_internal).

Avrai bisogno dell'ubicazione ospitata del tuo broker dei servizi per completare il prossimo passo. Tieni pronti l'URL e le credenziali associate alla tua applicazione quando prosegui al passo successivo.
{: tip}

## Come verificare il tuo broker dei servizi
{: #broker-test}

Devi convalidare il tuo broker eseguendo i comandi curl sui diversi endpoint che stai abilitando. Il file readme di esempio fornisce delle indicazioni eccellenti per il curl dei tuoi endpoint OSB: [https://github.com/IBM/sample-resource-service-brokers/blob/master/README.md](https://github.com/IBM/sample-resource-service-brokers/blob/master/README.md){: new_window} ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")

### Come eseguire il curl del tuo broker dei servizi
{: #curl-broker}
Utilizza il seguente esempio per verificare la risposta curl dei tuoi broker:

```
curl -X PUT  https://<sample-service-broker>/v2/service_instances/<encoded-resource-crn> \
     -u '<your broker user>:<your broker password>' \
     -H 'content-type: application/json' \
      -d '{ "context": {"platform": "ibmcloud", \
                        "account_id": "34ff5928-c3c7-4d46-bbf6-1a5628c325d1", \
                        "resource_group_crn": "crn:v1:bluemix:public:resource-controller::a/003e9bc3993aec710d30a5a719e57a80::resource-group:b4570a825f7f4d57aa54e8e1d9507926", \
                        "crn": "<resource-crn>", \
                        "target_crn": "<target_crn>"}, \
            "service_id": "a07f025c-90db-4652-afd1-cf4adfac93c8", \
            "plan_id": "fe442cec-2eef-41fe-9f92-58d6c094584f"}'
```

## Passi successivi
{: #cis3-next-steps}

Ottimo lavoro! Hai creato e ospitato un broker dei servizi che soddisfa la specifica OSB. Consulta [Passo 4: Sviluppa un flusso di autenticazione](/docs/third-party?topic=third-party-step4-iam#step4-iam).
