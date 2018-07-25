---


copyright:
  years: 2018
lastupdated: "2018-06-28"


---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:download: .download}

# Présentation : Développement d'un service de facturation intégrée
{: #overview}

Cette rubrique est conçue pour vous aider lors de la procédure de développement et de publication de votre service de facturation intégrée de tiers dans {{site.data.keyword.Bluemix_notm}}. Une fois que vous êtes autorisé à mettre à disposition votre offre dans le catalogue {{site.data.keyword.Bluemix_notm}}, vous allez commencer à la développer dans la console de gestion des ressources (interface utilisateur vous guidant lors de différents processus). Dans la console de gestion des ressources, vous allez concevoir vos métadonnées de catalogue, configurer vos plans de tarification de service et effectuer l'intégration avec IBM Cloud Access Management (IAM). Ensuite, en dehors de la console de gestion des ressources, vous allez effectuer le développement du code pour générer et héberger un nouveau courtier OSB (des exemples de courtier de démarrage et des documents d'API seront fournis) et vous allez utiliser IAM pour développer un flux d'authentification. Une fois ces étapes effectuées, vous accédez à nouveau à la console de gestion des ressources pour déployer votre service dans le catalogue en mode de visibilité limitée. Ainsi, vous pouvez tester et valider plusieurs exigences en matière de mise à disposition. Lorsque vous êtes prêt et que votre offre respecte toutes les exigences, votre service sera entièrement visible dans le catalogue {{site.data.keyword.Bluemix_notm}}. 


## Que dois-je faire pour mettre à disposition un service de facturation intégrée ?

Vous allez utiliser PWB, la console de gestion des ressources et l'environnement de développement pour atteindre vos objectifs. Consultez la [liste de contrôle](/docs/third-party/checklist.html#checklist) pour le suivi de ces procédures.

Les procédures suivantes récapitulent le processus d'intégration à un niveau élevé :

Pour cette procédure, vous devez disposer de l'approbation vous permettant de fournir un service de facturation intégrée. Si vous n'avez pas effectué le processus d'enregistrement et d'approbation dans PWB, voir la section présentant comment [commencer à publier votre offre de tiers dans {{site.data.keyword.Bluemix_notm}}](/docs/third-party/index.md)
{: tip}

1. [Création : Création de documents de service et d'annonce marketing (PWB)](/docs/third-party/cis1-docs-marketing.html)
2. [Définition : Définition de votre offre dans la console de gestion des ressources {{site.data.keyword.Bluemix_notm}}](/docs/third-party/cis2-rmc-define.html)
3. [Développement : Développement et hébergement d'un ou de plusieurs courtiers de services en utilisant la spécification d'API Open Service Broker](/docs/third-party/cis3-broker.html)
4. [IAM : Développement d'un flux d'authentification (OAuth), validation de l'autorisation utilisateur (v2/authz) et dérivation de votre URI de redirection](/docs/third-party/cis5-iam.html)
5. [Publication et test : Connexion de votre courtier OSB à la console de gestion des ressources, publication de votre service en mode de visibilité limitée dans le catalogue {{site.data.keyword.Bluemix_notm}} et test de votre offre](/docs/third-party/cis4-rmc-publish.html).
6. [Demandez l'approbation pour la disponibilité générale de votre service](/docs/third-party/cis6-ga.html)

## Support

Le service de facturation intégrée exige que les fournisseurs de services tiers disposent de leur propre modèle de support. Votre interlocuteur IBM vous aidera à activer votre modèle de support. De plus, il s'assurera que lorsqu'un utilisateur ouvre un ticket auprès de l'équipe de support {{site.data.keyword.Bluemix_notm}}, cette dernière transmet le ticket au site de support tiers.

## Mises à jour en continu

Une fois que votre service est publié, vous pouvez continuer à faire des mises à jour en collaborant directement avec votre interlocuteur {{site.data.keyword.Bluemix_notm}}.



