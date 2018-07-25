---


copyright:
  years: 2018
lastupdated: "2018-06-22"


---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:download: .download}

# Etape 4 : Développement d'un flux d'authentification

Une fois que vous avez défini votre offre, la page **Access Management** de la console de gestion des ressources inclut votre ID client et votre valeur confidentielle {{site.data.keyword.Bluemix_notm}} Identity and Access Management (IAM), votre ID de service et votre clé d'API. Il est temps maintenant d'utiliser ces valeurs pour effectuer la procédure suivante :

1. Dérivez votre URI de redirection en fonction du traitement de votre élément `dashboard_url`, accédez à nouveau à la console de gestion des ressources et ajoutez-le dans l'onglet IAM en vous assurant d'avoir mis à jour votre ID client.
2. Développez le flux OAuth pour l'authentification. Vous allez utiliser votre ou vos URI de redirection, votre ID client, et votre valeur confidentielle du client en tant que paramètres des API Rest IAM `token_endpoint` pour finaliser ce flux.
3. Validez l'autorisation utilisateur :
   1. Communiquez avec IAM afin d'obtenir un jeton d'accès à partir de votre clé d'API
   2. Validez l'autorisation concernant le tableau de bord de service en utilisant l'élément `authorization_endpoint` pour l'utilisateur (/v2/authz POST)

Cette étape suppose que vous disposez de l'approbation permettant de fournir un service de facturation intégrée. Si vous n'avez pas encore effectué le processus d'enregistrement et d'approbation dans PWB, voir la section présentant comment [commencer à publier votre offre de tiers dans {{site.data.keyword.Bluemix_notm}}](/docs/third-party/index.html)
{: tip}

## Avant de commencer

