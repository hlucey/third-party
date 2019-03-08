---

copyright:

  years: 2015, 2019

lastupdated: "2019-02-25"

keywords: IBM Cloud, different metering options, new IBM Cloud Identity, faqs 

subcollection: third-party

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:tip: .tip}
{:new_window: target="_blank"}
{:faq: data-hd-content-type="faq"}
{:note: .note}

# Foire aux questions
{: #3p-faqs}

## Quelles sont les différentes options de mesure pour les plans ?
{: #metering}
{: faq}

{{site.data.keyword.Bluemix}} prend en charge plusieurs modèles pour l'agrégation de l'utilisation d'offre. Les fournisseurs d'offres prennent différentes mesures sur les instances mises à disposition et soumettent ces mesures au service approprié. Le service d'évaluation place l'utilisation soumise à différents emplacements (instance, groupe de ressources et compte) en fonction du modèle choisi par les fournisseurs d'offre. Les modèles d'agrégation et d'évaluation de toutes les mesures d'un plan sont disponibles dans les documents permettant de définir la mesure et l'évaluation du plan.

Vous devez automatiser la soumission de l'utilisation horaire en utilisant l'API de service de mesure si vous proposez un plan mesuré.
{: note}

Pour plus d'informations sur l'opération de mesure, voir [Intégration des mesures](/docs/third-party?topic=third-party-meteringintera#meteringintera). Pour plus d'informations sur la soumission de l'utilisation mesurée, voir [Soumission de l'utilisation pour les plans mesurés](/docs/third-party?topic=third-party-submitusage#submitusage).

## Comment puis-je générer une nouvelle clé d'API {{site.data.keyword.Bluemix_notm}} Identity and Access Management ?
{: #iam-creds}
{: faq}

Une clé d'API vous est octroyée lorsque vous activez IAM. Il est primordial de sauvegarder cette clé. Cette valeur ne s'affichera plus. Si vous perdez votre clé d'API, vous pouvez supprimer la clé et en créer une nouvelle. Pour plus d'informations, voir [Gestion des clés d'API d'ID de service](/docs/iam?topic=iam-serviceidapikeys#serviceidapikeys). 


