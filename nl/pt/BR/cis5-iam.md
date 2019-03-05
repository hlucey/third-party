---


copyright:
  years: 2018, 2019
lastupdated: "2019-01-04"


---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:download: .download}

# Etapa 4. Desenvolvendo um fluxo de autenticação
{: #step4-iam}

Ao definir a oferta, a página Gerenciar acesso no console de gerenciamento de recursos lista o identificador de cliente e o segredo, o ID do serviço e a chave API do Identity and Access Management (IAM) do {{site.data.keyword.Bluemix_notm}}. Agora você está pronto para usar esses valores para desenvolver um fluxo de autenticação.
{:shortdesc}

## Antes de começar
{: #pre-reqs}

Certifique-se de ter concluído o [tutorial de introdução](/docs/third-party/index.html) e que esteja aprovado para entregar um serviço de faturamento integrado.

## Derive o URI de redirecionamento do IAM
{: #redirect-uri}

Ao definir o serviço no console de gerenciamento de recurso, um identificador de cliente é gerado, mas observe que provavelmente você não tem um URI de redirecionamento no momento. Um identificador de cliente configurado como false é criado pelo IAM. Até você retornar ao console de gerenciamento de recurso com o URI de redirecionamento, não terá um identificador de cliente true.

A boa notícia é que na etapa de desenvolvimento anterior, você desenvolveu um OSB e hospedou-o (você provavelmente viu valores do IAM no código do broker de amostra). O `redirect_uri` é geralmente a URL do host em que o app reside com alguma URL adicional que pode manipular a autenticação/autorização.

 Os exemplos a seguir mostram URIs redirecionarem:

```
https://<myapp>.cloud.ibm.com/integrate/auth/callback
http://localhost:3000/auth/callback <-- for testing locally
```

Retorne para o console de gerenciamento de recursos e inclua o URI de redirecionamento na guia IAM:

1. Efetue sign in no console.
2. Agarre seu URI de redirecionamento.
3. Retorne para o console de gerenciamento de recursos.
4. Na **guia IAM**, cole seu URI de redirecionamento no campo **URI de redirecionamento**.
5. Clique em **Atualizar ID de cliente** para atualizar seu ID de cliente.

Agora você tem um identificador de cliente que entende o URI de redirecionamento e que está configurado como true! É possível usar esse ID de cliente nas próximas etapas para desenvolver o seu fluxo OAuth.

## Desenvolva seu fluxo OAuth para autenticação
{: #oauth}


**Autenticação - Etapa 0:** localize o terminal regional do IAM para login da IU mais próximo de seu aplicativo implementado chamando `https://iam.cloud.ibm.com/identity/.well-known/openid-configuration`.

```
curl -X GET \
  https://iam.cloud.ibm.com/identity/.well-known/openid-configuration
```

```
HTTP/1.1 200 OK
Content-Type: application/json
{
  "issuer": "https://iam.cloud.ibm.com/identity",
  "authorization_endpoint": "https://iam-region2.cloud.ibm.com/identity/authorize",
  "token_endpoint": "https://iam-region2.cloud.ibm.com/identity/token",
...
}
```

Essa solicitação poderá ser feita uma vez quando o aplicativo for iniciado e novamente se o `authorization_endpoint` falhar. Agora você é capaz de armazenar em cache o valor `authorization_endpoint` por um curto período de tempo e atualizar após a expiração do cache ou a localização de um erro.


**Autenticação - Etapa 1:** quando um usuário navegar para o seu `dashboard_url`, redirecione o navegador para `<authorization_endpoint>?client_id=<your-client-id>&redirect_uri=<your-redirect-uri>&response-type=code&state=<your-resource-instance-id>`


-> o prompt de login é mostrado

-> O usuário insere credenciais

-> retorno de chamada do navegador para redirecionar o URI fornecendo um parâmetro de resposta "code" e um valor "state"


**Autenticação - Etapa 2:** troque o código para uma chamada de token de acesso

### POST <token_endpoint>
{: #post}

#### Cabeçalhos:
{: #headers1}

  - Autorização: básica *[client id]:[client secret]*
  - Content-Type: application/x-www-form-urlencoded
  - Accept: application/json

#### Com parâmetros:
{: #parameters1}

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
  "https://iam-region2.cloud.ibm.com/identity/token"
```
{: codeblock}

### Resposta:
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

  Certifique-se de armazenar o access_token do usuário retornado nessa resposta, pois ele será usado durante a autorização do usuário em seguida.

Consulte o exemplo em nossos [brokers de amostra](https://github.com/IBM/sample-resource-service-brokers){: new_window} ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo").

## Agora é hora de validar a autorização do usuário
{: #validate}

1. Comunique-se com o IAM para obter um token de acesso para uma chave API.
2. Valide a autorização para o usuário para a instância de serviço (/v2/authz POST).

### Autorização - Etapa 1: obtenha um token do IAM do {{site.data.keyword.Bluemix_notm}} usando a chave API.
{: #iam_token_using_api_key}

### POST /identity/token

#### Cabeçalhos:
{: #headers2}

  - Content-Type: application/x-www-form-urlencoded
  - Accept: application/json

#### Com parâmetros:
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
  "https://iam.cloud.ibm.com/identity/token"


```
{: codeblock}

### Resposta:
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

**Nota:** esse token é válido por 1 hora e pode ser reutilizado quantas vezes forem necessárias durante o prazo de 1 hora. É altamente recomendável que esse token seja armazenado em cache para evitar fazer essa solicitação para cada acesso ao `dashboard_url`.


### Autorização - Etapa 2: validar a autorização para o usuário para a instância de serviço (/v2/authz POST)
{: #step-2-authorization}

Agora que você autenticou o usuário e tem o seu próprio token de acesso, é necessário validar que o usuário é capaz de acessar o painel de serviço. Primeiro, são necessárias algumas informações que estão incluídas no token de acesso do usuário decodificado na etapa 2.1. Em seguida, use essas informações para chamar o IAM para verificar se o usuário está autorizado a acessar o painel na etapa 2.2.

**Etapa 2.1**: decodifique o token de acesso do usuário (retornado durante `**Authentication - Step 2:** Exchange the code for an access token` localizado na seção anterior.)
   O token de acesso é um token JWT que pode ser decodificado usando qualquer biblioteca compatível com JWT. Por exemplo, consulte a biblioteca incluída em nosso [código de amostra do broker](https://github.com/IBM/sample-resource-service-brokers){: new_window} ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo").
   Depois que o token é decodificado, o formato é conforme mostrado na seção a seguir; você extrai os campos `iam_id` e `scope`, que são usados na próxima etapa:

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
  "iss": "https://iam.cloud.ibm.com/identity",
  "grant_type": "urn:ibm:params:oauth:grant-type:apikey",
  "scope": "openid <your serviceName>",
  "client_id": "bx",
  "acr": 1,
  "amr": [
    "pwd"
  ]
}
```

**Etapa 2.2**: chame o IAM para verificar se o usuário está autorizado a acessar o painel

```
curl -X POST \
  -H "Accept: application/json" \
  -H "Content-Type: application/json" \
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
  https://iam.cloud.ibm.com/v2/authz
```

Veja o exemplo em nossos brokers de amostra: https://github.com/IBM/sample-resource-service-brokers

## Escagem de Token do IAM para Adotivos de Terce
{: #token_scoping}

Os tokens de acesso de usuário criados com seu ID de cliente podem ser usados apenas para acessar suas APIs de serviço. As solicitações para as outras APIs de nuvem que usam esse token resultam em acesso negado, mesmo se o usuário tem uma política apropriada configurada.

Como parte da integração de terceiro, o escopo do token está sendo usado para assegurar que os tokens tenham o escopo de acesso mínimo necessário para realizar os objetivos do usuário. Para facilitar isso, o acesso aos tokens do IAM é baseado no identificador de cliente que criou o token. Se um token do IAM foi criado por um serviço de terceiro, um usuário final não poderá executar determinadas APIs e funções, mesmo que o usuário tenha uma política apropriada configurada.

O impacto nas autorizações (todas as chamadas para `https://iam.cloud.ibm.com/v2/authz`) é a necessidade de transmitir informações de `escopo` no assunto. Essas informações estão contidas em um token do IAM (codificado em base64) na solicitação de `scope`.

A seção a seguir é um exemplo do que é incluído na chamada de autorização:
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
{: #next-steps}

Agora é hora de reunir tudo! Retorne para o console de gerenciamento de recurso para publicar seu serviço em visibilidade limitada e validar sua oferta no catálogo. Para obter mais informações, consulte [Publicando e testando seu serviço](/docs/third-party/cis4-rmc-publish.html).
