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

# Etapa 4: desenvolvendo um fluxo de autenticação

Quando você definiu sua oferta, o console de gerenciamento de recurso - página **Gerenciamento de acesso** forneceu seu ID de cliente e Segredo do {{site.data.keyword.Bluemix_notm}} Identity and Access Management (IAM), o ID do serviço e a chave API. Agora, é hora de usar esses valores para concluir as etapas a seguir:

1. Derive seu URI de redirecionamento com base na manipulação de seu `dashboard_url`, retorne para o console de gerenciamento de recurso e inclua-o na guia IAM, assegurando a atualização do ID de cliente.
2. Desenvolva o fluxo OAuth para autenticação. Você usará seus URIs de redirecionamento, o ID de cliente e o segredo do cliente como parâmetros para as APIs de REST do IAM `token_endpoint` para concluir esse fluxo.
3. Valide a autorização do usuário:
   1. Comunique-se com o IAM para obter um token de acesso de sua chave API
   2. Valide a autorização para o usuário para o painel de serviço usando o `authorization_endpoint` (/v2/authz POST)

Esta etapa supõe que você tenha sido aprovado para entregar um serviço de Faturamento integrado. Se você ainda não concluiu o registro e a aprovação iniciais no PWB, veja: [Introdução à publicação de sua oferta de terceiros no {{site.data.keyword.Bluemix_notm}}](/docs/third-party/index.html)
{: tip}

## Antes de começar

Assegure-se de ter iniciado a etapa 1 e concluído as etapas 2 e 3:
1. [ Anúncios de serviço de autor e anúncio de marketing ](/docs/third-party/cis1-docs-marketing.html).
2. [Defina sua oferta no console de gerenciamento de recurso](/docs/third-party/cis2-rmc-define.html).
3. [ Desenvolva e hospeda seus brokers de serviço ](/docs/third-party/cis3-broker.html).


## Derivar o URI de redirecionamento do IAM (console de gerenciamento de recurso: página do IAM)

Quando você definiu o seu serviço no console de gerenciamento de recurso, gerou um ID de cliente, mas observe que provavelmente não tinha um URI de redirecionamento no momento. Isso significa que o IAM criou um ID de cliente que está configurado para false. Até que retorne para o console de gerenciamento de recurso com seu URI de redirecionamento, você não terá um ID de cliente verdadeiro.

A boa notícia é que na etapa de desenvolvimento anterior, você desenvolveu um OSB e hospedou-o (você provavelmente viu valores do IAM no código do broker de amostra). O `redirect_uri` é geralmente a URL do host na qual o app reside com alguma URL adicional que manipulará a autenticação/autorização.

 Aqui estão alguns exemplos de URIs de redirecionamento

```
https://myapp.bluemix.net/integrate/auth/callback
http://localhost:3000/auth/callback <-- para testar localmente
```

Retorne para o console de gerenciamento de recursos e inclua o URI de redirecionamento na guia IAM:

1. Conecte-se ao console
2. Capture seu URI de redirecionamento
3. Retorne para o console de gerenciamento de recurso
4. Na **guia IAM**, cole seu URI de redirecionamento no campo **URI de redirecionamento**.
5. Clique em **Atualizar ID de cliente** para atualizar seu ID de cliente.

Agora é necessário ter um ID de cliente que entenda seu URI de redirecionamento e esteja configurado como true! É possível usar esse ID de cliente nas próximas etapas para desenvolver o seu fluxo OAuth.

