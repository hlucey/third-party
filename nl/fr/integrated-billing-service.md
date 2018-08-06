---


copyright:
  years: 2018
lastupdated: "2018-07-20"


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

Ensuite, en dehors de la console de gestion des ressources, vous effectuez le développement du code pour générer et héberger un nouveau courtier OSB (des exemples de courtier de démarrage et des documents d'API sont fournis) et vous utilisez IAM pour développer un flux d'authentification. Une fois ces étapes effectuées, vous accédez à nouveau à la console de gestion des ressources pour déployer votre service dans le catalogue en mode de visibilité limitée. Ainsi, vous pouvez tester et valider plusieurs exigences en matière de mise à disposition. Lorsque vous êtes prêt et que votre offre respecte toutes les exigences, votre service devient entièrement visible dans le catalogue {{site.data.keyword.Bluemix_notm}}.


## Fonctionnement du processus
{: #process}

Pour mettre à disposition un service de facturation intégrée, utilisez Provider Workbench, la console de gestion des ressources et l'environnement de développement de votre choix. Consultez la [liste de contrôle](/docs/third-party/checklist.html#checklist) pour le suivi de ces procédures.

1. [Création de votre documentation et de vos annonces marketing](/docs/third-party/cis1-docs-marketing.html).
2. [Définition de votre offre dans la console de gestion des ressources{{site.data.keyword.Bluemix_notm}}](/docs/third-party/cis2-rmc-define.html).
3. [Développement et hébergement de vos courtiers de services](/docs/third-party/cis3-broker.html).
4. [Développement d'un flux d'authentification](/docs/third-party/cis5-iam.html).
5. [Test de votre service](/docs/third-party/cis4-rmc-publish.html).
6. [Diffusion publique de votre service](/docs/third-party/cis6-ga.html).

Pour cette procédure, vous devez disposer de l'approbation vous permettant de fournir un service de facturation intégrée. Si vous n'avez pas effectué le processus d'enregistrement et d'approbation initial dans Provider Workbench, consultez le [tutoriel d'initiation](/docs/third-party/index.md).
{: tip}

## Support
{: #support}

Le service de facturation intégrée exige que les fournisseurs d'offre tiers disposent de leur propre modèle de support. Votre interlocuteur IBM peut vous aider à activer votre modèle de support. De plus, il s'assure que lorsqu'un utilisateur ouvre un ticket auprès de l'équipe de support {{site.data.keyword.Bluemix_notm}}, le ticket est transmis au site de support tiers.

## Mises à jour en continu
{: #maintain}

Une fois que votre service est publié, vous pouvez continuer à faire des mises à jour en collaborant directement avec votre interlocuteur {{site.data.keyword.Bluemix_notm}}.



