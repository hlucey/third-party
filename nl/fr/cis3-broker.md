---


copyright:
  years: 2018
lastupdated: "2018-06-26"


---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:download: .download}

# Etape 3 : Développement et hébergement de vos courtiers de services

En utilisant les métadonnées exportées de la console de gestion des ressources, vous allez créer un ou plusieurs courtiers de services dans le langage de programmation de votre choix.

Les courtiers de services gèrent le cycle de vie des services. La plateforme {{site.data.keyword.Bluemix_notm}} interagit avec les courtiers de services pour mettre à disposition et gérer des instances de service (instanciation d'une offre de service) et des liaisons de service (représentation d'une association entre une application et une instance de service, qui contient souvent les données d'identification utilisées par l'application pour communiquer avec l'instance de service). Le fait de mettre à disposition des valeurs de métadonnées valides crée une réponse d'API RESTful lors d'une demande.

Vous pouvez commencer à créer votre courtier en utilisant une combinaison des métadonnés exportées à partir de la console de gestion des ressources, de nos exemples de courtiers de services {{site.data.keyword.Bluemix_notm}} publics et de la documentation de l'API Resource Broker. Pour développer votre courtier, vous allez :

1. Consulter notre scénario de mise à disposition de plateforme
2. Parcourir la spécification OSB
2. Examiner le courtier {{site.data.keyword.Bluemix_notm}} exemple
3. Utiliser la documentation de l'API Resource Broker pour découvrir la logique de noeud final de l'API REST
4. Utiliser les métadonnées exportées à partir de la console de gestion des ressources pour le développement
5. Consulter les informations de courtier fournies par la plateforme {{site.data.keyword.Bluemix_notm}}
6. Parcourir les recommandations supplémentaires afin d'optimiser votre développement
7. Héberger votre courtier
8. Tester votre courtier

## Avant de commencer

Pour cette procédure, vous devez disposer d'une approbation permettant de fournir un service de facturation intégrée. Si vous n'avez pas effectué le processus d'enregistrement et d'approbation initial dans Provider Workbench, consultez le [tutoriel d'initiation](/docs/third-party/index.md).
{: tip}

Vérifiez que vous avez commencé l'étape 1 et avez terminé l'étape 2
1. [Création de documents de service et d'annonce marketing](/docs/third-party/cis1-docs-marketing.html).
2. [Définition de votre offre dans la console de gestion des ressources](/docs/third-party/cis2-rmc-define.html).


## Consultez notre scénario de mise à disposition de plateforme {{site.data.keyword.Bluemix_notm}}

Vous allez développer un courtier OSB (Open Service Broker) fonctionnant avec la plateforme {{site.data.keyword.Bluemix_notm}}. Consultez notre [scénario de mise à disposition](/docs/third-party/platform.html#provisioning-scenario-pulling-it-all-together) pour plus d'informations sur la création de ressources.

## Familiarisez-vous avec la spécification OSB

{{site.data.keyword.Bluemix_notm}} utilise la spécification OSB (Open Service Broker) `version 2.12`. Familiarisez-vous avec la [spécification d'API Open Service Broker](https://github.com/openservicebrokerapi/servicebroker/blob/v2.12/spec.md){: new_window} ![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe") et consultez le fichier readme pour en savoir plus.

## Affichez nos exemples de courtiers {{site.data.keyword.Bluemix_notm}}

[https://github.com/IBM/sample-resource-service-brokers](https://github.com/IBM/sample-resource-service-brokers){: new_window} ![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe")

**Remarque :** Tous les langages ne sont pas représentés par un exemple. Si vous avez besoin d'un courtier Python exemple, cherchez un exemple Cloud Foundry en utilisant Google. Il peut être nécessaire d'adapter cet exemple pour répondre aux exigences OSB.


## Consultez la documentation de l'API Open Service Broker {{site.data.keyword.Bluemix_notm}}

Les courtiers de services doivent être développés en prenant en compte l'[API Open Service Broker {{site.data.keyword.Bluemix_notm}}](https://console.bluemix.net/apidocs/821-ibm-cloud-open-service-broker-api?&language=node#introduction){: new_window} ![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe"). Familiarisez-vous avec l'API Broker et découvrez comment cette dernière interagit avec votre courtier ou vos courtiers.

{{site.data.keyword.Bluemix_notm}} Open Service Broker étend la spécification Open Service Broker 2.12.
{: tip}

### Logique de noeud final requise pour tous les courtiers de services

Les courtiers de services doivent fournir un ensemble standard de valeurs de métadonnées utilisées par les API REST et les courtiers {{site.data.keyword.Bluemix_notm}} doivent inclure la logique pour les noeuds finaux/chemins d'API REST suivants :

<dl>
  <dt>catalog (GET)</dt>
  <dd>Renvoie vos métadonnées de catalogue incluses dans votre courtier. Un grand nombre de valeurs de métadonnées de catalogue supplémentaires n'est pas renvoyé. Ces valeurs sont ajoutées exclusivement dans la console de gestion des ressources et stockées dans le catalogue {{site.data.keyword.Bluemix_notm}}.</dd>
  <dt>resource instances (PUT)</dt>
  <dd>Met à disposition votre instance de service</dd>
  <dt>resource instances (DELETE)</dt>
  <dd>Annule la mise à disposition de votre instance de service.</dd>
  <dt>resource instances (PATCH)</dt>
  <dd>Met à jour votre instance de service.</dd>
</dl>

**Remarque concernant catalog (GET)** : ce noeud final définit le contrat entre le courtier et la plateforme {{site.data.keyword.Bluemix_notm}} pour les services et les plans pris en charge par le courtier. Ce noeud final renvoie les métadonnées de catalogue stockées dans votre courtier. Ces valeurs définissent le contrat de mise à disposition minimal entre votre service et la plateforme {{site.data.keyword.Bluemix_notm}}. Toutes les métadonnées de catalogue supplémentaires qui ne sont pas requises pour la mise à disposition sont stockées dans le catalogue {{site.data.keyword.Bluemix_notm}} et les mises à jour apportées à ce dernier affichent les valeurs utilisées pour le tableau de bord, telles que des liens et des icônes. De plus, les métadonnées traduites d'internationalisation doivent être mises à jour dans la console de gestion des ressources et non hébergées dans le courtier. Aucune des métadonnées stockées dans votre courtier ne s'affiche dans la console {{site.data.keyword.Bluemix_notm}} ou dans l'interface CLI {{site.data.keyword.Bluemix_notm}}. La console et l'interface CLI affichent les éléments définis dans la console de gestion des ressources et stockés dans le catalogue {{site.data.keyword.Bluemix_notm}}. Il s'agit des valeurs requises minimales que catalog (GET) doit renvoyer :

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

### Logique des noeuds finaux requis pour les services pouvant être liés

Si votre service peut être lié à des applications dans {{site.data.keyword.Bluemix_notm}}, il doit pouvoir renvoyer des données d'identification et des noeuds finaux d'API à vos consommateurs de service. Un service pouvant être lié doit utiliser les opérations pouvant être liées dans la spécification Open Service Broker et implémenter les noeuds finaux/chemins suivants :

<dl>
  <dt>bindings and credentials (PUT)</dt>
  <dd>Lie votre instance de service à une application.</dd>
  <dt>bindings and credentials (DEL)</dt>
  <dd>Annule la liaison de votre instance de service à une application.</dd>
</dl>

### Noeuds finaux d'extension {{site.data.keyword.Bluemix_notm}} requis

La spécification OSB ne prend *pas* en charge l'état désactivé (mais pas encore supprimé) d'une instance. Pour qu'{{site.data.keyword.Bluemix_notm}} prenne en charge des clients pouvant avoir subi un retard de paiement ou d'autres situations générant une suspension de compte (sans qu'il ne soit annulé), {{site.data.keyword.Bluemix_notm}} a défini des noeuds finaux étendus qui permettent de désactiver puis d'activer à nouveau des instances de service. Les extensions de noeud final suivantes sont **requises** :

<dl>
  <dt>enable and disable instances (GET)</dt>
  <dd>Statut - renvoie l'état de votre instance de service.</dd>
  <dt>enable and disable instances (PUT)</dt>
  <dd>Vous permet d'activer ou de désactiver une instance de service.</dd>
</dl>

**Remarque** : Le fournisseur de services a la charge de désactiver l'accès à l'instance de service lorsque le noeud final de désactivation est appelé puis de réactiver cet accès lorsque le noeud final d'activation est appelé.

## Apprenez à utiliser les métadonnées exportées pour développer plus facilement votre courtier

Les métadonnées exportées à partir de la console de gestion des ressources peuvent être utilisées pour développer plus facilement votre propre courtier. Toutes les valeurs entrées dans la console de gestion des ressources sont requises pour la mise à disposition d'un service. Les métadonnées exportées à partir de la console de gestion des ressources définissent le contrat de mise à disposition minimal entre votre service et la plateforme {{site.data.keyword.Bluemix_notm}}. L'élément json exporté doit inclure les valeurs suivantes :

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


Votre tableau de services doit être identique aux métadonnées de l'offre ajoutées à la console de gestion des ressources. Pour garantir une parité individuelle entre OSB et la console de gestion des ressources, il est essentiel de comparer le tableau des services du fichier `catalog.json` téléchargé à partir de la console de gestion des ressources au tableau des services de votre courtier. Tous les noms et ID de plan et de service doivent correspondre.
{: tip}

## Informations de courtier fournies par la plateforme {{site.data.keyword.Bluemix_notm}}

Vos courtiers de services reçoivent les informations suivantes de la plateforme {{site.data.keyword.Bluemix_notm}} :

### X-Broker-API-Originating-Identity

L'**en-tête d'identité d'utilisateur** est fourni via un en-tête d'identité provenant d'une API. Cet en-tête de demande inclut l'identité IAM {{site.data.keyword.Bluemix_notm}} de l'utilisateur. L'identité IAM est codée en base 64. {{site.data.keyword.Bluemix_notm}} prend en charge un seul domaine d'authentification, `IBMid`. Le domaine `IBMid` utilise un ID unique (IU) IBMid pour définir l'identité de l'utilisateur dans {{site.data.keyword.Bluemix_notm}}. Cet ID unique est une chaîne opaque pour le fournisseur de services.

Exemple :

```
X-Broker-API-Originating-Identity: ibmcloud eyJpYW1faWQiOiJJQk1pZC01MEdOUjcxN1lFIn0=
Decoded:
{"iam_id":"IBMid-50GNR717YE"}
```

### Version d'en-tête d'API

La **version d'en-tête d'API** est [2.12](https://github.com/openservicebrokerapi/servicebroker/blob/v2.12/spec.md){: new_window} ![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe"). Par exemple : `X-Broker-Api-Version: 2.12`.

### resource instance (PUT) body.context and resource instance (PATCH) body.context

`PUT /v2/service_instances/:resource_instance_id` et `PATCH /v2/service_instances/:resource_instance_id` ont la valeur suivante dans **body.context** : `{ "platform": "ibmcloud", "account_id": "tracys-account-id", "crn": "resource-instance-crn" }`.

## Recommandations de courtier supplémentaires

### Recommandations en matière d'utilisation d'opérations asynchrones et d'opérations synchrones

L'API OSB prend en charge à la fois les modes de fonctionnement synchrones et asynchrones. Si vos opérations durent moins de 10 secondes, les réponses synchrones sont recommandées.  Dans le cas contraire, vous devez utiliser le mode de fonctionnement asynchrone.  Des informations supplémentaires sont disponibles dans la spécification OSB.

Si votre opération asynchrone dure moins de 10 secondes lors de la tentative de mise à disposition d'une instance, la plateforme arrivera à expiration.
{: tip}

### Recommandations pour la gestion des courtiers dans les différents emplacements

Il est important que les utilisateurs connaissent l'emplacement de leurs services Cloud pour le temps d'attente, la disponibilité et l'hébergement des données.

Lors de la mise à disposition d'instances de service sur {{site.data.keyword.Bluemix_notm}}, il est nécessaire que vous utilisateurs indiquent l'emplacement où cette instance de service doit être mise à disposition. Certains services peuvent prendre en charge la mise à disposition à plusieurs emplacements. Par exemple, un service de base de données peut prendre en charge la mise à disposition dans toutes les régions {{site.data.keyword.Bluemix_notm}} ou il peut prendre en charge uniquement un sous-ensemble.

Si votre service de tiers reposant sur une API est implémenté dans un autre cloud et exposé dans {{site.data.keyword.Bluemix_notm}}, l'emplacement doit indiquer l'emplacement du service dans l'autre cloud.

Lors de l'intégration à {{site.data.keyword.Bluemix_notm}}, vous devez implémenter au moins un courtier OSB mais vous pouvez avoir plus d'un courtier en fonction de votre stratégie de déploiement et des emplacements à prendre en charge pour votre service.  Dans l'outil de console de gestion des ressources, vous avez établi le mappage entre votre bloc de données service/plan/emplacement et le courtier qui va traiter les opérations pour ce bloc de données. Les choix standard consistent à définir un courtier unique pour traiter tous les emplacements pour votre service ou à définir un courtier par emplacement. Ce choix dépend de votre fournisseur de services.

Pour obtenir la liste des emplacements disponibles, consultez les [emplacements IBM Global Catalog](https://resource-catalog.bluemix.net/search?q=kind:geography){: new_window} ![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe"). Si votre service exige que des emplacements supplémentaires soient définis dans le catalogue global, consultez l'équipe d'intégration {{site.data.keyword.Bluemix_notm}}.


## Hébergement de vos courtiers

Votre courtier doit être hébergé comme partie d'une application pouvant répondre aux appels d'API REST. De plus, votre emplacement hébergé doit être conforme aux instructions de sécurité {{site.data.keyword.Bluemix_notm}}. L'hébergement peut être effectué dans {{site.data.keyword.Bluemix_notm}} ou en externe tant que l'élément est accessible publiquement à partir d'{{site.data.keyword.Bluemix_notm}}.

Pour héberger votre courtier en dehors d'IBM, vous devez vous assurer que les instructions de sécurité suivantes sont respectées :
- Le protocole TLS (Transport Layer Security) version 1.2 doit être respecté
- L'hébergement doit être effectué sur un noeud final HTTPs valide accessible sur le réseau Internet public

Si vous souhaitez effectuer l'hébergement dans {{site.data.keyword.Bluemix_notm}}, vous pouvez trouver des informations sur la création d'une application utilisant des conteneurs (Kubernetes) ici : [Utilisateurs internes - Informations sur l'utilisation](/docs/containers/cs_internal.html#cs_internal).

Vous allez avoir besoin de l'emplacement hébergé de votre courtier de services pour l'étape suivante. Faites en sorte que l'URL et les données d'identification associées à votre application soient prêtes pour l'étape suivante.
{: tip}

## Test de votre courtier de services

Vous devez valider votre courtier en exécutant des commandes curl pour les noeuds finaux que vous activez. Le fichier readme exemple inclut des conseils pour l'exécution de commandes curl sur vos noeuds finaux OSB : https://github.com/IBM/sample-resource-service-brokers/blob/master/README.md

### Exécution de commandes curl pour votre courtier de services

Utilisez l'exemple suivant pour tester la réponse curl de vos courtiers :

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

## Etapes suivantes

Vous venez de créer et d'héberger un courtier de services respectant la spécification OSB. Voir [Etape 4 : Développement d'un flux d'authentification](/docs/third-party/cis5-iam.html).
