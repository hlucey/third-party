---


copyright:
  years: 2018
lastupdated: "2018-08-28"


---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:download: .download}

# Passo 4. Sviluppa un flusso di autenticazione
{: #step4-iam}

Quando definisci la tua offerta, la pagina Access Manage della console di gestione delle risorse elenca i tuoi segreto e ID client, il tuo ID servizio e la tua chiave API di {{site.data.keyword.Bluemix_notm}} Identity and Access Management (IAM). Ora sei pronto per utilizzare questi valori per sviluppare un flusso di autenticazione.
{:shortdesc}

## Prima di iniziare
{: #pre-reqs}

Assicurati di aver completato l'[esercitazione introduttiva](/docs/third-party/index.html) e di aver ricevuto l'approvazione a distribuire un servizio di fatturazione integrato.

## Ricava l'URI di reindirizzamento IAM 
{: #redirect-uri}

Quando definisci il tuo servizio nella console di gestione delle risorse, generi un ID client, ma è probabile che in quel momento non disponevi di un URI di reindirizzamento. Un ID client che è impostato su false viene creato da IAM. Finché non ritorni alla console di gestione delle risorse con il tuo URI di reindirizzamento, non avrai un vero ID client.

La buona notizia è che nel passo di sviluppo precedente hai sviluppato un OSB e lo hai ospitato (hai probabilmente viso i valori IAM nel codice broker di esempio). Il `redirect_uri` è di norma l'url host dove risiede l'applicazione con qualche url aggiuntivo che può gestire l'autenticazione/autorizzazione.

 I seguenti esempi mostrano gli URI di reindirizzamento:

```
https://myapp.bluemix.net/integrate/auth/callback
http://localhost:3000/auth/callback <-- per l'esecuzione di test in locale
```

Ritorna alla console di gestione delle risorse e aggiungi il tuo URI di reindirizzamento alla scheda IAM.

1. Accedi alla console.
2. Prendi l'URI di reindirizzamento.
3. Ritorna alla console di gestione delle risorse.
4. Dalla **scheda IAM**, incolla il tuo URI di reindirizzamento nel campo **Redirect URI**.
5. Fai clic su **Update Client ID** per aggiornare il tuo ID client.

Hai ora un ID client che capisce il tuo URI di reindirizzamento ed è impostato su true. Puoi utilizzare tale ID client nei passi successivi per sviluppare il tuo flusso OAuth.

## Sviluppa il tuo flusso OAuth per l'autenticazione
{: #oauth}


**Autenticazione - Passo 0:** trova l'endpoint regionale IAM per l'accesso all'IU più vicina alla tua applicazione distribuita richiamando `https://iam.bluemix.net/identity/.well-known/openid-configuration`.

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

Questa richiesta può essere eseguita dopo che l'applicazione è stata avvitata e nuovamente se si verifica un malfunzionamento dell'`authorization_endpoint`. Sei ora in grado di archiviare nella cache il valore `authorization_endpoint` per un breve periodo di tempo ed eseguire l'aggiornamento dopo la scadenza della cache o il riscontro di un errore.


**Autenticazione - Passo 1:** quando un utente accede al tuo `dashboard_url`, reindirizza il browser a `<authorization_endpoint>?client_id=<your-client-id>&redirect_uri=<your-redirect-uri>&response-type=code&state=<your-resource-instance-id>`


-> viene visualizzato il prompt di accesso

-> l'utente immette le credenziali

-> callback del browser all'URI di reindirizzamento che fornisce un parametro di risposta "code" e un valore "state"


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
  - redirect_uri=*[stesso URI come il redirect_uri dal passo 1]*
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

  Assicurati di archiviare l'access_token dell'utente restituito in questa risposta poiché viene utilizzato successivamente durante l'autorizzazione dell'utente.

Vedi l'esempio nei nostri broker di esempio: https://github.com/IBM/sample-resource-service-brokers

## Ora è il momento di convalidare l'autorizzazione utente
{: #validate}

1. Comunica con IAM per ottenere un token di accesso per una chiave API.
2. Convalida l'autorizzazione per l'utente all'istanza del servizio (/v2/authz POST).

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

**Nota: ** questo token è valido per un'ora e può essere riutilizzato il numero di volte necessario durante il periodo di tempo di un'ora. Si consiglia vivamente di memorizzare nella cache questo token per evitare di eseguire questa richiesta per ogni accesso al `dashboard_url`.


### Autorizzazione - Passo 2: convalida l'autorizzazione per l'utente all'istanza del servizio (/v2/authz POST)

Ora che hai autenticato l'utente e disponi del tuo token di accesso, devi convalidare che l'utente sia in grado di accedere al dashboard del servizio. Innanzitutto, ti servono alcune informazioni incluse nel token di accesso dell'utente che decodifichi nel passo 2.1. Quindi, utilizza tali informazioni per richiamare IAM per verificare se l'utente è autorizzato ad accedere al dashboard nel passo 2.2.

**Passo 2.1**: decodifica il token di accesso dell'utente (restituito durante `**Autenticazione - Passo 2:** Scambia il codice per un token di accesso ` che si trovano nella precedente sezione).
   Il token di accesso è un token JWT che può essere decodificato utilizzando una qualsiasi libreria conforme a JWT. Ad esempio, vedi la libreria inclusa nel nostro [codice broker di esempio](https://github.com/IBM/sample-resource-service-brokers).
   Dopo che il token è stato decodificato, il formato è quello mostrato nella seguente sezione; estrai i campi `iam_id` e `scope`, che vengono utilizzati nel passo successivo:

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

## Ambito del token IAM per utenti di terze parti
{: #token_scoping}

I token di accesso utente creati con il tuo ID client possono essere utilizzati solo per accedere alle tue API del servizio. Le richieste ad altre API cloud che utilizzano questo token producono un accesso negato, anche se l'utente dispone di una politica appropriata configurata.

Come parte dell'integrazione di terze parti, la definizione dell'ambito del token viene utilizzata per garantire che i token dispongano dell'ambito di accesso minimo necessario per raggiungere gli obiettivi dell'utente. Per facilitare ciò, i token IAM hanno un accesso basato sull'ID client che ha creato il token. Se un token IAM è stato creato da un servizio di terze parti, un utente finale non può eseguire alcune API e funzioni, anche se dispone di una politica appropriata configurata.

L'impatto sulle autorizzazioni (tutte le chiamate a `https://iam.bluemix.net/v2/authz`) è la necessità di trasmettere le informazioni sull'ambito (`scope`) nell'oggetto. Queste informazioni sono contenute all'interno di un token IAM (con codifica base64) nell'attestazione `scope`.

La seguente sezione è un esempio di cosa viene aggiunto nella chiamata di autorizzazione:
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
{: #next-steps}

Ora è il momento di mettere tutto insieme. Ritorna alla console di gestione delle risorse per pubblicare il tuo servizio in modalità di visibilità limitata e convalidare la tua offerta nel catalogo. Vedi [Pubblicazione e verifica del tuo servizio](/docs/third-party/cis4-rmc-publish.html).
