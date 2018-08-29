---


copyright:
  years: 2018
lastupdated: "2018-08-21"


---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:download: .download}

# Etape 2. Définition de votre offre dans la console de gestion des ressources

La console de gestion des ressources est un outil disponible sur le Web qui vous permet d'intégrer votre offre de tiers au catalogue {{site.data.keyword.Bluemix_notm}}.

Maintenant que vous disposez d'une approbation vous permettant de mettre à disposition un service de facturation intégrée, vous êtes prêt à accéder à la console de gestion des ressources pour effectuer l'enregistrement, démarrer le développement de votre offre et proposer des plans de tarification :
   1. Enregistrez votre service avec la console de gestion des ressources et validez la page Summary.
   2. Entrez vos métadonnées de catalogue sur la page Offering.
   3. Enregistrez votre offre avec {{site.data.keyword.Bluemix_notm}} Identity and Access Management (IAM). L'enregistrement génère des données d'identification de client et de service utilisées pour l'authentification de votre service.
   4. Complétez la page Pricing, en vous assurant que votre offre de service d'{{site.data.keyword.Bluemix_notm}} propose les plans de tarification adaptés aux clients. Les plans définis incluent des données de mesure fournissant des détails d'utilisation importants.
   5. Exportez vos métadonnées d'offre au format JSON.


## Avant de commencer

