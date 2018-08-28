---


copyright:
  years: 2018
lastupdated: "2018-08-21"


---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:download: .download}

# Passo 4. Sviluppa un flusso di autenticazione

Quando hai definito la tua offerta, la pagina Access Management della console di gestione delle risorse ti ha fornito il segreto e l'ID client, l'ID servizio e la chiave API di {{site.data.keyword.Bluemix_notm}} Identity and Access Management (IAM). Ora puoi utilizzare questi valori per completare la seguente procedura:

1. Deriva il tuo URI di reindirizzamento in base alla tua gestione del tuo `dashboard_url`, ritorna alla console di gestione delle risorse e aggiungilo alla scheda IAM, assicurandoti di aggiornare il tuo ID client.
2. Sviluppa il flusso OAuth per l'autenticazione. Per completare questo flusso, utilizzerai i tuoi URI di reindirizzamento, il tuo id client e il tuo segreto client come parametri per le API REST `token_endpoint` IAM.
3. Convalida l'autorizzazione utente:
   1. Comunica con IAM per ottenere un token di accesso dalla tua chiave api.
   2. Convalida l'autorizzazione per l'utente al dashboard del servizio utilizzando `authorization_endpoint` (/v2/authz POST).

Questo passo presuppone che hai ricevuto l'approvazione a distribuire un servizio di fatturazione integrato. Se non hai ancora completato la registrazione e l'approvazione iniziali nel Provider Workbench, consulta l'[esercitazione introduttiva](/docs/third-party/index.html).
{: tip}

## Prima di iniziare

Assicurati di aver avviato il passo 1 e di aver completato i passi 2 e 3.
1. [Crea i documenti e il comunicato di marketing del servizio](/docs/third-party/cis1-docs-marketing.html).
2. [Definisci la tua offerta nella console di gestione delle risorse](/docs/third-party/cis2-rmc-define.html).
3. [Sviluppa e ospita i tuoi broker dei servizi](/docs/third-party/cis3-broker.html).


## Deriva il tuo URI di reindirizzamento IAM (console di gestione delle risorse: pagina IAM)

Quando hai definito il tuo servizio nella console di gestione delle risorse, hai generato un ID client, ma è probabile che in quel momento non disponevi di un URI di reindirizzamento. Questo significa che IAM ha creato un ID client che è impostato su false. Finché non ritorni alla console di gestione delle risorse con il tuo URI di reindirizzamento, non avrai un vero ID client.

La buona notizia è che nel passo di sviluppo precedente hai sviluppato un OSB e lo hai ospitato (hai probabilmente viso i valori IAM nel codice broker di esempio). Il `redirect_uri` è di norma l'url host dove risiede l'applicazione con qualche url aggiuntivo che gestirà l'autenticazione/autorizzazione.

 Ecco alcuni URI di reindirizzamento di esempio

```
https://myapp.bluemix.net/integrate/auth/callback
http://localhost:3000/auth/callback <-- per l'esecuzione di test in locale
```

Ritorna alla console di gestione delle risorse e aggiungi il tuo URI di reindirizzamento alla scheda IAM.

1. Esegui l'accesso alla console
2. Prendi l'URI di reindirizzamento
3. Ritorna alla console di gestione delle risorse
4. Dalla **scheda IAM**, incolla il tuo URI di reindirizzamento nel campo **Redirect URI**.
5. Fai clic su **Update Client ID** per aggiornare il tuo ID client.

Dovresti avere ora un ID client che capisce il tuo URI di reindirizzamento ed è impostato su true. Puoi utilizzare tale ID client nei passi successivi per sviluppare il tuo flusso OAuth.

