BMW FINANCIAL ANALYSIS

# Contexte:
Ce projet a été effectué dans le cadre de mise en situation, à la fin de formation POEC Data Analyst de Global Knowledge. L'équipe contenait quatres membres: Houcine, Tomos, Nancy et Boubacar. Bien que les tâches ont été partagées, l'implication de tous les membres à chaque tâche était plus ou moins respectée.

Image: Capture écran du tableau de bord élaboré avec Power BI et fourni parmi les déliverables.

![image](https://github.com/elho2007/BMW/assets/34011591/f2f9cfd2-6341-455d-93f9-7fd244648d0b)

# Sommaire:

# Résumé du projet:
Le projet consiste à faire une analyse des données financières de BMW de 2021 en mettant l'accent sur l'évolution d'une année à l'autre des points suivants suivants: 
- Chiffre d'affaire, 
- Coûts de production,
- Bénéfices brute et net,
- Actifs et passifs,
- Rendement de l'activité,
- etc.. 
Un autre aspect de l'étude consiste à faire une comparaison entre les résultats de BMW et ceux d'un concurrent, en l'occurence ici VW.
 
# Sources des données
Les données financières des groupe BMW et VW sont disponibles en libre accès au publique, sur leurs sites officiel respectives:
- https://www.bmwgroup.com/en/download-centre.html
- https://annualreport2022.volkswagenag.com (modifier l'url pour accéder aux données des autres années)

# Étapes et outils:
## Étape 1: Compréhension de l'objectif et organisation du déroulement de projet 
- Compréhension des questions du projet,
- Exploration des données sources BMW et VW pour un inventaire des informations disponibles,
- Étude des mesures financières théoriques utiles à l'étude de la santé financière d'une entreprise (KPIs),
- Choix des mesures à calculer et des données intervenantes dans ces calculs, 
- Organisation du projet, diagramme de Gantt est utilisé.

## Étape 2: ETL (Extraction, Transform and Load)
### Étape 2.1-BMW
Les données de BMW ont été extrait depuis des feuilles de calculs (.xlsx), transformé et nettoyées en utilisant Python (voir le colab ici). 

Exemple de feuille BMW original et résultat après traitement Python:
![image](https://github.com/elho2007/BMW/assets/34011591/916ae37f-22dc-4b97-bbfe-a719d1e65020)

Traitements effectués avec Python dans l'ordre:
- Téléchargement des feuilles de calculs depuis le site de BMW en utilisant Pandas,
- Effacer les lignes et colonnes non nécessauires,
- Transposition et ajout de noms de colonnes corrigés,
- Enregistrement en nouveaux feuilles de calculs,
- Construction des tâbles de faits et de dimensions pour BMW.
### Étape 2.2-VW
De même, les données de VW ont été traitées en utilisant les outils de feuilles de calculs (Google Sheets et SheetsPal). Le temps nécessaire était moins important que celui de BMW en comptant le temps de développement Python mais en cas de données plus volumineux et de tâches répététives, il est clairement établi que Python est largement plus efficace.

## Étape 3: Nettoyage et préparation des données
Nous avons choisis Power BI pour cette étape et les étapes suivantes. Bien que le nettoyage des données a été effectué à l'étape 2 mais un nettoyage supplémentaire était nécessaire sous PBI Desktop pour corriger les erreurs de type par exemple. Deux modèles séparés pour BMW et VW ont été élaborés dû au partage de tâches entre les membres de l'équipe. Voici quelques opérations effectuées avec PBI Desktop dans cette étape:
- Nettoyage et typage des colonnes,
- Préparation de la colonne date (ici l'année, pas de données de jour ou mois),
- Construction des tables des faits et dimensions pour VW, celles de BMW ont été générée à l'étape précédente,
- Calculs des KPIs (DAX).
Les formules de mesures simples étaient suffisantes pour le calcul, sauf pour un KPI qui mesurait l'accroissement annuel du chiffre d'affaire, Voici sa formule:

Growth revenue per year = 
VAR CurrentYearSales = SUM('F-IncomeStatement'[Revenues])
VAR PreviousYearSales = CALCULATE(
    SUM('F-IncomeStatement'[Revenues]),
    FILTER(
        ALL('Dim-Time'),
        YEAR('Dim-Time'[Date]) = YEAR(MAX('Dim-Time'[Date])) - 1
    )
)
RETURN
IF(
    ISBLANK(PreviousYearSales),
    BLANK(),
    DIVIDE(
        CurrentYearSales - PreviousYearSales,
        PreviousYearSales
    )
)

## Étape 4: Analyse et rapports
