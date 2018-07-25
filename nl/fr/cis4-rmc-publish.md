---


copyright:
  years: 2018
lastupdated: "2018-06-27"


---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:download: .download}

# Etape 5 : Publication et test de votre service

Maintenant que vos courtiers hébergés respectent la spécification OSB, vous pouvez accéder à nouveau à la console de gestion des ressources pour publier votre service dans le catalogue {{site.data.keyword.Bluemix_notm}}. Renseignez l'onglet *Deployments*, planifiez le déploiement de vos plans de service dans une ou plusieurs régions du catalogue {{site.data.keyword.Bluemix_notm}}, testez vos courtiers et pour finir, effectuez la publication dans le catalogue en mode de visibilité limitée. Une fois le déploiement effectué, testez votre offre afin de vous assurer qu'elle répond aux critères requis puis effectuez à nouveau le processus de publication, si nécessaire.


## Avant de commencer

Pour cette procédure, vous devez disposer d'une approbation permettant de fournir un service de facturation intégrée. Si vous n'avez pas effectué le processus d'enregistrement et d'approbation initial dans Provider Workbench, consultez le [tutoriel d'initiation](/docs/third-party/index.md).
{: tip}

Vérifiez que vous avez commencé l'étape 1 et avez terminé les étapes 2, 3 et 4 :
1. [Création de documents de service et d'annonce marketing](/docs/third-party/cis1-docs-marketing.html).
2. [Définition de votre offre dans la console de gestion des ressources](/docs/third-party/cis2-rmc-define.html).
3. [Développement et hébergement de vos courtiers de services](/docs/third-party/cis3-broker.html).
3. [Développement d'un flux d'authentification](/docs/third-party/cis-iam.html).

## Publication de votre service dans {{site.data.keyword.Bluemix_notm}}

1. Dans la console de gestion des ressources, cliquez sur la page **Deployments**.
2. Cliquez sur l'onglet **Brokers** puis sur **Add broker**
3. Cliquez sur **Manage** pour ouvrir la page Service Broker Configuration.
4. Ajoutez votre courtier hébergé puis cliquez sur **Register broker**.
5. Une fois l'enregistrement effectué, accédez à l'onglet **Catalog Deployments**.
6. Cliquez sur **Add Deployment** puis sélectionnez le plan et le courtier à déployer.
7. Sélectionnez la région et le centre de données où vous souhaitez déployer votre service puis cliquez sur **Add**.
8. Sur la page **Deployments**, consultez votre déploiement non publié puis cliquez sur **Publish**.
9. Sur la page **Publish to the Catalog**, consultez les détails de votre déploiement puis cliquez sur **Publish**.

La page Deployments doit être marquée comme complétée dans le navigateur, indiquant que les exigences minimales ont été respectées.

Vous êtes bloqué suite à un problème de déploiement ? Contactez votre interlocuteur IBM pour obtenir de l'aide.
{: tip}

## Test de votre offre déployée 

Etant donné que le déploiement a été effectué en mode de visibilité limitée, vous ne pouvez voir votre offre que dans le catalogue {{site.data.keyword.Bluemix_notm}} . A l'aide de la liste de contrôle ci-dessous, connectez-vous à {{site.data.keyword.Bluemix_notm}} et consultez les critères de test.

1. Connectez-vous à {{site.data.keyword.Bluemix_notm}} : [https://console.bluemix.net](https://console.bluemix.net){: new_window} ![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe") avec votre IBMid.
2. Vérifiez que vous utilisez le compte approprié (même compte que celui utilisé pour la création du service)
3. Cliquez sur le lien **Catalog** dans l'en-tête puis recherchez votre offre. Il peut être nécessaire d'ouvrir le catalogue de service expérimental. 
4. Utilisez ensuite la liste de contrôle pour valider votre service.

### Liste de contrôle - Test de votre service
1. Validez l'authentification à partir du tableau de bord d'instance de service
2. Le catalogue s'affiche correctement (l'importation à partir du courtier s'affiche correctement dans la console de gestion des ressources)
3. La mise à disposition fonctionne - vous pouvez créer une instance de service dans le plan de votre choix
4. L'annulation de la mise à disposition fonctionne - vous pouvez supprimer une instance de service.
5. La liaison fonctionne - vous pouvez cliquer sur **Connexions** et connecter votre service à une autre application
6. L'annulation de la liaison fonctionne - vous pouvez déconnecter votre service et supprimer la connexion.
7. Créez une clé de service/supprimez une clé de service - vous pouvez cliquer sur **Données d'identification** et générer une clé de service puis supprimer cette dernière.
8. Testez `plan_changeable` si vous prenez en charge plusieurs plans. Si vous activez cette possibilité en sélectionnant Yes, vous devez étendre votre courtier OSB afin de prendre en charge les modifications de plan pour les instances mises à disposition. Si votre offre prend en charge plusieurs plans et que vous souhaitez que les utilisateurs puissent en changer pour une instance mise à disposition, vous devez faire en sorte que ces derniers puissent mettre à jour leur instance de service. Pour plus de détails, voir le noeud final /v2/service_instances/{id_instance} PATCH dans le correctif de l'API Open Service Broker API v2.12 indiquant que l'utilisateur peut changer de plan dans l'instance mise à disposition. Pour effectuer un test, changez de plan pour une instance de service mise à disposition existante.
9. La spécification OSB ne prend pas en charge l'état désactivé (mais pas encore supprimé) d'une instance. Pour qu'IBM Cloud prenne en charge des clients pouvant avoir subi un retard de paiement ou d'autres situations générant une suspension de compte (sans qu'il ne soit annulé), IBM Cloud a défini des noeuds finaux étendus qui permettent de désactiver puis d'activer à nouveau des instances de service. Les extensions de noeud final suivantes sont **REQUISES**, consultez votre interlocuteur IBM en vue de tester vos noeuds finaux d'activation et de désactivation :
   - enable and disable instances (GET) : statut - renvoie l'état de votre instance de service.
   - enable and disable instances (PUT) : permet d'activer ou de désactiver une instance de service.
10. Testez la soumission d'utilisation si vous prenez en charge des plans mesurés. Pour tout plan avec une utilisation mesurée, vous devez valider les affirmations suivantes :
   - Vous pouvez exécuter des commandes curl pour l'API d'utilisation puis renvoyer correctement la tarification adaptée en fonction de l'utilisation.
   - Vous pouvez démontrer que vous avez activé la soumission horaire de l'utilisation, prenant en charge tous les utilisateurs qui mettent à disposition une instance de votre service.

Si vos tests échouent, répétez les étapes précédentes pour publier et tester à nouveau votre service, en renouvelant cette opération jusqu'à ce qu'elle aboutisse.


## Etapes suivantes

Maintenant que vous disposez d'un service fonctionnel dans le catalogue, vous pouvez créer une démonstration et demander une approbation afin de pouvoir diffuser publiquement votre service. Voir : [Etape 6 : Diffusion publique de votre service](/docs/third-party/cis6-ga.html).