## Sviluppa il tuo flusso OAuth per l'autenticazione
{: #oauth}


**Autenticazione - Passo 0:** trova l'endpoint regionale IAM per l'accesso all'IU più vicino alla tua applicazione distribuita richiamando `https://iam.bluemix.net/identity/.well-known/openid-configuration`.

```
curl -X GET \
  https://iam.bluemix.net/identity/.well-known/openid-configuration
```

```
HTTP/1.1 200 OK
Content-Type: application/json
{
  "issuer": "https://iam.bluemix.net/identity",
  "authorization_endpoint": "https://iam-region2.bluemix.net/identity/authorize",
  "token_endpoint": "https://iam-region2.bluemix.net/identity/token",
...
}
```

Questa richiesta può essere eseguita dopo che l'applicazione è stata avvitata e nuovamente se si verifica un malfunzionamento dell'`authorization_endpoint`. Dovresti essere in grado di archiviare in cache il valore `authorization_endpoint` per un breve periodo di tempo ed eseguire l'aggiornamento dopo la scadenza della cache o il riscontro di un errore.


**Autenticazione - Passo 1:** quando un utente accede al tuo `dashboard_url`, reindirizza il browser a `<authorization_endpoint>?client_id=<your-client-id>&redirect_uri=<your-redirect-uri>&response-type=code&state=<your-resource-instance-id>`


-> verrà visualizzato il prompt di accesso

-> l'utente immette le credenziali

-> callback del browser all'uri di reindirizzamento che fornisce un parametro di risposta "code" e un valore "state"


**Autenticazione - Passo 2:** scambia il codice per una chiamata al token di accesso

### POST <token_endpoint>

#### Intestazioni:
{: #headers1}

  - Authorization: Basic *[client id]: [client secret]*
  - Content-Type: application/x-www-form-urlencoded
  - Accept: application/json

#### Con parametri:
{: #parameters1}

  - client_id=*[id client]*
  - client_secret=*[segreto client]*
  - grant_type=authorization_code
  - response_type=cloud_iam
  - redirect_uri=*[stesso uri come il redirect_uri dal passo 1]*
  - code=*[codice dalla callback]*

```
curl -k -X POST \
  -u "<your-client-id>:<your-client-secret>" \
  -H "Content-Type: application/x-www-form-urlencoded" \
  -H "Accept: application/json" \
  --data-urlencode "client_id=<your-client-id>" \
  --data-urlencode "client_secret=<your-client-secret>" \
  --data-urlencode "grant_type=authorization_code" \
  --data-urlencode "response_type=cloud_iam" \
  --data-urlencode "code=<code-from-the-callback>" \
  --data-urlencode "redirect_uri=<redirect_uri>" \
  "https://iam-region2.bluemix.net/identity/token"
```
{: codeblock}

### Risposta:
{: #response1}

```
{
  "access_token": "eyJraWQiOiI......XmpBTIDdR5w",
  "refresh_token": "SPrXw5tBE3......KBQ+luWQVY=",
  "token_type": "Bearer",
  "expires_in": 3600,
  "expiration": 1473188353
}
```
{: codeblock}

  Assicurati di archiviare l'access_token dell'utente restituito in questa risposta poiché verrà utilizzato successivamente durante l'autorizzazione dell'utente.

Vedi l'esempio nei nostri broker di esempio: https://github.com/IBM/sample-resource-service-brokers

## Ora è il momento di convalidare l'autorizzazione utente
{: #validate}

1. Comunica con IAM per ottenere un token di accesso per una chiave api
2. Convalida l'autorizzazione per l'utente all'istanza del servizio (/v2/authz POST)

### Autorizzazione - Passo 1: Ottieni un token IAM {{site.data.keyword.Bluemix_notm}} utilizzando una chiave API.
{: #iam_token_using_api_key}

### POST /identity/token

#### Intestazioni:
{: #headers2}

  - Authorization: Basic *[client id]: [client secret]*
  - Content-Type: application/x-www-form-urlencoded
  - Accept: application/json

#### Con parametri:
{: #parameters2}

  - grant_type=urn:ibm:params:oauth:grant-type:apikey
  - response_type=cloud_iam
  - apikey=*[Chiave api]*

```
curl -k -X POST \
  -H "Content-Type: application/x-www-form-urlencoded" \
  -H "Accept: application/json" \
  --data-urlencode "grant_type=urn:ibm:params:oauth:grant-type:apikey" \
  --data-urlencode "response_type=cloud_iam" \
  --data-urlencode "apikey=<apikey>" \
  "https://iam-region2.bluemix.net/identity/token"
```
{: codeblock}

### Risposta:
{: #response2}

```
{
  "access_token": "eyJhbGciOiJIUz......sgrKIi8hdFs",
  "refresh_token": "SPrXw5tBE3......KBQ+luWQVY=",
  "token_type": "Bearer",
  "expires_in": 3600,
  "expiration": 1473188353
}
```
{: codeblock}

**Nota: ** questo token è valido per un'ora e può essere riutilizzato il numero di volte necessario durante il periodo di tempo di un'ora. Si consiglia vivamente di archiviare in cache questo token per evitare di eseguire questa richiesta per ogni accesso al `dashboard_url`.


### Autorizzazione - Passo 2: convalida l'autorizzazione per l'utente all'istanza del servizio (/v2/authz POST)

Ora che hai autenticato l'utente e disponi del tuo token di accesso, dobbiamo convalidare che l'utente sia in grado di accedere al dashboard del servizio. Innanzitutto, ci servono alcune informazioni incluse nel token di accesso dell'utente che decodificheremo nel passo 2.1. Quindi, utilizzeremo tali informazioni per richiamare IAM per verificare se l'utente è autorizzato ad accedere al dashboard nel passo 2.2.

**Passo 2.1**: decodifica il token di accesso dell'utente (restituito durante ` ** Autenticazione - Passo 2: ** Scambia il codice per un token di accesso ` che si trova sopra).
   Si tratta di un token JWT che può essere decodificato utilizzando qualsiasi libreria conforme a JWT. Ad esempio, vedi la libreria inclusa nel nostro [codice broker di esempio](https://github.com/IBM/sample-resource-service-brokers).
   Una volta decodificato il token, il formato è come mostrato di seguito; dovremo estrarre i campi `iam_id` e `scope` che verranno utilizzati nel passo successivo:

```
{
  "iam_id": "IBMid-XXXXXXX",
  "id": "IBMid-XXXXXXX",
  "realmid": "IBMid",
  "identifier": "XXXXXXX",
  "given_name": "Don",
  "family_name": "Quixote",
  "name": "Don Quixote",
  "email": "quixote@email.com",
  "sub": "quixote@email.com",
  "account": {
    "bss": "123123123123123"
  },
  "iat": 1522114004,
  "exp": 1522117604,
  "iss": "https://iam.bluemix.net/identity",
  "grant_type": "urn:ibm:params:oauth:grant-type:apikey",
  "scope": "openid <your serviceName>",
  "client_id": "bx",
  "acr": 1,
  "amr": [
    "pwd"
  ]
}
```

**Passo 2.2 **: richiama IAM per verificare se l'utente è autorizzato ad accedere al dashboard

```
curl -X POST \
  -H "Accept: application/json" \
  -H "Authorization: <token di accesso dal passo 1>" \
  -d '[ \
    { \
      "subject" : \
      { \
        "attributes": \
        { \
          "id": "<valore del campo iam_id dal token dell'utente>", \
          "scope": "<valore del campo scope dal token dell'utente>" \
        } \
      }, \
      "resource" : \
      { \
        "crn" : "<CRN dell'istanza della risorsa>" \
      }, \
      action : <il tuo nome servizio> + ".dashboard.view" \
    } \
  ]' \
  https://iam.bluemix.net/v2/authz
```

Vedi l'esempio nei nostri broker di esempio: https://github.com/IBM/sample-resource-service-brokers

## Definizione dell'ambito dei token {{site.data.keyword.Bluemix_notm}} Identity and Access Management per gli adattatori di terze parti
{: #token_scoping}

I token di accesso utente creati con il tuo ID client possono essere utilizzati solo per accedere alle tue API del servizio. Le richieste ad altre API cloud che utilizzano questo token produrranno un accesso negato, anche se l'utente dispone di una politica appropriata configurata.

Come parte dell'integrazione di terze parti, la definizione dell'ambito del token viene utilizzata per garantire che i token dispongano dell'ambito di accesso minimo necessario per raggiungere gli obiettivi dell'utente. Per facilitare ciò, i token IAM avranno un accesso basato sull'ID client che ha creato il token. Questo significa che, se un token IAM è stato creato da un servizio di terze parti, un utente finale non sarà in grado di eseguire alcune API e funzioni, anche se dispone di una politica appropriata configurata.

L'impatto sulle autorizzazioni (tutte le chiamate a `https://iam.bluemix.net/v2/authz`) è la necessità di trasmettere le informazioni sull'ambito (`scope`) nell'oggetto. Queste informazioni sono contenute all'interno di un token IAM (con codifica base64) nell'attestazione `scope`.

Di seguito è riportato un esempio di ciò che è stato aggiunto nella chiamata di autorizzazione:
```
  [
   {  Intestazioni
   `Authorization` -> un token jwt che rappresenta un servizio di terze parti e/o un dashboard
   `Transaction-ID` -> "un guid univoco ci consente di agevolare la traccia della richiesta end-to-end"
   `Accept` -> `application/vnd.authz.v2+json`
   `Content-Type` -> `application/json`

      Body
      "subject":{
         "attributes":{
            "id":"IBMid-123",
            "scope":"libraryservice openid"
         }
      },
      "action":"libraryservice.books.read",
      "resource":{
         "attributes":{
            "serviceName":"libraryservice",
            "serviceInstance":"12345",
            "accountId":"123456789"
         }
      }
   }
]
```
{: codeblock}

Ciò è applicabile a tutti gli utilizzi (`user, serviceId, crn`) e tutti i `subject.attributes` hanno bisogno di un ambito.

## Passi successivi

Ora è il momento di mettere tutto insieme. Ritorna alla console di gestione delle risorse per pubblicare il tuo servizio in modalità di visibilità limitata e convalidare la tua offerta nel catalogo. Vedi [Pubblicazione e verifica del tuo servizio](/docs/third-party/cis4-rmc-publish.html).
