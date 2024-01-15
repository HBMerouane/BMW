# BMW FINANCIAL ANALYSIS

## Contexte:
<table>
<tr>
<td>
Ce projet a été effectué dans le cadre de mise en situation, à la fin de formation POEC Data Analyst de Global Knowledge. L'équipe contenait quatres membres: Houcine, Tomos, Nancy et Boubacar. Bien que les tâches ont été partagées, l'implication de tous les membres à chaque tâche était plus ou moins respectée.
</td>
</tr>
</table>
Image: Capture écran du tableau de bord élaboré avec Power BI et fourni parmi les déliverables.

![image](https://github.com/elho2007/BMW/assets/34011591/f2f9cfd2-6341-455d-93f9-7fd244648d0b)

<details open="open">
<summary>Sommaire</summary>

- [Résumé du projet](#Résumé-du-projet)
- [Sources des données](#Sources-des-données)
- [Étapes et outils](#Étapes-et-outils)
  - [Compréhension et organisation du projet](#Compréhension-et-organisation-du-projet)
  - [ETL](#ETL)(Extraction, Transform and Load)
  - [Nettoyage et préparation des données](#Nettoyage-et-préparation-des-données)
  - [Analyse, rapports et tableau de bord](#Analyse-rapports-et-tableau-de-bord)
- [Conclusion](#Conclusion)
- [Annexes](#Annexes)
</details>

# Résumé du projet
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
- https://annualreport2022.volkswagenag.com (modifier l'url pour accéder aux données des autres années, 2021, 2020, ...)

# Étapes et outils:
## Compréhension et organisation du projet
- Compréhension des questions du projet,
- Exploration des données sources BMW et VW pour un inventaire des informations disponibles,
- Étude des mesures financières théoriques utiles à l'étude de la santé financière d'une entreprise (KPIs),
- Choix des mesures à calculer et des données intervenantes dans ces calculs, 
- Organisation du projet, diagramme de Gantt est utilisé.

## ETL
### BMW
Les données de BMW ont été extrait depuis des feuilles de calculs (.xlsx), transformé et nettoyées en utilisant Python. 

Exemple de feuille BMW original et résultat après traitement Python:
![image](https://github.com/elho2007/BMW/assets/34011591/916ae37f-22dc-4b97-bbfe-a719d1e65020)

Traitements effectués avec Python dans l'ordre:
- Téléchargement des feuilles de calculs depuis le site de BMW en utilisant Pandas,
- Effacer les lignes et colonnes non nécessauires,
- Transposition et ajout de noms de colonnes corrigés,
- Enregistrement en nouveaux feuilles de calculs,
- Construction des tâbles de faits et de dimensions pour BMW.
### VW
De même, les données de VW ont été traitées en utilisant les outils de feuilles de calculs (Google Sheets et SheetsPal). Le temps nécessaire était moins important que celui de BMW en comptant le temps de développement Python mais en cas de données plus volumineux et de tâches répététives, il est clairement établi que Python est largement plus efficace.

## Nettoyage et préparation des données
Nous avons choisis Power BI pour cette étape et les étapes suivantes. Bien que le nettoyage des données a été effectué à l'étape 2 mais un nettoyage supplémentaire était nécessaire sous PBI Desktop pour corriger les erreurs de type par exemple. Deux modèles séparés pour BMW et VW ont été élaborés dû au partage de tâches entre les membres de l'équipe. Voici quelques opérations effectuées avec PBI Desktop dans cette étape:
- Nettoyage et typage des colonnes,
- Préparation de la colonne date (ici l'année, pas de données de jour ou mois),
- Construction des tables des faits et dimensions pour VW, celles de BMW ont été générée à l'étape précédente,
- Calculs des KPIs (DAX).
Les formules de mesures simples étaient suffisantes pour le calcul, sauf pour un KPI qui mesurait l'accroissement annuel du chiffre d'affaire, Voici sa formule:

```python
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
```
Image: Le modèle des données de BMW sur Power BI:

![image](https://github.com/elho2007/BMW/assets/34011591/e56ead57-d3da-4382-805b-2d0c29a018d1)


## Analyse, rapports et tableau de bord
Nous avons utilisé principalement des histogrammes pour visualiser le développement sur les années des différents KPIs, mais aussi des diagrammes sectoriels et courbe quand il s'agit de l'analyse par secteur d'activité. Voici quelques pages du rapport en incluant la formule du KPI utilisé:
- ![image](https://github.com/elho2007/BMW/assets/34011591/c562d99e-b2fd-4db2-aa33-532a1ea5916e)

- ![image](https://github.com/elho2007/BMW/assets/34011591/b76adb98-ff86-4fe5-ab5f-a853307c3bf2)

- ![image](https://github.com/elho2007/BMW/assets/34011591/830bff66-47a9-44d8-9cfe-afefc9a27456)
  
-![image](https://github.com/elho2007/BMW/assets/34011591/6f3f2b8d-f8be-4b13-a41e-3f537f7c500d)

Nous avons également inclus des prévisions pour les deux années suivantes 2022-2023:
![image](https://github.com/elho2007/BMW/assets/34011591/5f56f6ac-c100-4086-b75f-bbb569fd5083)

**Un travail similaire a été effectué pour VW pour obtenir des KPIs avec lesquels comparer ceux de BMW. Les deux rapports de BMW et VW générés séparément avec Power BI Destop, ont été chargé sur power BI Service pour élaborer un Dashboard résumant ces résultats et incluant un comparatif entre les deux groups**
![image](https://github.com/elho2007/BMW/assets/34011591/cf394d81-a7a7-4a03-8928-859f465fa65c)

Trois insights essentiels ont été tirées de cette analyse:
- BMW est en bonne santé financière, voire très bonne, ce qui a été validé par les indicateurs d'investissement sur les marchés boursiers;
- Depuis COVID, les deux entreprises BMW et VW récupèrent leur rythme de croissance constaté avant la crise;
- Bien que le taux d'endettement de BMW est légèrement meilleur que celui de VW, cela ne permet pas de dire que BMW est mieux placé pour obtenir des crédits de développement (Voir la crise de VW de 2015).

## Conclusion
Le projet nous a permis d'appliquer plusieurs connaissances et outils: Power BI, DAX, Power query, Python, Sheets, CSV. Par ailleurs, nous avons dû avoir de nouvelles connaissances en finance pour pouvoir utiiser les bon KPIs et faire les bonnes interprétations.

## Annexes
Téléchargez les fichiers nécessaires [ici]()
- Énnoncé du projet,
- Données nettoyés de VW,
- Données nettoyés et tables de faits et dimensions de BMW,
- Scripts Python (sous Colab);
