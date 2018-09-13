---

 
copyright:

  years: 2017, 2018

lastupdated: "2018-08-30" 

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:tip: .tip}
{:new_window: target="_blank"}

# Soumission de l'utilisation pour les plans mesurés
{: #submitusage}

Vous devez toutes les heures soumettre l'utilisation pour toutes les instances de service actives. Si vous ne le faites pas, cela peut générer une perte de collecte des recettes pour IBM, pouvant ensuite provoquer une perte de revenu pour les fournisseurs d'offre.
{:shortdesc}

## Fonctionnement du processus
{: #process-flow}

La procédure suivante présente le processus de soumission d'utilisation :

1. Soumettez un test d'utilisation initiale en utilisant l'outil d'API REST de soumission d'utilisation afin de valider que vos plans mesurés sont correctement configurés.
2. Automatisez la soumission horaire continue dans l'outil d'API REST de soumission d'utilisation pour chaque plan mesuré. Vous pouvez héberger ces soumissions automatisées tant que l'élément SSO standard est pris en charge.
2. Les enregistrements d'utilisation sont regroupés en fonction du modèle de mesure et la quantité totale s'affiche sur le tableau de bord d'utilisation dans la console {{site.data.keyword.Bluemix_notm}}.
3. La quantité d'unités agrégées à partir du processus de mesure est utilisée, le coût est appliqué et la quantité appartenant à l'utilisateur pour l'instance de service est calculée.
4. A la fin du mois, le coût calculé final correspond à la quantité générée pour l'utilisateur.

## Prérequis
{: #prereqs}

Consultez les conditions préalables suivantes pour activer la fonction de mesure pour votre service :

* Le catalogue de facturation est mis à jour avec les prix de toutes les mesures payantes des plans de la ressource.
* Les définitions de mesure et d'évaluation de tous les plans de la ressource sont vérifiées et intégrées.

## Conseils pour la soumission de l'utilisation 
{: #metering_guidelines}

### Conseils de soumission

Reportez-vous aux conseils suivants lorsque vous utilisez le service de mesure {{site.data.keyword.Bluemix_notm}} pour soumettre des données d'utilisation de ressource :

* L'heure de début et l'heure de fin représentent la plage durant laquelle les mesures sont collectées. Ces heures ne dépendent pas de l'heure à laquelle l'enregistrement de l'utilisation est soumis aux API de mesure. 
* Les enregistrements d'utilisation sont des faits. Ne mettez pas à jour l'enregistrement d'utilisation après l'avoir créé. Un emplacement est spécifié lorsque vous créez avec succès un enregistrement d'utilisation. Si un code d'erreur s'affiche, consultez les [actions](#actions) possibles.
* Un enregistrement d'utilisation est identifié de manière unique par la signature `account_id/resource_group_id/resource_instance_id/consumer_id/plan_id/region/start/end`. Lorsqu'un tel enregistrement est traité, tout autre élément ayant la même signature est rejeté comme doublon.
* N'associez pas à d'autres services l'interaction avec le service de mesure. Les demandes doivent être traitées individuellement même si l'opération de mesure commence et se termine avec la mise à disposition et l'annulation de la mise à disposition de l'instance.
* Les données d'utilisation des ressources doivent être soumises au service de mesure une fois par période allant de deux à 24 heures. La fréquence de soumission de vos données d'utilisation dépend de la fréquence de changement de vos mesures d'utilisation.
* Les enregistrements d'utilisation doivent être soumis dans les deux jours suivant la prise de mesure. Les enregistrements d'utilisation plus anciens sont rejetés.
* Une soumission réussie renvoie le code de réponse 201. Si un autre code de réponse est renvoyé, mettez à jour et renvoyez les données jusqu'à ce que le code 201 s'affiche.

Vous trouverez ci-dessous les meilleures pratiques en matière de soumission de l'utilisation :

* Il est recommandé que les fournisseurs de services soumettent l'utilisation toutes les heures afin que le délai entre l'utilisation des ressources et l'heure à laquelle cette donnée apparaît dans les comptes de l'utilisateur ne soit pas trop long.
* Soumettez à nouveau les enregistrements d'utilisation uniquement si un échec est survenu dans la demande précédente. Ne soumettez pas à nouveau les enregistrements d'utilisation déjà acceptés.

### Instructions d'ID de service

  Vous devez suivre ces instructions lorsque vous spécifiez l'ID de service en utilisant la zone d'ID dans la définition de ressource :
  * Le premier caractère de l'ID doit être alphanumérique.
  * Utilisez les caractères A - Z, a - z et 0 - 9. Les seuls caractères spéciaux que vous pouvez utiliser sont les tirets (-) et les traits de soulignement (_).
  * Suivez la convention de casse mixte si l'ID contient plusieurs mots.
  * Vérifiez que l'ID comporte au maximum 50 caractères.

### Instructions de nom de ressource

  Vous devez suivrez ces instructions lorsque vous spécifiez le nom de la ressources en utilisant la zone resources.name dans la définition de ressource :

  * Utilisez uniquement des mots qui décrivent vos ressources. Par exemple, **Stockage** ou **AppelsApi**. 
  * Suivez la convention de casse mixte si le nom contient plus d'un mot.
  * Utilisez une majuscule pour la première lettre du nom.

### Instructions concernant le nom d'unité de ressource

  Vous devez suivre ces instructions lorsque vous spécifiez le nom d'unité de ressource en utilisant la zone resources.unit.name dans la définition de ressource :

  * Utilisez un mot comme nom d'unité et utilisez un trait de soulignement (_) et non un espace, pour séparer les mots. Par exemple, indiquez **API_CALL** et non **API CALL**.  
  * Utilisez des majuscules pour toutes les lettres du nom.
  
### Instructions concernant la quantité d'unités de ressource

  Vous devez suivre ces instructions lorsque vous spécifiez le type de quantité de ressource en utilisant la zone resources.unit.quantityType dans la définition de ressource :
  
  * Utilisez un mot pour le type de quantité.
  * Utilisez des majuscules pour toutes les lettres du type de quantité.
  
### Instructions d'ID d'agrégation

  Vous devez suivre ces instructions lorsque vous spécifiez l'ID d'agrégation en utilisant la zone aggregations.id dans la définition de ressource :

  * Utilisez des majuscules pour toutes les lettres du type de quantité.
  * Utilisez un trait de soulignement (_) et non un espace pour séparer les mots.
  * Vérifiez que cet ID commence par la valeur de l'élément aggregations.unit ou correspond à cette dernière. Par exemple, vous pouvez spécifier **API_CALLS_PER_MONTH** pour aggregations.id et spécifier **API_CALLS** pour aggregations.unit.

### Instructions d'unité d'agrégation

  Vous devez suivre ces instructions lorsque vous spécifiez l'unité d'agrégation en utilisant la zone aggregations.unit dans la définition de ressource :
   
  * Utilisez une forme au singulier pour le nom d'unité.
  * Utilisez des majuscules pour toutes les lettres du nom d'unité.
  * Vérifiez que le nom d'unité spécifié dans la zone aggregations.unit est le nom d'unité spécifié dans la zone resources.unit.name.
  
### Instructions de groupe d'agrégation

  Vous devez utiliser des lettres minuscules pour la zone aggregations.aggregationGroup dans la définition de ressource.
  
### Instructions de formule d'agrégation

  Pour la zone aggregations.formula dans la définition de ressource, si vous souhaitez utiliser des opérations arithmétiques dans la formule, vous devez utiliser l'unité de ressource en tant qu'opérande et une expression arithmétique infixe dans la fonction de la formule. Par exemple, vous pouvez indiquer la formule suivante pour convertir des octets en mégaoctets :
  ```
  SUM({BYTE}/1048576)
  ```

## API REST de soumission d'utilisation
{: #RAPIusesubmit}

Les utilisateurs {{site.data.keyword.Bluemix_notm}} sont facturés en fonction de la quantité de ressources qu'ils utilisent. Par exemple, les utilisateurs ayant recours à des services de base de données peuvent être facturés en fonction de la quantité de stockage utilisée par leurs applications.

Pour utiliser le service de mesure {{site.data.keyword.Bluemix_notm}} afin de signaler des données d'utilisation, implémentez l'API de service de mesure afin de signaler les données d'utilisation de votre offre. Pour plus de détails, voir la [documentation sur l'API publique](https://ibm-bluemix-docs.github.io/usage-submission/).  

Il vous est demandé d'automatiser la soumission d'utilisation horaire en utilisant l'API de service de mesure. Vous pouvez héberger votre soumission automatique sur tout noeud final HTTPs valide accessible sur le réseau Internet public.
{: tip}

## Soumission de vos enregistrements d'utilisation
{: #usage-records}

Les enregistrements d'utilisation constituent les plus petites entités faisant partie des valeurs agrégées des mesures. Un enregistrement d'utilisation est construit en utilisant les zones suivantes :

| Nom | Description                                           |
| ------ | ---------------------------------------------------- |
| resource_instance_id |  ID de l'instance de ressource.  |
| plan_id | Contrat utilisé pour l'agrégation et l'évaluation de l'enregistrement d'utilisation.   |
| start  | Période à partir de laquelle l'utilisation est mesurée, définie en millisecondes.  |
| end  | Période jusqu'à laquelle l'utilisation est mesurée, définie en millisecondes.  |
| region  | Région du fournisseur de l'offre dans laquelle l'utilisation est mesurée.  |
| measured_usage  | Grappe de mesures avec des valeurs.  |
| consumer_id | Facultatif. Cette zone est requise uniquement si l'agrégation est requise au niveau client. Seuls les fournisseurs d'offre connaissent la valeur consumer_id. |
{: caption="Tableau 1. Zones d'un enregistrement d'utilisation" caption-side="top"}

Vous pouvez soumettre plusieurs enregistrements d'utilisation en utilisant l'appel d'API et soumettre au maximum 100 enregistrements d'utilisation par appel. Le corps de la réponse inclut le statut d'acceptation de chaque enregistrement d'utilisation. Un code d'erreur s'affiche pour tout statut autre que 201 et il est indiqué pourquoi l'enregistrement d'utilisation n'est pas accepté. Le tableau suivant répertorie les codes d'état et les actions requises.

| Code d'état | Action requise                                       |
| ------ | ---------------------------------------------------- |
| 500 |  Essayez de soumettre à nouveau l'enregistrement d'utilisation. Si le problème persiste, contactez l'équipe de mesure BSS. |
| 400 |  L'enregistrement d'utilisation n'est pas au format correct. Soit, la validation du schéma a échoué (les mesures des enregistrements d'utilisation sont incorrectes), soit l'heure de début et de fin ne sont pas comprises entre l'heure de mise à disposition et l'heure d'annulation de mise à disposition. Mettez à jour l'enregistrement d'utilisation et soumettez-le à nouveau.   |
| 424  | Des problèmes ont été détectés dans les métadonnées d'instance. Mettez à jour les détails de l'instance et soumettez à nouveau l'enregistrement d'utilisation.  |
| 404  | La définition de mesure n'a pas été intégrée. Collaborez avec l'équipe de mesure BSS pour vous assurer que la ressource est intégrée puis soumettez à nouveau l'enregistrement d'utilisation.  |
| 409  | L'enregistrement d'utilisation est un doublon. N'essayez pas de le soumettre à nouveau. |
{: caption="Tableau 2. Code d'état et actions requises" caption-side="top"}
{: #actions}


  
