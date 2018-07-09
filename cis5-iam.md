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

# Step 4: Developing an authentication flow

When you defined your offering, The resource management console - **Access Management** page provided you with your {{site.data.keyword.Bluemix_notm}} Identity and Access Management (IAM) Client ID and Secret, your Service ID, and your API key. Now it's time to use those values to complete the following steps:

1. Derive your redirect URI based on your handling of your `dashboard_url`, return to the resource managent console and add it to the IAM Tab, ensuring you update your Client ID.
2. Develop the OAuth flow for authentication. You will use your redirect uri(s), client id and client secret as parameters to the `token_endpoint` IAM Rest APIs to complete this flow.
3. Validate user authorization:
   1. Communicate with IAM to obtain an access token from your api key
   2. Validate authorization for the user to the service dashboard using the `authorization_endpoint` (/v2/authz POST)

This step assumes you have been approved to deliver an Integrated Billing service. If you haven't yet completed the initial registration and approval in PWB, see: [Getting started publishing your third-party offering in {{site.data.keyword.Bluemix_notm}}](/docs/third-party/index.html)
{: tip}

## Before you begin

Ensure you have started step 1 and completed steps 2 and 3:
1. [Author service docs and marketing announcement](/docs/third-party/cis1-docs-marketing.html).
2. [Define your offering in the resource management console](/docs/third-party/cis2-rmc-define.html).
3. [Develop and host your service brokers](/docs/third-party/cis3-broker.html).


## Derive your IAM Redirect URI (resource management console: IAM page)

When you defined your service in resource management console, you generated a Client ID, but note that you likely did not have a Redirect URI at the time. This means IAM created a Client ID that is set to false. Until you return to the resource management console with your Redirect URI, you won't have a true Client ID.

The good news is that in the previous development step, you developed an OSB and hosted it (You probably saw IAM values in the sample broker code). The `redirect_uri` is usually the host url where the app lives with some additional url that will handle the authentication/authorization.

 Here are some example redirect URIs

```
https://myapp.bluemix.net/integrate/auth/callback
http://localhost:3000/auth/callback <-- for testing locally
```

Return to the resource management console and add your redirect URI to the IAM tab:

1. Sign into the console
2. Grab your redirect URI
3. Return to the resource management console
4. From the **IAM tab**, paste your redirect URI into the **Redirect URI** field.
5. Click **Update Client ID** to update your Client ID.

You should now have a Client ID that understands your Redirect URI and is set to true! You can use that Client ID in the next steps to develop your OAuth flow.

## Develop your OAuth flow for authentication
{: #oauth}


**Authentication - Step 0:** Find IAM regional endpoint for UI login closer to your deployed application by calling `https://iam.bluemix.net/identity/.well-known/openid-configuration`.

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

This request can be done once when the application is started and again if the `authorization_endpoint` fails. You should be able to cache the `authorization_endpoint` value for a short amount of time and refresh after the cache expired or an error is encountered.


**Authentication - Step 1:** When a user navigates to your `dashboard_url`, redirect browser to `<authorization_endpoint>?client_id=<your-client-id>&redirect_uri=<your-redirect-uri>&response-type=code&state=<your-resource-instance-id>`


-> login prompt will show up

-> User enters credentials

-> browser callback to redirect uri providing a "code" response parameter and "state" value


**Authentication - Step 2:** Exchange the code for an access token calling

### POST <token_endpoint>

#### Headers:
  - Authorization: Basic *[client id]:[client secret]*
  - Content-Type: application/x-www-form-urlencoded
  - Accept: application/json

#### With parameters:
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

### Response:

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

  Make sure to store the user's access_token returned in this response as it will be used during user authorization next.

See the example in our sample brokers: https://github.com/IBM/sample-resource-service-brokers

## Now it's time to validate the user authorization
{: #validate}

1. Communicate with IAM to obtain an access token for an api key
2. Validate authorization for the user to the service instance (/v2/authz POST)

### Authorization - Step 1: Get an {{site.data.keyword.Bluemix_notm}} IAM token using an API Key.
{: #iam_token_using_api_key}

### POST /identity/token

#### Headers:
  - Authorization: Basic *[client id]:[client secret]*
  - Content-Type: application/x-www-form-urlencoded
  - Accept: application/json

#### With parameters:
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

### Response:

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

**Note:** This token is valid for one hour, and can be reused as many times as needed during the one hour time frame. It is highliy recommended that this token is cached as to avoid doing this request for every access to the `dashboard_url`.


### Authorization - Step 2: Validate authorization for the user to the service instance (/v2/authz POST)

Now that we have authenticated the user and have our own access token, we need to validate the user has the ability to access the service dashboard. First, we'll need a few pieces of information included in the user's access token which we will decode on step 2.1. Then, we'll use that information to call IAM to check if the user is authorized to access the dashboard in step 2.2.

**Step 2.1**: Decode the user's access token (returned during `**Authentication - Step 2:** Exchange the code for an access token ` found above.)
   This is a JWT token which can be decoded using the any JWT compliant library. For example, see the library included in our [sample broker code](https://github.com/IBM/sample-resource-service-brokers).
   Once the token is decoded, the format is as shown below; we'll need to extract `iam_id` and `scope` fields which will be used in the next step:

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

**Step 2.2**: Call IAM to check if the user is authorized to access the dashboard

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

See the example in our sample brokers: https://github.com/IBM/sample-resource-service-brokers

## {{site.data.keyword.Bluemix_notm}} Identity and Access Management Token Scoping for third-party adopters
{: #token_scoping}

User access tokens created with your client id can only be used to access your service APIs. Requests to other cloud APIs using this token will result in access denied, even if the user has an appropriate policy configured.

As part of third-party integration, token scoping is being used to ensure that tokens have the minimal access scope needed to accomplish the user's goals. To facilitate this, IAM tokens will have access based on the client ID that created the token. This means that if an IAM token was created by a third-party service, an end user will not be able to execute certain APIs and functions, even if the user has an appropriate policy configured.

The impact on authorizations (all calls  to [v2/authz](https://iam.bluemix.net/v2/authz) is the need to pass down `scope` information in the subject. This information is contained inside an IAM token (base64 encoded) in the `scope` claim.

Here is an example of what has been added in the authorization call:
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

This is applicable to all usages (`user, serviceId, crn`) and all `subject.attributes` need a scope.

## Next steps

Now it's time to pull everyting together! Return to the resource management console to publish your service in limited visibility and validate your offering in the catalog. See: [Publishing and testing your service](/docs/third-party/cis4-rmc-publish.html).