## Desenvolva seu fluxo OAuth para autenticação
{: #oauth}


**Autenticação - Etapa 0:** localize o terminal regional do IAM para login da IU mais próximo de seu aplicativo implementado chamando `https://iam.bluemix.net/identity/.well-known/openid-configuration`.

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

Essa solicitação poderá ser feita uma vez quando o aplicativo for iniciado e novamente se o `authorization_endpoint` falhar. Será necessário armazenar em cache o valor `authorization_endpoint` por um curto período de tempo e atualizar após o cache expirar ou um erro ser encontrado.


**Autenticação - Etapa 1:** quando um usuário navegar para o seu `dashboard_url`, redirecione o navegador para `<authorization_endpoint>?client_id=<your-client-id>&redirect_uri=<your-redirect-uri>&response-type=code&state=<your-resource-instance-id>`


-> o prompt de login será mostrado

-> O usuário insere credenciais

-> retorno de chamada de navegador para redirecionar o URI fornecendo um parâmetro de resposta "code" e um valor "state"


**Autenticação - Etapa 2:** troque o código para uma chamada de token de acesso

### POST <token_endpoint>

#### Cabeçalhos:
  - Autorização: básica *[client id]:[client segredo]*
  - Content-Type: application/x-www-form-urlencoded
  - Accept: application/json

#### Com parâmetros:
  - client_id=*[ID de cliente]*
  - client_secret=*[segredo do cliente]*
  - grant_type=authorization_code
  - response_type=cloud_iam
  - redirect_uri=*[mesmo URI que redirect_uri da etapa 1]*
  - code=*[código de retorno de chamada]*

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

### Resposta:

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

  Certifique-se de armazenar o access_token do usuário retornado nessa resposta, pois ele será usado durante a autorização do usuário em seguida.

Veja o exemplo em nossos brokers de amostra: https://github.com/IBM/sample-resource-service-brokers

## Agora é hora de validar a autorização do usuário
{: #validate}

1. Comunique-se com o IAM para obter um token de acesso para uma chave API
2. Valide a autorização para o usuário para a instância de serviço (/v2/authz POST)

### Autorização - Etapa 1: obter um token do {{site.data.keyword.Bluemix_notm}} IAM usando uma chave API.
{: #iam_token_using_api_key}

### POST /identity/token

#### Cabeçalhos:
  - Autorização: básica *[client id]:[client segredo]*
  - Content-Type: application/x-www-form-urlencoded
  - Accept: application/json

#### Com parâmetros:
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

### Resposta:

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

**Nota:** esse token é válido por uma hora e pode ser reutilizado quantas vezes forem necessárias durante o prazo de uma hora. É altamente recomendado que esse token seja armazenado em cache para evitar fazer essa solicitação para cada acesso ao `dashboard_url`.


### Autorização - Etapa 2: validar a autorização para o usuário para a instância de serviço (/v2/authz POST)

Agora que nós autenticamos o usuário e temos nosso próprio token de acesso, precisamos validar que o usuário tem a capacidade de acessar o painel de serviço. Em primeiro lugar, precisaremos de algumas informações incluídas no token de acesso do usuário, que vamos decodificar na etapa 2.1. Em seguida, usaremos essas informações para chamar o IAM para verificar se o usuário está autorizado a acessar o painel na etapa 2.2.

**Etapa 2.1**: decodifique o token de acesso do usuário (retornado durante `**Authentication - Step 2:** Exchange the code for an access token` localizado acima.)
   Esse é um token JWT que pode ser decodificado usando a biblioteca compatível com JWT. Por exemplo, veja a biblioteca incluída em nosso [código do broker de amostra](https://github.com/IBM/sample-resource-service-brokers).
   Depois que o token é decodificado, o formato é conforme mostrado a seguir; precisaremos extrair os campos `iam_id` e `scope` que serão usados na próxima etapa:

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

**Etapa 2.2**: chamar o IAM para verificar se o usuário está autorizado a acessar o painel

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

Veja o exemplo em nossos brokers de amostra: https://github.com/IBM/sample-resource-service-brokers

## Definição de escopo do token do {{site.data.keyword.Bluemix_notm}} Identity and Access Management para adotantes de terceiros
{: #token_scoping}

Os tokens de acesso de usuário criados com seu ID de cliente podem ser usados somente para acessar suas APIs de serviço. As solicitações para outras APIs de nuvem que usam esse token resultarão no acesso negado, mesmo se o usuário tiver uma política apropriada configurada.

Como parte da integração de terceiros, a definição de escopo do token está sendo usada para assegurar que os tokens tenham o escopo de acesso mínimo necessário para cumprir os objetivos do usuário. Para facilitar isso, os tokens do IAM terão acesso com base no ID de cliente que criou o token. Isso significa que, se um token do IAM foi criado por um serviço de terceiro, um usuário final não será capaz de executar determinadas APIs e funções, mesmo se o usuário tiver uma política apropriada configurada.

O impacto em autorizações (todas as chamadas para `https://iam.bluemix.net/v2/authz`) é a necessidade de passar informações de `scope` no assunto. Essas informações estão contidas em um token do IAM (codificado em base64) na solicitação de `scope`.

Aqui está um exemplo do que foi incluído na chamada de autorização:
```
  [
   {
   `Authorization` -> a jwt token representing a 3rd party service and/or dashboard
   `Transaction-ID` -> "a unique guid lets us help trace the request end to end"
   ` Accept `-> `application/vnd.authz.v2 + json `
   ` Content-Type `-> ` application/json `

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

Isso é aplicável a todos os usos (`user, serviceId, crn`) e todos os `subject.attributes` precisam de um escopo.

## Próximas Etapas

Agora é hora de reunir tudo! Retorne para o console de gerenciamento de recurso para publicar seu serviço em visibilidade limitada e validar sua oferta no catálogo. Veja: [Publicando e testando seu serviço](/docs/third-party/cis4-rmc-publish.html).
