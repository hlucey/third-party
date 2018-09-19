---


copyright:
  years: 2018
lastupdated: "2018-09-05"


---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:download: .download}

# Schritt 4. Authentifizierungsablauf entwickeln
{: #step4-iam}

Beim Definieren Ihres Angebots haben Sie in der Konsole für das Ressourcenmanagement auf der Seite für das Zugriffsmanagement eine Client-ID und einen geheimen Schlüssel für {{site.data.keyword.Bluemix_notm}} Identity and Access Management (IAM), Ihre Service-ID und Ihren API-Schlüssel erhalten. Nun sind Sie bereit, um mit diesen Werten einen Authentifizierungsablauf zu entwickeln.
{:shortdesc}

## Vorbereitende Schritte
{: #pre-reqs}

Vergewissern Sie sich, dass Sie das [Lernprogramm 'Einführung'](/docs/third-party/index.html) durchgearbeitet haben und über die Genehmigung zur Bereitstellung eines integrierten Abrechnungsservice verfügen.

## IAM-Weiterleitungs-URI ableiten
{: #redirect-uri}

Wenn Sie Ihren Service in der Konsole für das Ressourcenmanagement definieren, dann wird eine Client-ID generiert. Hierbei ist zu beachten, dass zu diesem Zeitpunkt mit hoher Wahrscheinlichkeit kein Weiterleitungs-URI zur Verfügung steht. IAM erstellt eine Client-ID, für die der Wert 'false' festgelegt wurde. Erst nachdem Sie mit dem Weiterleitungs-URI zur Konsole für das Ressourcenmanagement zurückgekehrt sind, verfügen Sie über eine gültige Client-ID.

Im vorherigen Entwicklungsschritt haben Sie einen OSB (Open Service Broker) entwickelt und gehostet. (Sie haben vermutlich IAM-Werte im Beispielcode des Brokers erkannt.) Die Weiterleitungs-URI (`redirect_uri`) stellt normalerweise die Host-URL dar, unter der die App mit einer zusätzlichen URL gespeichert ist, die zur Authentifizierung und Berechtigung verwendet wird.

 In den folgenden Beispielen werden Weiterleitungs-URIs dargestellt:

```
https://myapp.bluemix.net/integrate/auth/callback
http://localhost:3000/auth/callback <-- for testing locally
```

Kehren Sie zur Konsole für das Ressourcenmanagement zurück und fügen Sie den Weiterleitungs-URI zur Registerkarte für IAM hinzu:

1. Melden Sie sich bei der Konsole an.
2. Halten Sie den Weiterleitungs-URI bereit.
3. Kehren Sie zur Konsole für das Ressourcenmanagement zurück.
4. Fügen Sie auf der Registerkarte **IAM** den Weiterleitungs-URI ins Feld **Weiterleitungs-URI** ein.
5. Klicken Sie auf **Client-ID aktualisieren**, um Ihre Client-ID zu aktualisieren.

Nun verfügen Sie über eine Client-ID, die Ihren Weiterleitungs-URI erkennt und auf den Wert 'true' gesetzt ist. Mit dieser Client-ID können Sie in den nachfolgenden Schritten Ihren OAuth-Ablauf entwickeln.

## OAuth-Ablauf für die Authentifizierung entwickeln
{: #oauth}


**Authentifizierung - Schritt 0:** Suchen Sie den regionalen IAM-Endpunkt für die Anmeldung an der Benutzerschnittstelle, der sich näher an der von Ihnen bereitgestellten Anwendung befindet. Rufen Sie hierzu `https://iam.bluemix.net/identity/.well-known/openid-configuration` auf.

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

Diese Anforderung kann einmalig ausgeführt werden, wenn die Anwendung gestartet wird. Anschließend kann sie erneut ausgeführt werden, wenn der Berechtigungsendpunkt (`authorization_endpoint`) fehlschlägt. Der Wert für `authorization_endpoint` kann für kurze Zeit im Cache zwischengespeichert werden. Er kann nach Ablauf des Caches oder Auftreten eines Fehlers aktualisiert werden.


**Authentifizierung - Schritt 1:** Navigiert ein Benutzer zu Ihrer Dashboard-URL (`dashboard_url`), dann wird der Browser zu `<authorization_endpoint>?client_id=<your-client-id>&redirect_uri=<your-redirect-uri>&response-type=code&state=<your-resource-instance-id>` weitergeleitet.


-> Der Anmeldedialog wird angezeigt.

-> Der Benutzer gibt die Berechtigungsnachweise ein.

-> Der Browser führt einen Callback an den Weiterleitungs-URI durch und stellt einen Antwortparameter "code" und einen Wert für "state" zur Verfügung.


**Authentifizierung - Schritt 2:** Code für Aufruf eines Zugriffstokens austauschen

### POST <token_endpoint>
{: #post}

#### Header:
{: #headers1}

  - Authorization: Basic *[client id]:[client secret]*
  - Content-Type: application/x-www-form-urlencoded
  - Accept: application/json

#### Mit Parametern:
{: #parameters1}

  - client_id=*[client id]*
  - client_secret=*[client secret]*
  - grant_type=authorization_code
  - response_type=cloud_iam
  - redirect_uri=*[same URI as redirect_uri from step 1]*
  - code=*[code from callback]*

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

### Antwort:
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

  Vergewissern Sie sich, dass das Zugriffstoken (access_token) des Benutzers, das in dieser Antwort zurückgegeben wurde, gespeichert wird. Es wird bei der nachfolgenden Benutzerberechtigung benötigt.

Informationen zu diesem Thema finden Sie in den Beispielbrokern: https://github.com/IBM/sample-resource-service-brokers

## Benutzerberechtigung validieren
{: #validate}

1. Mit IAM kommunizieren, um ein Zugriffstoken für einen API-Schlüssel anzufordern.
2. Berechtigung des Benutzers für die Serviceinstanz validieren (/v2/authz POST).

### Berechtigung - Schritt 1: {{site.data.keyword.Bluemix_notm}}-IAM-Token mit einem API-Schlüssel abrufen
{: #iam_token_using_api_key}

### POST /identity/token

#### Header:
{: #headers2}

  - Authorization: Basic *[client id]:[client secret]*
  - Content-Type: application/x-www-form-urlencoded
  - Accept: application/json

#### Mit Parametern:
{: #parameters2}

  - grant_type=urn:ibm:params:oauth:grant-type:apikey
  - response_type=cloud_iam
  - apikey=*[Api key]*

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

### Antwort:
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

**Hinweis:** Dieses Token besitzt eine Gültigkeitszeitdauer von einer Stunde und kann innerhalb des einstündigen Zeitrahmens beliebig oft wiederverwendet werden. Es wird dringend empfohlen, dieses Token im Cache zwischenzuspeichern, um zu vermeiden, dass diese Anforderung bei jedem Zugriff auf die Dashboard-URL (`dashboard_url`) wiederholt werden muss.


### Berechtigung - Schritt 2: Berechtigung des Benutzers für die Serviceinstanz validieren (/v2/authz POST)
{: #step-2-authorization}

Nach der Authentifizierung des Benutzers und der Erstellung eines eigenen Zugriffstokens muss überprüft werden, ob der Benutzer auf das Service-Dashboard zugreifen kann. Zuerst müssen bestimmte Informationen, die im Zugriffstoken des Benutzers gespeichert sind, abgerufen werden. Diese Informationen werden in Schritt 2.1 entschlüsselt. Anschließend werden diese Informationen zum Aufrufen von IAM verwendet. Auf diese Weise kann geprüft werden, ob der Benutzer für den Zugriff auf das Dashboard (Schritt 2.2) berechtigt ist.

**Schritt 2.1**: Zugriffstoken des Benutzers entschlüsseln (Rückgabe während `**Authentifizierung - Schritt 2:** Code eines Zugriffstokens austauschen ` oben.)
   Das Zugriffstoken ist ein JWT-Token, das mit einer beliebigen JWT-kompatiblen Bibliothek entschlüsselt werden kann. Siehe hierzu die im [Beispielcode für den Broker](https://github.com/IBM/sample-resource-service-brokers) enthaltene Bibliothek.
   Nach der Entschlüsselung des Tokens wird das folgende Format angezeigt. Sie müssen nun die Werte der Felder `iam_id` und `scope` extrahieren, die im nächsten Schritt verwendet werden:

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

**Schritt 2.2**: IAM aufrufen, um Berechtigung des Benutzers für den Dashboardzugriff zu überprüfen

```
curl -X POST \
  -H "Accept: application/json" \
  -H "Authorization: <access token from step 1>" \
  -d '[ \
    { \
      "subject" : \
      { \
        "attributes": \
        { \
          "id": "<iam_id field value from user's token>", \
          "scope": "<scope field value from user's token>" \
        } \
      }, \
      "resource" : \
      { \
        "crn" : "<resource instance CRN>" \
      }, \
      action : <your service name> + ".dashboard.view" \
    } \
  ]' \
  https://iam.bluemix.net/v2/authz
```

Informationen zu diesem Thema finden Sie in den Beispielbrokern: https://github.com/IBM/sample-resource-service-brokers

## IAM-Token-Scoping für Adopter anderer Anbieter
{: #token_scoping}

Die mit Ihrer Clent-ID erstellten Benutzerzugriffstokens können nur für den Zugriff auf Ihre Service-APIs verwendet werden. Mit diesem Token ausgeführte Anforderungen an andere Cloud-APIs führen zur Zugriffsverweigerung. Dies gilt auch dann, wenn für den Benutzer eine entsprechende Richtlinie konfiguriert wurde.

Im Rahmen der Drittanbieterintegration wird das Token-Scoping verwendet, um sicherzustellen, dass die Token über den mindestens erforderlichen Zugriffsbereich verfügen, um die Benutzerziele erreichen zu können. Hierzu erhalten IAM-Tokens den Zugriff auf Basis der Client-ID, mit der das Token erstellt wurde. Wurde ein IAM-Token mit einem Service eines anderen Anbieters erstellt, dann ist ein Endbenutzer nicht in der Lage, bestimmte APIs und Funktionen auszuführen. Dies gilt auch dann, wenn für den Benutzer eine entsprechende Richtlinie konfiguriert wurde.

Die Auswirkungen auf die Berechtigungen (alle Aufrufe an `https://iam.bluemix.net/v2/authz`) bestehen darin, dass die Bereichsinformationen (`scope`) im Betreff übergeben werden müssen. Diese Informationen sind in einem IAM-Token (Base64-Codierung) im Claim `scope` enthalten.

Im folgenden Abschnitt wird dargestellt, welche Elemente im Berechtigungsaufruf hinzugefügt werden:
```
  [
   {  Headers
   `Authorization` -> a jwt token representing a 3rd party service and/or dashboard
   `Transaction-ID` -> "a unique guid lets us help trace the request end to end"
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

Dies gilt für alle Verwendungen (`user, serviceId, crn`). Für alle Vorkommen von `subject.attributes` wird ein Bereich benötigt.

## Nächste Schritte
{: #next-steps}

Nun müssen alle erarbeiteten Erkenntnisse in Beziehung zueinander gesetzt werden. Rufen Sie erneut die Konsole für das Ressourcenmanagement auf, um Ihren Service im Modus für die eingeschränkte Sichtbarkeit zu veröffentlichen, und überprüfen Sie Ihr Angebot im Katalog. Siehe hierzu: [Eigenen Service veröffentlichen und testen](/docs/third-party/cis4-rmc-publish.html).
