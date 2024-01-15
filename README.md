BMW FINANCIAL ANALYSIS

# Contexte:
Ce projet a été effectué dans le cadre de mise en situation à la fin de formation POEC Data Analyst de Global Knowledge.

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
https://www.bmwgroup.com/en/download-centre.html
https://annualreport2022.volkswagenag.com (modifier l'url pour accéder aux données des autres années)

# Étapes et outils:
## Étape 1: Compréhension de l'objectif et organisation du déroulement de projet 
- Compréhension des questions du projet,
- Exploration des données sources BMW et VW pour un inventaire des informations disponibles,
- Étude des mesures financières théoriques utiles à l'étude de la santé financière d'une entreprise (KPIs),
- Choix des mesures à calculer et des données intervenantes dans ces calculs, 
- Organisation du projet, diagramme de Gantt est utilisé.

## Étape 2: ETL (Extraction, Transform and Load)
Les données de BMW ont été extrait depuis des feuilles de calculs (.xlsx), transformé et néttoyées en utilisant Python (voir le colab ici). Ceux de VW en utilisant les outils de feuilles de calculs (Google Sheets et SheetsPal).

Exemple de feuille BMW original et résultat après traitement Python:
![image](https://github.com/elho2007/BMW/assets/34011591/916ae37f-22dc-4b97-bbfe-a719d1e65020)

Traitements effectués avec Python dans l'ordre:
- Téléchargement des feuilles de calculs depuis le site de BMW en utilisant Pandas,
- Effacer les lignes et colonnes non nécessauires,
- Transposition et ajout de noms de colonnes corrigés,
- Enregistrement en nouveaux feuilles de calculs,
- Construction des tâbles de faits et de dimensions.
