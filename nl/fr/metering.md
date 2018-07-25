---


copyright:

  years: 2017, 2018

lastupdated: "2018-06-21"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}
{:tip: .tip}

# Intégration des mesures
{: #meteringintera}

{{site.data.keyword.Bluemix}} prend en charge plusieurs modèles pour l'agrégation de l'utilisation de l'offre. Les fournisseurs d'offre prennent différentes mesures sur les instances mises à disposition et soumettent ces données au service approprié. Le service d'évaluation place l'utilisation soumise à différents emplacements (instance, groupe de ressources et compte) en fonction du modèle choisi par les fournisseurs d'offre. Les modèles d'agrégation et d'évaluation de toutes les mesures d'un plan sont disponibles dans les documents de définition de mesure et d'évaluation du plan.
{:shortdesc}

La liste suivante décrit les attentes pour le suivi et la soumission de l'utilisation :

*	Les fournisseurs d'offre tiers n'ont pas besoin de soumettre l'utilisation pour les plans gratuits.
*	Les fournisseurs d'offre tiers n'ont pas besoin de soumettre l'utilisation pour les plans d'abonnement mensuels.
*	Pour les plans mesurés, tous les fournisseurs d'offre doivent soumettre une utilisation horaire (pour les plans Lite, la soumission doit s'effectuer à une périodicité de 15 minutes à une heure).
*	Le fournisseur d'offre est chargé d'automatiser la soumission de l'utilisation, notamment l'automatisation de nouvelles tentatives suite à des échecs. {{site.data.keyword.Bluemix_notm}} ne fournit pas de fonction de nouvelle tentative pour les soumissions n'ayant pas abouti. Pour plus d'informations, consultez le tableau des codes d'état et d'actions à la section [Soumission des enregistrements d'utilisation](/docs/third-party/submitusage.html#submitting-usage-records).
*	Les enregistrements d'utilisation pour le mois en cours doivent être soumis au plus tard le 2 du mois suivant.
*	{{site.data.keyword.Bluemix_notm}} est configuré pour un cycle de facturation mensuelle et l'heure est représentée au format UTC.
*  Les fournisseurs d'offre doivent tester la soumission de l'utilisation et valider leurs résultats afin d'indiquer comment le cycle de facturation mensuelle est calculé.

Voir la page décrivant comment calculer vos coûts[](https://console.bluemix.net/docs/billing-usage/estimating_costs.html#cost) pour obtenir des informations d'ordre général sur la tarification.

## Propriétés de configuration
{: #configure}

Les propriétés suivantes définissent comment les soumissions d'utilisation pour les plans sont mesurées et évaluées :

<dl>
<dt>Unité</dt>
<dd>Eléments à mesurer (par exemple, appels d'API, octets, heures, instances et noeuds).</dd>
<dt>Agrégation</dt>
<dd>Mode de compilation des données d'unité mesurées, par exemple INSTANCES_BY_MONTH ou ACTIVE_HOURS_BY_MONTH.</dd>
<dt>Modèle de mesure</dt>
<dd>Mode de traitement des données de soumission, comme cela est présenté dans le tableau suivant.</dd>
<dt>Nom de ressource</dt>
<dd>Nom de la ressource mesurée (par exemple, stockage, instance, serveur virtuel ou octets transmis).</dd>
<dt>Nom d'unité</dt>
<dd>Nom descriptif de l'unité si le nom par défaut n'est pas adapté pour l'offre.</dd>
</dl>

## Types de modèle de mesure
{: #metermodel}

Le tableau suivant présente les modèles de mesure disponibles.

|  Type | Description  |
|-----|-----|
| standard_add | Quantité d'ajout de tous les enregistrements d'utilisation soumis pendant un mois. | 
| standard_max  | Quantité maximale de tous les enregistrements d'utilisation soumis pendant un mois. | 
| standard_avg | Quantité moyenne de tous les enregistrements d'utilisation soumis pendant un mois. |
| dailyproration_max | Valeur maximale quotidienne calculée. Récapitule tous les jours du mois. | 
| dailyproration_avg | Moyenne quotidienne calculée. Récapitule tous les jours du mois. |
| monthlyproration | Calcul similaire à la proratisation quotidienne mais le prix utilisé correspond au prix du plan divisé par le nombre total de jours pour le mois (prix par jour). |
{: caption="Tableau 1. Modèle de mesure" caption-side="top"}

### Exemples
Notez que la quantité indiquée dans le tableau de bord de chacun des exemples suivants correspond à la situation avant que l'utilisation suivante ne soit soumise mais après le traitement de l'utilisation en cours.

#### Ajout standard
Calcul des utilisations pour l'ensemble du mois

Formule : ADD(utilisations)

| Période            | Utilisation envoyée dans | Calcul | Quantité dans le tableau de bord |
|-----------------|:-------------:| ----------- |:---------------------:|
| Jour 1 (matin) | 5             | 5           | 5                     |
| Jour 1 (soir)   | 5             | 5 + 5       | 10                    |
| Jour 2 (matin) | 5             | 10 + 5      | 15                    |
| Jour 3 (matin) | 5             | 15 + 5      | 20                    |
| Jour 4 (soir)   | 5             | 20 + 5      | 25                    |

#### Moyenne standard
Calcule la moyenne des utilisations pour l'ensemble du mois. La soumission d'une utilisation égale à zéro est prise en compte lors du calcul de la moyenne.

Formule : AVG(utilisations)

| Période            | Utilisation envoyée dans | Calcul             | Quantité dans le tableau de bord |
|-----------------|:-------------:| ----------------------- |:---------------------:|
| Jour 1 (matin) | 4             | 4 / 1                   | 4                     |
| Jour 1 (soir)   | 0             | (4 + 0) / 2             | 2                     |
| Jour 2 (matin) | 5             | (4 + 0 + 5) / 3         | 3                     |
| Jour 3 (matin) | 3             | (4 + 0 + 5 + 3) / 4     | 3                     |
| Jour 4 (soir)   | 3             | (4 + 0 + 5 + 3 + 3) / 5 | 3                     |

#### Valeur maximale standard
Calcule la valeur maximale des utilisations pour l'ensemble du mois.

Formule : MAX(utilisations)

| Période            | Utilisation envoyée dans  | Calcul  | Quantité dans le tableau de bord |
|-----------------|:--------------:| ------------ |:---------------------:|
| Jour 1 (matin) | 5              | MAX(5)       | 5                     |
| Jour 1 (soir)   | 10             | MAX(5, 10)   | 10                    |
| Jour 2 (matin) | 0              | MAX(10, 0)   | 10                    |
| Jour 3 (matin) | 15             | MAX(10, 15)  | 15                    |
| Jour 4 (soir)   | 1              | MAX(15, 1)   | 15                    |

#### Moyenne de proratisation quotidienne
Calcule l'utilisation moyenne pour chaque jour et effectue une moyenne pour l'ensemble du mois. Les moyennes de chaque jour sont ajoutées puis ce nombre est divisé par le nombre de jours actuellement transmis (au format UTC).

Formule : total(moyenne quotidienne) / Nombre de jours transmis lors de la période de facturation

La quantité peut changer au cours du mois, mais l'élément évalué est l'utilisation moyenne par jour.

Prenons un mois à 30 jours :

| Période               | Utilisation envoyée dans    |Moyenne quotidienne | Calcul                            | Quantité dans le tableau de bord*                           |
| ------------------ | :--------------: | ------------- | ------------------                     | :----------------------------------------------: |
| Jour 1 (matin)     | 8                | 8 / 1         | 8 / 1                                  | 8                                                |
| Jour 1 (soir)      | 3                | (8 + 3) / 2   | 5,5 / 1                                | 5,5 (A la fin du jour 1)                               |
| Jour 2 (matin)    | 2                | 2 / 1         | (5,5 + 2) / 2                          | 3,75                                             |
| Jour 2 (soir)      | 5                | (2 + 5) / 2   | (5,5 + 3,5) / 2                        | 4,5 (A la fin du jour 2)                               |
| Jour 3 à jour 15    | 1                | 1 / 1         | (5,5 + 3,5 + (1 + 13)  / 15            | 1,4666 (A la fin du jour 15)                          |
| Jour 15 à jour 30   | 0                | 0 / 1         | (5,5 + 3,5 + (1 * 12) + (0  * 15) / 30 | 0,7333  (A la fin du jour 30)                         |

\* Situation au jour de soumission de l'utilisation.

#### Valeur maximale de la proratisation quotidienne
Calcule l'utilisation maximale par jour et calcule une moyenne pour le mois. La valeur maximale de chaque jour est ajoutée puis ce nombre est divisé par le nombre de jours actuellement transmis (au format UTC).

Formule : Total (valeur maximale quotidienne) / nombre de jours dans la période de facturation

La quantité peut changer au cours du mois, mais l'élément évalué est l'utilisation maximale par jour.

Prenons un mois à 30 jours :

| Période             | Utilisation envoyée dans  | Valeur maximale quotidienne | Calcul                    | Quantité dans le tableau de bord* |
|------------------|:--------------:| --------- | ------------------------------ |:----------------------:|
| Jour 1 (matin)  | 0              | MAX(0)    | 0 / 1                          | 0                      |
| Jour 1 (soir)    | 1              | MAX(0, 1) | 1 / 1                          | 1                      |
| Jour 2 à jour 15  | 1              | MAX(1)    | (1 + 1 + ...) / jour            | 1                      |
| Jour 15 à jour 30 | 0              | MAX(0)    | (1 + (1 * 14) + 0 + ...) / jour | < 1                    |

\* Situation au jour de soumission de l'utilisation.

## Exemples d'échelle d'évaluation et de mesure
{: #scale-examples}

Vous pouvez utiliser la configuration de mise à l'échelle pour compiler la quantité d'unités différemment lors de l'envoi dans les soumissions d'utilisation, lors de l'affichage dans le tableau de bord d'utilisation ainsi que lors de l'affichage des éléments utilisés pour les calculs d'évaluation et de coût. Les exemples suivants présentent des scénarios dans lesquels ces valeurs doivent être configurées :

### Vous souhaitez une granularité plus importante que ce que les utilisateurs voient
Vous souhaitez envoyer les utilisations à un niveau plus granulaire mais vous souhaitez malgré tout afficher un nombre lisible d'éléments pour les clients.

Par exemple, vous pouvez mesurer le trafic d'une instance en octets et avoir les valeurs agrégées en mégaoctets. Pour cela, ajoutez une `échelle` de 1024 à la configuration de **mesure**.

### Vous souhaitez une granularité plus importante que celle de votre configuration de tarification
La tarification des prix est effectuée sous la forme X $ / gigaoctet mais vous souhaitez envoyer ces données en mégaoctets. Si votre mesure est tarifiée sous la forme 1 $ / gigaoctets mais qu'un utilisateur utilise 0,5 mégaoctet, il est facturé 1 $ car votre tarification s'effectue par gigaoctet. Ajoutez une `échelle` de 1024 à la configuration d'**évaluation** et attribuez la valeur `true` à `clip`.

La valeur true est conservée si votre mesure est également tarifée sous la forme suivante : X $ par 100 appels d'API (ou autre taille de paquet).

### Vous souhaitez effectuer la mise à l'échelle aux niveaux de mesure et d'évaluation
Vous pouvez ajouter la mise à l'échelle pour les configurations de mesure et d'évaluation. Si vous souhaitez effectuer l'envoi en octets mais que l'affichage pour l'utilisateur s'effectue en mégaoctets, attribuez la valeur 1024 à l'échelle de mesure. Si votre tarif de mesure est en gigaoctets, vous pouvez également attribuer la valeur 1024 à l'échelle d'évaluation.

## Modèles de tarification
{: #pricing}

Le tableau suivant inclut des informations détaillées sur les modèles de tarification disponibles. Pour la plupart des mesures disponibles, sélectionnez un modèle de tarification associé.

| Modèle          | Description | Calcul | Exemple (quantité 5 000) |
|:-----------------|:-------------|:----------- |:---------------------|
| Linéaire         | Multipliez le prix unitaire par ressource (P) par la quantité d'utilisation (Q) pour obtenir le montant total (T)  | P*Q    | P = 1 $ T = 1*5 000 = 5 000 $        |
| Proratisation      | Multipliez le prix unitaire quotidien par ressource (P) par la quantité d'utilisation quotidienne (Q) pour obtenir le montant quotidien total. La facturation totale implique l'ajout des frais pour tous les jours du mois indiqué.         | T= (pd * Q1) + ...+(Pd *Qn)     | <ul><li>P= 30 $</li><li>Pd (prix par jour) = 30 $/30= 1 $ (pour un mois à 30 jours)</li><li>T1 = 1 $ * 1 =1 $</li><li>T2 = 1 $ * 0 =0 $</li><li>Tn = 1 * 1 =1 $</li><li>T = 1 $ + 0 $ +...+1 $ = 5 000$</li></ul>     |
| Niveau simple (niveau granulaire)  | Modèle P*Q dans lequel le prix unitaire de l'ensemble de la consommation est déterminé par le niveau de la quantité.           | <ul><li>Si Q est < = Q1, T = P1*Q</li><li>Si Q1 < Q < = Q2, T = P2*Q</li><li>Si Q2 < Q < = Q3, T = P3*Q</li></ul>     |   <ul><li>Q1 = 1 000, P1 = 1 $</li><li>Q2 = 2 500, P2 = 0,9 $</li><li>Q3 = 10 000, P3 = 0,75 $</li><li>T = 0,75 $ * 5 000 = 3 750 $</li></ul>              |
| Niveau gradué (niveau d'étape)   | Le prix par unité varie lorsque la quantité utilisée transite dans les différents niveaux prédéfinis. La facturation totale implique le cumul à partir des niveaux précédents           | <ul><li>T1 = P1*Q (0 < Q</li><li>Si Q1 < Q < = Q2, T = T2</li><li>Si Q2 < Q < = Q3, T = T3</li></ul>     | <ul><li>Q1 = 1 000, P1 = 1 $, T1 = 1*1 000</li><li>Q2 = 1 500, P2 = 0,9 $, T2 = 0,9*1 500</li><li>Q3 = 10 000, P3 = 0,75 $, T3 = 0,75*2 500</li><li>T = 1 000 + 1 350 + 1 875 = 4 225 $</li></ul>          |
| Niveau de bloc (quantité maximale)           | Le montant total facturé est établi en fonction d'une quantité maximale qui ne varie pas dans le bloc     | <ul><li>Si Q < = Q1, T = T1</li><li>Si Q1 < Q < = Q2, T = T2</li><li>Si Q2 < Q < = Q3, T = T3</li></ul>    |  <ul><li>Q1 = 1 000, T1 = 0 $</li><li>Q2 = 2 500, T2 = 2 500</li><li>Q3 = 10 000, T3 = 4 500 $</li><li>T = 4 500 $</li></ul>            |