Pour cette procédure, vous devez disposer d'une approbation permettant de fournir un service de facturation intégrée. Si vous n'avez pas effectué le processus d'enregistrement et d'approbation initial dans Provider Workbench, consultez le [tutoriel d'initiation](/docs/third-party/index.html).
{: tip}

1. Vérifiez que avez commencé la tâche suivante : [Etape 1 : Création de documents de service et d'annonce marketing (PWB)](/docs/third-party/cis1-docs-marketing.html).
2. Vérifiez que vous êtes enregistré auprès d'{{site.data.keyword.Bluemix_notm}}. Dans le cas contraire, [inscrivez-vous](https://console.bluemix.net/registration) avant de continuer.
3. Vérifiez que vous vous trouvez dans le compte correct avant de commencer à utiliser la console de gestion des ressources.
4. Préparez votre nom de service {{site.data.keyword.Bluemix_notm}}.

   Vous devez indiquer un nom de service permettant à la plateforme {{site.data.keyword.Bluemix_notm}} d'identifier le service ainsi que le nom que vos clients voient dans le catalogue {{site.data.keyword.Bluemix_notm}}.

  Lorsque vous enregistrez votre offre avec la console de gestion des ressources, votre nom de service {{site.data.keyword.Bluemix_notm}} doit être prêt. Le nom de service ne correspond pas au nom affiché. Il doit respecter les règles suivantes :
   - Le nom doit être entièrement en minuscule
   - Le nom ne peut pas inclure d'espace mais peut inclure des tirets (`-`)
   - Le nom doit comporter moins de 32 caractères

   Votre nom de service doit inclure le nom de votre entreprise. Si votre entreprise a plus d'une offre, il doit inclure à la fois l'entreprise et l'offre. Par exemple, l'entreprise Compose a des offres pour Redis et Elasticsearch. {{site.data.keyword.Bluemix_notm}} peut alors inclure les noms de service suivants pour ces offres : `compose-redis` et `compose-elasticsearch`. Ces deux noms de service ont des noms associés visibles dans le catalogue {{site.data.keyword.Bluemix_notm}} : *Compose Redis* et *Compose Elasticsearch*. Une autre entreprise (FastJetMail, par exemple) peut avoir la seule offre JetMail. Dans ce cas, le nom de service sera `fastjetmail`.

## Enregistrement de votre offre

Pour commencer, connectez-vous et enregistrez votre offre.

1. Connectez-vous à {{site.data.keyword.Bluemix_notm}} : [https://console.bluemix.net](https://console.bluemix.net){: new_window} ![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe") avec votre ID {{site.data.keyword.Bluemix_notm}}.
   **Avertissement** : Il est primordial d'être dans le compte {{site.data.keyword.Bluemix_notm}} approprié. Si vous avez plusieurs comptes, vérifiez que vous accédez au compte souhaité.
2. Accédez au tableau de bord de la console de gestion des ressources : [https://console.bluemix.net/onboarding/dashboard](https://console.bluemix.net/onboarding/dashboard){: new_window} ![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe").
3. Cliquez sur **New Resource** pour ajouter votre ressource.
4. Renseignez la zone **Resource name**. Cette valeur est votre nom de service {{site.data.keyword.Bluemix_notm}} unique extrait à la section précédente.
5. A ce stade du processus, nous ne attendons pas à ce que vous ayez un courtier de services hébergé existant. Sélectionnez **No** pour la zone **Is your broker ready for import?** Nous allons vous guider lors du processus de création d'un courtier. Vous accédez ensuite à la console de gestion des ressources pour importer votre courtier une fois qu'il est développé et hébergé.
7. Après la soumission, la page **Summary** s'affiche. Renseignez toutes les valeurs requises** supplémentaires puis cliquez sur **Save**.

Vous pouvez enregistrer votre progression dans la console de gestion des ressources puis accéder à nouveau à cette console pour ajouter des informations supplémentaires. La console de gestion des ressources est conçue pour vous aider à gérer le cycle de vie de votre service. Vous pouvez donc ne pas avoir immédiatement toutes les réponses pour toutes les zones.
{: tip}

## Saisie de vos métadonnées d'offre

Sur la page **Offering**, indiquez les valeurs de métadonnées stockées dans le catalogue {{site.data.keyword.Bluemix_notm}}. De plus, certaines de ces valeurs doivent être exportées et stockées dans votre courtier de services où elles sont utilisées pour la mise à disposition et renvoyées comme partie de la réponse `catalog (GET)`. Ces valeurs permettent d'accélérer le développement d'un courtier de services dans une procédure ultérieure.

1. Dans la console de gestion des ressources, cliquez sur la page **Offering** puis sur l'onglet **Listing Page**. ****Dans cet onglet, vous pouvez définir les métadonnées affichées dans votre tableau de bord de services de l'offre {{site.data.keyword.Bluemix_notm}}. Renseignez toutes les valeurs requises puis cliquez sur **Save**. La console de gestion des ressources effectue un enregistrement initial de votre service dans {{site.data.keyword.Bluemix_notm}} Identity and Access Management (IAM). Une notification indiquant que votre service a été enregistré avec IAM s'affiche. Vous allez effectuer des actions supplémentaires avec IAM ultérieurement.
2. Sur la page Offering, cliquez sur l'onglet **Settings**.
   1. Définissez l'option **Plan changes supported?** pour votre offre. La valeur par défaut est **No**. Si vous indiquez **Yes**, vous devez étendre votre courtier OSB pour prendre en charge des modifications de plan pour les instances mises à disposition. Si votre offre prend en charge plusieurs plans et que vous souhaitez que les utilisateurs puissent en changer pour une instance mise à disposition existante, vous devez faire en sorte que ces derniers puissent mettre à jour leur instance de service. Pour plus de détails, voir le noeud final `/v2/service_instances/{instance_id} PATCH` dans [l'API Open Service Broker v2.12](https://github.com/openservicebrokerapi/servicebroker/blob/v2.12/spec.md#updating-a-service-instance){: new_window} ![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe")
   2. Définissez l'option **Bindable** pour votre service. La valeur par défaut est **No**. Sélectionnez **Yes** si votre service peut être lié à des applications dans {{site.data.keyword.Bluemix_notm}}. Le cas échéant, il doit pouvoir renvoyer des données d'identification et des noeuds finaux d'API à vos consommateurs de service. Lors du développement d'un service pouvant être lié, vous devez utiliser les [opérations pouvant être liées dans l'API Open Service Broker v2.12](https://github.com/openservicebrokerapi/servicebroker/blob/v2.12/spec.md#binding){: new_window} ![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe")
   3. Renseignez toutes les zones requises supplémentaires puis cliquez sur **Save**.
3. La page Offering doit désormais comporter une coche dans la navigation, indiquant que vous avez respecté les exigences minimales requises pour cette page. S'il est toujours indiqué que la page est incomplète, vous devez l'ouvrir à nouveau et rechercher les zones incomplètes *requises*.

Votre lettre d'offre initiale inclut une URL de documentation de service générée par Provider Workbench. Vous devez entrer cette URL dans les zones **Documentation URL** et **Instructions URL**.
{: tip}

## Enregistrement avec IAM

IAM est requis pour tous les services intégrés à {{site.data.keyword.Bluemix_notm}}. Voir [Qu'est-ce qu'IAM ?](/docs/iam/index.html#what-is-cloud-iam-) pour en savoir plus sur les exigences et les concepts IAM.

La console de gestion des ressources génère les valeurs IAM suivantes :
   - ID de service (élément généré et stocké)
   - Clé d'API (élément généré et non stocké - s'affiche une seule fois)
   - ID client (élément généré et stocké)
   - Valeur confidentielle du client (élément généré et non stocké)

Le fournisseur de services doit fournir :
   - L'URI de redirection (vous accédez à nouveau à la console de gestion des ressources une fois que vous avez développé votre courtier OSB. Vous pouvez dériver l'URI de redirection à partir de l'emplacement du courtier de services hébergé)

1. Dans la console de gestion des ressources, cliquez sur la page **Access Management**.
2. Cliquez sur **Enable IAM**. La console de gestion des ressources enregistre votre service auprès d'IAM, crée votre règle et ID de service puis crée une clé d'API pour vous. Elle crée également un ID client et une valeur confidentielle incomplets. L'ID client doit être mis à jour avec votre URI de redirection une fois que vous en disposez d'un.
3. Cliquez sur **Status** pour voir l'état en cours de votre activation IAM.

**Remarque** : Vous devez accéder ultérieurement à la page IAM pour indiquer votre `URI de redirection`. Vous ne disposez pas de cette valeur tant que vous n'avez pas effectué de tâches de développement supplémentaires pour générer un flux d'authentification. Les étapes ultérieures vous permettent de définir votre valeur d'URI de redirection.

Une clé d'API vous est octroyée lorsque vous **activez IAM**. Il est primordial de la sauvegarder. Cette valeur ne s'affiche pas à nouveau. Si vous perdez votre clé d'API, vous pouvez supprimer la clé et en créer une nouvelle : [Gestion des clés d'API d'ID de service](/docs/iam/serviceid_keys.html#serviceidapikeys)
{: tip}

## Développement d'un plan de tarification

Lorsque vous intégrez votre service dans {{site.data.keyword.Bluemix_notm}}, vous devez définir un plan de planification. Si vous savez de manière précise comment vous souhaitez facturer les utilisateurs pour votre service, vous pouvez indiquer ces informations dans votre plan. Toutefois, si vous ne vous êtes pas encore décidé pour un plan payant, vous pouvez commencer par activer un plan gratuit puis configurer ultérieurement un plan payant.

1. Dans la console de gestion des ressources, cliquez sur la page **Pricing**.
2. Cliquez sur **Add plan** pour créer une entrée de plan puis cliquez sur **Edit plan** pour modifier le plan.
   * **Free plan** : Toutes les offres peuvent avoir un plan Lite qui est gratuit, permettant aux utilisateurs de tester votre service. Pour les plans gratuits, la valeur *Lite* est indiquée pour l'option **Display Name** et la valeur *lite* pour l'option **Programmatic Name**. Indiquez **Yes** pour **Is this plan free?**. Cliquez sur **Save**. Votre plan est publié dans le catalogue {{site.data.keyword.Bluemix_notm}}.
   * **Subscription plan** : Indiquez **No** pour l'option **Is this plan free?**. Renseignez les zones obligatoires. Conservez la valeur **Pricing metrics** par défaut. Cette mesure par défaut est fournie afin que vous puissiez facturer les utilisateurs une fois par mois. Cliquez sur **Save**. Votre plan est publié dans le catalogue {{site.data.keyword.Bluemix_notm}}. Sauvegardez la commande curl exemple pour soumettre l'utilisation.
   * **Metered plan** : Indiquez **No** pour l'option **Is this plan free?**. Renseignez les zones obligatoires. *Supprimez* la valeur d'abonnement **Pricing metrics** par défaut. Cliquez sur **Add another metric**, complétez la page **Add pricing metric** puis cliquez sur **Add metric**. Cliquez sur **Save**. Votre plan est publié dans le catalogue {{site.data.keyword.Bluemix_notm}}. Sauvegardez la commande curl exemple pour soumettre l'utilisation. Pour obtenir de l'aide en matière de sélection des mesures appropriées, voir [Intégration des mesures](/docs/third-party/metering.html).
3. La page **Pricing** doit désormais être marquée comme complète, indiquant que vous avez respecté les exigences minimales requises pour cette page.

Les fournisseurs de services doivent automatiser la soumission d'utilisation horaire pour tous les plans mesurés. Pour plus d'informations, voir [Soumission de l'utilisation pour les plans mesurés](/docs/third-party/submitusage.html)
{: tip}

## Exportation de vos métadonnées au format JSON

Maintenant que vous avez défini votre service dans la console de gestion des ressources, vous pouvez télécharger un fichier catalog.json et l'utiliser pour signaler le développement de votre courtier OSB. Le fichier catalog.json contient des métadonnées devant être hébergées dans votre courtier. Ces valeurs définissent le contrat entre le courtier et la plateforme {{site.data.keyword.Bluemix_notm}} pour les services et les plans pris en charge par votre courtier. Toutes les métadonnées de catalogue supplémentaires qui ne sont pas requises pour la mise à disposition sont stockées dans le catalogue {{site.data.keyword.Bluemix_notm}} et les mises à jour apportées à ce dernier affichent les valeurs utilisées pour le tableau de bord, telles que des liens et des icônes. De plus, les métadonnées traduites pour l'internationalisation doivent être mises à jour dans la console de gestion des ressources et non hébergées dans le courtier. Aucune des métadonnées stockées dans votre courtier ne s'affiche dans la console {{site.data.keyword.Bluemix_notm}} ou dans l'interface CLI {{site.data.keyword.Bluemix_notm}}. La console et l'interface CLI affichent les éléments définis dans la console de gestion des ressources et stockés dans le catalogue {{site.data.keyword.Bluemix_notm}}.

1. Dans la console de gestion des ressources, ouvrez la page **Deployments**.
2. Cliquez sur **Manage**.
3. Cliquez sur **Download Definitions**.

Sauvegardez votre fichier `catalog.json`. Vous allez l'utiliser pour développer votre courtier OSB (Open Service Broker) dans la section suivante.

## Etapes suivantes

Vous avez défini votre offre de service en ajoutant des métadonnées d'affichage de catalogue, en effectuant l'enregistrement avec IAM et en créant un ou plusieurs plans de tarification. Vous pouvez ensuite utiliser votre fichier JSON exporté et commencer à développer un courtier de services. Voir [Etape 3 : Développement et hébergement des courtiers de services](/docs/third-party/cis3-broker.html).