Vérifiez que vous avez commencé l'étape 1 et avez terminé les étapes 2 et 3 :
1. [Création de documents de service et d'annonce marketing](/docs/third-party/cis1-docs-marketing.html).
2. [Définition de votre offre dans la console de gestion des ressources](/docs/third-party/cis2-rmc-define.html).
3. [Développement et hébergement de vos courtiers de services](/docs/third-party/cis3-broker.html).


## Dérivez votre URI de redirection IAM (console de gestion des ressources : page IAM)

Lorsque vous avez défini votre service dans la console de gestion des ressources, vous avez généré un ID client mais il est fort probable que vous ne disposiez pas d'un URI de redirection à ce moment là. Autrement dit, IAM a créé un ID client ayant la valeur false. Tant que vous n'accédez pas à la console de gestion des ressources avec votre URI de redirection, l'ID client n'a pas la valeur true.

Lors de l'étape de développement précédente, vous avez développé un courtier OSB et l'avez hébergé (vous avez sans doute vu des valeurs IAM dans le code de courtier exemple). L'élément `redirect_uri` est généralement l'URL de l'hôte dans laquelle se trouve l'application avec une URL supplémentaire qui traite l'authentification/l'autorisation.

 Voici quelques exemples d'URI de redirection

```
https://myapp.bluemix.net/integrate/auth/callback
http://localhost:3000/auth/callback <-- for testing locally
```

Accédez à nouveau à la console de gestion des ressources et ajoutez votre URI de redirection à l'onglet IAM :

1. Connectez-vous à la console
2. Notez votre URI de redirection
3. Accédez à nouveau à la console de gestion des ressources
4. Dans l'onglet **IAM**, collez votre URI de redirection dans la zone **Redirect URI**.
5. Cliquez sur **Update Client ID** pour mettre à jour votre ID client.

Vous devez maintenant avoir un ID client qui prend en compte votre URI de redirection et qui a la valeur true. Vous pouvez utiliser cet ID client dans la procédure suivante pour développer votre flux OAuth.

## Développez votre flux OAuth pour authentification
{: #oauth}


**Authentification - Etape 0 :** Recherchez un noeud final régional IAM pour la connexion d'interface utilisateur proche de votre application déployée en appelant `https://iam.bluemix.net/identity/.well-known/openid-configuration`.

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

Cette demande peut être effectuée une fois lorsque l'application est démarrée et une nouvelle fois en cas de défaillance d'`authorization_endpoint`. Vous devez pouvoir mettre en cache la valeur `authorization_endpoint` pendant une courte période et effectuer l'actualisation après l'expiration du cache ou une erreur est générée.


**Authentification - Etape 1 :** Lorsqu'un utilisateur accède à votre adresse `dashboard_url`, redirigez-le vers `<authorization_endpoint>?client_id=<your-client-id>&redirect_uri=<your-redirect-uri>&response-type=code&state=<your-resource-instance-id>`


-> L'invite de connexion s'affiche

-> L'utilisateur entre les données d'identification

-> Rappel du navigateur pour rediriger l'URI fournissant un paramètre de réponse "code" et une valeur "state"


**Authentification - Etape 2 :** Echangez le code pour un appel de jeton d'accès

### POST <token_endpoint>

#### En-têtes :
  - Authorization: Basic *[client id]:[client secret]*
  - Content-Type: application/x-www-form-urlencoded
  - Accept: application/json

#### Avec les paramètres :
  - client_id=*[client id]*
  - client_secret=*[client secret]*
  - grant_type=authorization_code
  - response_type=cloud_iam
  - redirect_uri=*[same uri as redirect_uri from step 1]*
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

### Réponse :

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

  Assurez-vous de stocker le jeton d'accès (access_token) de l'utilisateur renvoyé dans cette réponse car il sera utilisé lors de l'autorisation utilisateur suivante.

Consultez l'exemple souhaité sur la page suivante : https://github.com/IBM/sample-resource-service-brokers 

## Il est temps maintenant de valider l'autorisation utilisateur
{: #validate}

1. Communiquez avec IAM afin d'obtenir un jeton d'accès pour une clé d'API
2. Validez l'autorisation concernant l'instance de service pour l'utilisateur (/v2/authz POST)

### Autorisation - Etape 1 : Obtention d'un jeton IAM {{site.data.keyword.Bluemix_notm}} en utilisant une clé d'API.
{: #iam_token_using_api_key}

### POST /identity/token

#### En-têtes :
  - Authorization: Basic *[client id]:[client secret]*
  - Content-Type: application/x-www-form-urlencoded
  - Accept: application/json

#### Avec les paramètres :
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

### Réponse :

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

**Remarque :** Ce jeton est valide pendant une heure et peut être réutilisé autant de fois que nécessaire pendant cette période. Il est fortement recommandé de mettre en cache ce jeton afin d'éviter d'effectuer cette demande pour chaque accès à l'élément `dashboard_url`.


### Autorisation - Etape 2 : Validez l'autorisation concernant l'instance de service pour l'utilisateur (/v2/authz POST)

Maintenant que nous avons authentifié l'utilisateur et que nous disposons de notre propre jeton d'accès, nous devons valider le fait que l'utilisateur peut accéder au tableau de bord de service. Nous allons tout d'abord avoir besoin d'informations incluses dans le jeton d'accès de l'utilisateur que nous allons décoder lors de l'étape 2.1. Nous allons ensuite utiliser ces informations pour appeler IAM afin de vérifier si l'utilisateur est autorisé à accéder au tableau de bord à l'étape 2.2.

**Etape 2.1** : Décodez le jeton d'accès de l'utilisateur (renvoyé lors de l'étape `**Authentification - Etape 2 :** Echangez le code pour un appel de jeton d'accès`.)
   Il s'agit d'un jeton JWT pouvant être décodé en utilisant toute bibliothèque compatible JWT. Par exemple, voir la bibliothèque incluse dans notre [code de courtier exemple](https://github.com/IBM/sample-resource-service-brokers).
   Une fois que le jeton est décodé, le format s'affiche, comme présenté ci-dessous. Nous devons extraire les zones `iam_id` et `scope` qui seront utilisées dans l'étape suivante :

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

**Etape 2.2** : Appelez IAM pour vérifier que l'utilisateur est autorisé à accéder au tableau de bord

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

Consultez l'exemple souhaité sur la page suivante : https://github.com/IBM/sample-resource-service-brokers

## Portée des jetons {{site.data.keyword.Bluemix_notm}} Identity and Access Management pour les utilisateurs tiers
{: #token_scoping}

Les jetons d'accès utilisateur créés avec votre ID client peuvent uniquement être utilisés pour accéder à vos API de service. L'accès sera refusé pour les demandes effectuées auprès d'autres API de cloud utilisant ce jeton même si la règle appropriée est configurée pour l'utilisateur.

Lors de l'intégration de tiers, la portée de jeton est utilisée afin de vérifier que les jetons disposent de la portée d'accès minimale pour atteindre les objectifs de l'utilisateur. Pour faciliter cela, les jetons IAM disposent d'un accès en fonction de l'ID client ayant créé le jeton. Cela signifie que si un jeton IAM a été créé par un service tiers, un utilisateur final ne pourra pas exécuter certaines API et fonctions même si une règle appropriée est configurée pour l'utilisateur.

L'impact sur les autorisations (tous les appels de `https://iam.bluemix.net/v2/authz`) est le suivant : il est nécessaire de transmettre des informations de `portée` dans le sujet. Ces informations se trouvent dans un jeton IAM (code base64) dans la demande de `portée`.

Voici un exemple d'ajout dans l'appel d'autorisation :
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

S'applique à toutes les utilisations (`utilisateur, ID de service, nom de ressource de cloud`) et tous les éléments `subject.attributes` ont besoin d'une portée.

## Etapes suivantes

Il est temps maintenant de rassembler tous les éléments ! Accédez à nouveau à la console de gestion des ressources pour publier votre service en mode de visibilité limitée et valider votre offre dans le catalogue. Voir [Publication et test de votre service](/docs/third-party/cis4-rmc-publish.html).
