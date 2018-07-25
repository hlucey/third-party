---


copyright:
  years: 2018
lastupdated: "2018-06-29"


---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:download: .download}

# Comment les services de facturation intégrée utilisent-ils la plateforme {{site.data.keyword.Bluemix_notm}} ?

Les services de facturation intégrée sont différents des services de référence. Un service de facturation intégrée utilise la plateforme {{site.data.keyword.Bluemix_notm}} pour l'authentification, l'accès, la mise à disposition, les opérations de mesure et la facturation. Cette rubrique présente de manière détaillée les composants de plateforme utilisés par votre service de facturation intégrée.

## Couche de mise à disposition {{site.data.keyword.Bluemix_notm}}

La couche de mise à disposition gère le cycle de vie des ressources {{site.data.keyword.Bluemix_notm}}. La couche de mise à disposition a la charge du contrôle et du suivi du cycle de vie des ressources dans un compte client. Les *ressources* sont des composants physiques et logiques pouvant être mis à disposition ou réservés pour une application ou une instance de service. Exemples de ressources : base de données,  comptes, limites de processeur, de mémoire ou de stockage. En général, les ressources suivies par la couche de mise à disposition sont conçues pour avoir une facturation et des mesures d'utilisation associées mais ce n'est pas toujours le cas. Dans la plupart des cas, les ressources peuvent être associées à la couche de mise à disposition afin de garantir que le cycle de vie des ressources peut être géré en même temps que le cycle de vie des comptes.

### Gestion du cycle de vie des ressources

