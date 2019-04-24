---

copyright:

  years: 2018, 2019

lastupdated: "2019-02-25"

keywords: billing service, resource management console, IBM Cloud, RMC, 

subcollection: third-party

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

Cette rubrique présente la procédure permettant de développer et de publier votre service de facturation intégrée tiers dans {{site.data.keyword.Bluemix}}. 
{:shortdesc}

Une fois que vous êtes autorisé à mettre à disposition votre offre dans le catalogue {{site.data.keyword.Bluemix_notm}}, vous allez commencer à la développer dans la console de gestion des ressources (interface utilisateur vous guidant lors de différents processus). Vous concevez vos métadonnées de catalogue, configurez les plans de facturation de service et intégrez ces données dans {{site.data.keyword.Bluemix_notm}} Identity and Access Management (IAM). 

Ensuite, en dehors de la console de gestion des ressources, vous effectuez le développement du code pour générer et héberger un nouveau courtier OSB. Des exemples de courtier de démarrage et des documents d'API sont fournis et vous utilisez IAM pour développer un flux d'authentification. Une fois ces étapes effectuées, vous accédez à nouveau à la console de gestion des ressources pour déployer votre service dans le catalogue en mode de visibilité limitée. Ainsi, vous pouvez tester et valider plusieurs exigences en matière de mise à disposition. Lorsque vous êtes prêt et que votre offre respecte toutes les exigences, votre service devient entièrement visible dans le catalogue {{site.data.keyword.Bluemix_notm}}.


## Fonctionnement du processus
{: #process}

Pour mettre à disposition un service de facturation intégrée, utilisez Provider Workbench, la console de gestion des ressources et l'environnement de développement de votre choix. Consultez la [liste de contrôle](/docs/third-party?topic=third-party-checklist#checklist) pour le suivi de ces procédures.

Pour cette procédure, vous devez disposer de l'approbation vous permettant de fournir un service de facturation intégrée. Si vous n'avez pas encore effectué le processus d'enregistrement et d'approbation initial dans PWB, consultez la rubrique relative à la [publication de votre offre tierce dans {{site.data.keyword.Bluemix_notm}}](/docs/third-party/index.md?topic=third-party-get-started#get-started).
{: tip}

1. [Création de votre documentation et de vos annonces marketing](/docs/third-party?topic=third-party-content-tasks#content-tasks).
2. [Définition de votre offre dans la console de gestion des ressources{{site.data.keyword.Bluemix_notm}}](/docs/third-party?topic=third-party-step2-define#step2-define).
3. [Développement et hébergement de vos courtiers de services](/docs/third-party?topic=third-party-step3-osb#step3-osb).
4. [Développement d'un flux d'authentification](/docs/third-party?topic=third-party-step4-iam#step4-iam).
5. [Test de votre service](/docs/third-party?topic=third-party-step5-pubtest#step5-pubtest).
6. [Diffusion publique de votre service](/docs/third-party?topic=third-party-public-releasing#public-releasing).

## Support
{: #support}

Le service de facturation intégrée exige que les fournisseurs d'offre tiers disposent de leur propre modèle de support. Votre interlocuteur IBM peut vous aider à activer votre modèle de support. De plus, il s'assure que lorsqu'un utilisateur ouvre un ticket auprès de l'équipe de support {{site.data.keyword.Bluemix_notm}}, le ticket est transmis au site de support tiers.

## Mises à jour en continu
{: #maintain}

Une fois que votre service est publié, vous pouvez continuer à faire des mises à jour en collaborant directement avec votre interlocuteur {{site.data.keyword.Bluemix_notm}}.