La couche de mise à disposition fournit des API communes afin de contrôler le cycle de vie des ressources composé des étapes suivantes : mise à disposition (création d'une instance), liaison (création de données d'identification d'accès), annulation de la liaison (retrait d'accès), annulation de la mise à disposition (suppression d'une instance). De plus, la plateforme {{site.data.keyword.Bluemix_notm}} fournit des interfaces CLI et une interface utilisateur qui peuvent gérer le cycle de vie des ressources pour lesquelles il n'est pas nécessaire de créer vos propres fonctions.

La couche de mise à disposition fournit des API vous permettant de gérer les éléments suivants de votre cycle de vie de ressources :
* Mise à disposition
* Mise à jour d'une instance de ressource
* Liaison
* Clés de ressource
* Annulation de la liaison
* Annulation de la mise à disposition

## {{site.data.keyword.Bluemix_notm}} Identity and Access Management (IAM)

Identity Access Management (IAM) vous permet d'authentifier de manière sécurisée et de contrôler de façon cohérente l'accès à toutes les ressources d'{{site.data.keyword.Bluemix_notm}}. La couche de mise à disposition d'{{site.data.keyword.Bluemix_notm}} utilise IAM pour l'authentification et l'autorisation des actions effectuées dans la couche de mise à disposition. Les fournisseurs d'offre tiers utilisent IAM pour créer un flux d'authentification (OAuth). Pour plus de détails, voir [Qu'est-ce qu'IAM ?](/docs/iam/index.html#iamoverview)?

Si votre offre utilise des bibliothèques OpenID Connect (OIDC), IAM prend en charge l'intégration d'OIDC. OIDC est une couche d'authentification qui complète OAuth 2.0, structure d'autorisation, et qui peut permettre de simplifier le processus d'intégration. Pour plus d'informations sur OIDC, voir [Open ID Connect](http://openid.net/connect/){: new_window} ![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe").

## Catalogue {{site.data.keyword.Bluemix_notm}}

Le catalogue {{site.data.keyword.Bluemix_notm}} stocke les définitions d'offre (description, fonctions, images, URL, etc.) des ressources affichées dans la console {{site.data.keyword.Bluemix_notm}}. La console de gestion des ressources permet de définir tous les aspects des métadonnées requises de votre service. Ces métadonnées sont publiées dans le catalogue et utilisées pour affichage dans le catalogue. Des informations détaillées sur les zones de métadonnées requises et facultatives sont disponibles sur les pages **Offering** et **Plan** de la console de gestion des ressources. Cependant, les éléments principaux sont décrits ci-dessous pour une meilleure compréhension.

   * Service Name : nom technique de votre service. Le nom de service est essentiel et doit être correctement défini. Vous devez indiquer un nom de service permettant à la plateforme {{site.data.keyword.Bluemix_notm}} d'identifier le service ainsi que le nom que vos clients voient dans le catalogue {{site.data.keyword.Bluemix_notm}}. Le nom de service n'est pas votre nom affiché.
   * Service Display Name : nom intuitif de votre service. Par exemple, "Compose Redis"
   * Service ID : identificateur global unique de votre service utilisé dans les appels d'API de votre courtier OSB. Cette valeur doit être unique.
   * Service Icon : fichier SVG incluant votre logo de service
   * Service Description : description de la ressource qui s'affiche lorsque vous passez votre souris sur l'icône de ressource dans l'interface utilisateur du catalogue {{site.data.keyword.Bluemix_notm}}. Vous pouvez ajouter une phrase unique comme description.
   * Service Detailed Description : premier paragraphe qui s'affiche sur la page du catalogue. Pensez à utiliser au moins deux phrases pour une description détaillée.
   * Documentation URL : lien vers votre documentation {{site.data.keyword.Bluemix_notm}}. Vous deviendrez auteur dans PWB et votre valeur d'URL sera générée par PWB pour vous.
   * Terms URL: lien vers les dispositions de votre service. Pour des raisons liées au règlement RGPD, n'indiquez aucun lien vers les dispositions d'un service tiers. A la place, vous devez fournir une page unique pour un service de facturation intégrée.
   * Instructions URL : élément similaire à l'URL de documentation. Votre documentation {{site.data.keyword.Bluemix_notm}} est désignée. Toutefois, l'URL Instructions place dynamiquement votre documentation dans un onglet Initiation du tableau de bord de votre service.
   * Category : sélection des catégories {{site.data.keyword.Bluemix_notm}} disponibles où votre service doit être placé dans le catalogue.
   * Bullets : brèves descriptions de votre service
   * Media : captures d'écran et vidéos concernant votre service
   * Service Plan Name : chaque plan a un nom technique. Ce nom inclut des lettres en minuscules, aucun espace et peut inclure le caractère "-". Par exemple, `gold`.
   * Service Plan Display Name : nom intuitif du plan. Par exemple, `Gold`
   * Service Plan ID : identificateur global unique de votre plan de service utilisé dans les appels d'API de votre courtier OSB. Cette valeur doit être unique. La console de gestion des ressources génère cette valeur pour vous.
   * Service Plan Description : description du plan de ressources. Cette description s'affiche une fois que vous avez sélectionné un plan sur la page des détails de ressources dans le catalogue IBM Cloud
   * Service Plan Bullets : brèves descriptions de votre plan de service


## Open Service Broker

Les courtiers de services gèrent le cycle de vie des services. La plateforme {{site.data.keyword.Bluemix_notm}} interagit avec les courtiers de services pour mettre à disposition et gérer des instances de service (instanciation d'une offre de service) et des liaisons de service (représentation d'une association entre une application et une instance de service, qui contient souvent les données d'identification utilisées par l'application pour communiquer avec l'instance de service). Le fait de mettre à disposition des valeurs de métadonnées valides crée une réponse d'API REST lors d'une demande.

{{site.data.keyword.Bluemix_notm}} utilise la spécification OSB (Open Service Broker) `version 2.12`. Familiarisez-vous avec la [spécification d'API Open Broker](https://github.com/openservicebrokerapi/servicebroker/blob/v2.12/spec.md){: new_window} ![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe") et consultez le fichier readme pour en savoir plus.

Lorsque le contrôleur de ressources reçoit une demande de mise à disposition d'une ressource, il appelle votre courtier OSB afin de valider la disponibilité des régions, des plans, de l'offre et du type de service. Le contrôleur de ressources valide également la visibilité du plan associé au compte client. {{site.data.keyword.Bluemix_notm}} fournit des exemples de courtier et des documents d'API qui étendent la spécification OSB. Vous pouvez trouver plus d'informations sur le développement et l'hébergement de votre courtier lorsque vous parcourez les procédures détaillées de développement d'intégration de facturation.

## Service de mesure {{site.data.keyword.Bluemix_notm}}

Si un service inclut un plan mesuré, les utilisateurs {{site.data.keyword.Bluemix_notm}} sont facturés en fonction de la quantité de ressources qu'ils utilisent. Par exemple, les utilisateurs {{site.data.keyword.Bluemix_notm}} ayant recours à des services de base de données peuvent être facturés en fonction de la quantité de stockage utilisée par leurs applications. La soumission de l'utilisation doit être effectuée de telle sorte que l'utilisation soit convertie en enregistrement facturable.

Tous les services de facturation intégrée proposant un plan mesuré doivent utiliser le service de mesure {{site.data.keyword.Bluemix_notm}} pour transmettre les données d'utilisation.

**Remarque :** vous devez automatiser la soumission d'utilisation horaire en utilisant l'API de service de mesure si vous proposez un plan mesuré.

Pour plus d'informations sur la mesure, voir [Intégration de mesure](/docs/third-party/metering.html#meteringintera). Pour plus d'informations sur la soumission de l'utilisation mesurée, voir [Soumission de l'utilisation pour les plans mesurés](/docs/third-party/submitusage.html#submitusage)

## Scénario de mise à disposition : rassemblement de tous les éléments

En prenant en compte tous les concepts décrits précédemment, examinons le processus de création d'instance de service via la plateforme {{site.data.keyword.Bluemix_notm}}.

![Scénario de mise à disposition](images/flow-am.svg "Traitement de la création d'instance de service par la plateforme")

Lorsqu'un utilisateur souhaite créer une instance de service, il peut procéder d'une des manières suivantes :
* **Via l'interface de ligne de commande** : Utilisation de la commande `ibmcloud cli [ ibmcloud resource service-instance-create NAME SERVICE_NAME SERVICE_PLAN_NAME LOCATION ]`
* **Via la console {{site.data.keyword.Bluemix_notm}}** : L'utilisateur peut sélectionner le service, le plan et utiliser l'opération **Créer**.

La plateforme {{site.data.keyword.Bluemix_notm}} valide le fait que l'utilisateur dispose des droits lui permettant de créer l'instance de service en utilisant {{site.data.keyword.Bluemix_notm}} IAM. Une fois que cette validation a lieu, le noeud final de mise à disposition du courtier de services (PUT /v2/resource_instances/:resource_instance_id) est appelé. Lorsque la mise à disposition a lieu, les règles suivantes doivent être respectées :
* Le contexte {{site.data.keyword.Bluemix_notm}} doit être inclus dans la variable de contexte
* L'élément `X-Broker-API-Originating-Identity` doit avoir l'ID IBM IAM à l'origine de la demande
* La section des paramètres doit inclure l'emplacement demandé (et des paramètres supplémentaires requis par votre service).

Exemple de demande de mise à disposition :

```
    PUT /v2/service_instances/crn%3Av1%3Abluemix%3Apublic%3Acompose-redis%3Aus-south%3Aa%2F46aa677e-e83f-4d17-a2b6-5b752564477c%3A416d769b-682d-4833-8bd7-5ef8778e5b52?accepts_incomplete=true HTTP/1.1
    Host:  https://broker.compose.cloud.ibm.com
    Authorization: basic dXNlcjpwYXNzd29yZA==
    X-Broker-Api-Version: 2.12
    X-Broker-API-Originating-Identity: ibmcloud aWJtaWQtNDU2MzQ1WA==
    {
      "service_id": "0bc9d744-6f8c-4821-9648-2278bf6925bb", // your service's GUID from onboarding
      "plan_id": "ecc19311-aba2-49f7-8198-1e450c8460d4", //your plan's GUID from onboarding
      "context": {
        "platform": "ibmcloud",
        "account_id": "003e9bc3993aec710d30a5a719e57a80",
        "crn": "crn:v1:bluemix:public:compose-redis:us-south:a/003e9bc3993aec710d30a5a719e57a80:416d769b-682d-4833-8bd7-5ef8778e5b52",
        "resource_group_crn": "crn:v1:bluemix:public:resource-controller::a/003e9bc3993aec710d30a5a719e57a80::resource-group:b4570a825f7f4d57aa54e8e1d9507926",
        "target_crn": "crn:v1:bluemix:public:resource-catalog::a/e97a8c01ac694e308ef3ad7795c7cdb3::deployment:e62e2c19-0c3b-41e3-b8b3-c71762ecd489:us-south38399"
      },
      "parameters": {
        "location": "us-south",
        "optional-param":"parameter required by your service"
      }
    }
```

### Description du paramètre `context` {{site.data.keyword.Bluemix_notm}}

Dans l'exemple précédent, vous pouvez voir les métadonnées renvoyées dans le paramètre `context`. Le contexte de mise à disposition d'{{site.data.keyword.Bluemix_notm}} renvoie les éléments suivants :

* **platform** : Identifie la plateforme comme "ibmcloud"

* **"account_id"** : Renvoie l'ID du compte dans {{site.data.keyword.Bluemix_notm}} qui met à disposition l'instance de service.

* **crn** : Lorsqu'un client met à disposition votre service dans {{site.data.keyword.Bluemix_notm}}, une instance de service est créée et cette instance est identifiée par son nom de ressource de cloud (CRN) {{site.data.keyword.Bluemix_notm}}. Ce nom est utilisé lors de l'interaction avec {{site.data.keyword.Bluemix_notm}}, notamment lors de la mise à disposition, de la liaison (création de données d'identification et noeuds finaux), des opérations de mesure, de l'affichage dans le tableau de bord et du contrôle d'accès. Du point de vue du fournisseur de services, le nom de ressource de cloud (CRN) peut être traité comme une chaîne opaque à utiliser avec les API {{site.data.keyword.Bluemix_notm}}. Il peut également être décomposé en utilisant la structure suivante :

   ```
   crn:version:cname:ctype:service-name:location:scope:service-instance:resource-type:resource
   ```

   Dans l'exemple de mise à disposition, le nom CRN du service `compose-redis` est :

   ```
   crn:v1:bluemix:public:compose-redis:us-south:a/46aa677e-e83f-4d17-a2b6-5b752564477c:416d769b-682d-4833-8bd7-5ef8778e5b52::
   ```

   Dans cet exemple, cette instance `compose-redis` fait partie du compte {{site.data.keyword.Bluemix_notm}} ayant l'ID `46aa677e-e83f-4d17-a2b6-5b752564477c`, l'ID unique de l'instance est `416d769b-682d-4833-8bd7-5ef8778e5b52` et l'instance est hébergée dans la région `us-south` de l'élément {{site.data.keyword.Bluemix_notm}} public.

* **resource_group_crn** : renvoie le groupe de ressources contenant l'instance de service. Pour plus de détails, voir [Gestion des groupes de ressources](/docs/resources/resourcegroups.html).

   **Remarque** : Les fournisseurs de services ne sont pas concernés par le paramètre `resource_group_crn` sauf dans de très rares circonstances. Contactez votre interlocuteur IBM à propos de votre cas d'utilisation avant d'utiliser cette zone.

