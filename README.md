# 📊 Sanitoral — Tableau de bord de pilotage de projets avec Power BI

## 📌 Présentation du projet

Dans le cadre de ma formation **Business Intelligence Analyst chez OpenClassrooms**, j’ai réalisé un projet de Business Intelligence pour Sanitoral, une entreprise fictive internationale spécialisée dans les produits d’hygiène bucco-dentaire.

L’objectif est de concevoir un tableau de bord interactif avec Power BI afin de suivre la performance des projets, comparer les données prévisionnelles aux données réelles et identifier rapidement les projets présentant des écarts importants.

Ce projet couvre plusieurs étapes : compréhension du besoin métier, préparation et modélisation des données, création d’indicateurs, conception de visualisations et mise en place de la sécurité des données.

## 🎯 1. Contexte et problématique métier

La direction souhaite disposer d’une vision claire de l’avancement et de la performance des projets IT et Marketing à l’échelle internationale.

Les principaux enjeux sont :

- Comparer les coûts réels aux coûts prévisionnels.
- Suivre les écarts de durée entre la planification et la réalisation.
- Contrôler les livrables réalisés par rapport aux objectifs.
- Identifier les projets présentant des écarts significatifs.
- Analyser les résultats par région, pays, type de projet et phase.
- Faciliter le suivi des projets et la mise en place d’actions correctives.

Le seuil d’alerte retenu est de **15 %**, avec une règle adaptée au sens de chaque indicateur.

## 🧭 2. Cadrage du besoin métier — Product Strategy Canvas

Le Product Strategy Canvas formalise les objectifs du tableau de bord, les profils utilisateurs et leurs besoins fonctionnels.

<img width="1001" height="576" alt="image" src="https://github.com/user-attachments/assets/48bccfe0-782a-4345-8c90-ff719b93aa40" />


### Utilisateurs cibles

**Directeur Général (DG)**

- Disposer d’une vision globale de la performance des projets.
- Identifier les projets en alerte.
- Repérer les situations nécessitant une décision ou une action corrective.

**Directeur Régional (DR)**

- Filtrer les résultats selon sa région.
- Suivre les projets présentant des écarts importants.
- Identifier les pays nécessitant une attention particulière.

**Directeur Pays**

- Consulter le détail des projets et de leurs phases.
- Comparer les données prévues et réelles.
- Identifier les écarts pour faciliter le suivi opérationnel.

Ces besoins ont guidé la conception des indicateurs, des filtres et des deux pages du tableau de bord.

## 🛠️ 3. Outils utilisés

- **Power BI Desktop** : modélisation, mesures, visualisations et sécurité des données.
- **Power Query** : nettoyage, transformation et préparation des données.
- **DAX** : création des indicateurs et calcul des écarts.
- **Excel** : consultation et vérification des données sources.
- **GitHub** : documentation et présentation du projet dans mon portfolio.

## 🧹 4. Préparation et transformation des données

Les données ont été préparées dans Power Query afin de les rendre exploitables dans Power BI.

Les principales opérations comprennent :

- Vérification et harmonisation des colonnes.
- Nettoyage et mise en forme des données.
- Préparation des tables de coûts, de durées, de livrables et de planification.
- Intégration des informations géographiques et des types de projets.
- Création d’une clé permettant d’identifier chaque projet et chaque phase.

### Clé de liaison projet-phase

Une colonne `Project_Phase_Key` a été créée dans les tables concernées afin de relier les données prévisionnelles et réelles au niveau du projet et de la phase.

Cette clé facilite le rapprochement des informations et l’analyse des écarts.

## 🗂️ 5. Modélisation des données

Le modèle Power BI s’appuie sur les tables suivantes :

- `Projects_plans`
- `Project type`
- `Actual_Costs`
- `Actual_Duration`
- `Actual_Deliverable`
- `Projects_Locations`
- `Country_Profiles`
<img width="1197" height="701" alt="image" src="https://github.com/user-attachments/assets/6b9b88bc-47cd-4574-9197-e4e84da78da8" />


La table `Projects_plans` contient les données de planification et les objectifs prévisionnels. Les tables `Actual_Costs`, `Actual_Duration` et `Actual_Deliverable` contiennent les données réelles utilisées pour analyser les écarts.

Les tables de localisation, de type de projet et de profil pays permettent de segmenter les analyses selon les besoins des utilisateurs.

La modélisation repose notamment sur les relations entre projets, phases, coûts, durées, livrables et informations géographiques.

## 📐 6. Indicateurs de performance

Les indicateurs ont été conçus pour comparer les données réelles aux données prévisionnelles.

### Écart de coût

Cet indicateur permet de repérer les projets dont les dépenses réelles dépassent le budget prévu et ceux dont les coûts sont inférieurs aux prévisions.

### Écart de durée

Cet indicateur mesure la différence entre la durée réelle et la durée planifiée afin d’identifier les retards et les projets terminés plus rapidement que prévu.

### Écart de livrables

Cet indicateur compare les livrables réalisés aux livrables prévus pour repérer les projets dont les objectifs de livraison ne sont pas atteints.

### Identification des projets à risque

Un projet est considéré comme étant à risque lorsqu’au moins une des conditions suivantes est remplie :

- Écart de coût supérieur à **+15 %**.
- Écart de durée supérieur à **+15 %**.
- Écart de livrables inférieur à **−15 %**.

Cette règle tient compte du sens de chaque indicateur : un dépassement de coût ou de durée est défavorable, tandis qu’un nombre de livrables inférieur aux prévisions constitue une alerte.

## 📊 7. Conception du tableau de bord

Le tableau de bord comporte deux pages complémentaires, conçues pour répondre aux besoins de pilotage global et de suivi détaillé.

### Page 1 — Vue globale et régionale

Cette page permet de suivre la performance générale du portefeuille de projets et de repérer les zones nécessitant une attention particulière.

Elle comprend notamment :

- Des cartes KPI présentant le nombre total de projets et le nombre de projets à risque.
- Des indicateurs de coûts réels et prévisionnels.
- Les écarts de coût, de durée et de livrables.
- Un graphique du nombre de projets par région.
- Une visualisation du nombre de projets à risque par région.
- Une répartition des projets par type.
- Une comparaison des coûts réels et prévisionnels par année.
- Une carte géographique permettant d’analyser la répartition des projets à risque.
- Des filtres pour explorer les résultats selon le type de projet, la région, le projet et l’indicateur sélectionné.

Cette page s’adresse principalement au Directeur Général et aux Directeurs Régionaux pour faciliter le suivi des performances et l’identification des alertes.

**Capture d’écran :**

<img width="1455" height="802" alt="image" src="https://github.com/user-attachments/assets/1bf0ba69-bfad-41d6-8ddc-d90edd3f7457" />


### Page 2 — Analyse détaillée des projets et des phases

Cette page permet d’examiner plus précisément les écarts au niveau des projets et des phases.

Elle comprend notamment :

- Des filtres pour sélectionner les projets et affiner l’analyse.
- Un tableau détaillé des écarts de coût, de durée et de livrables.
- Une analyse des phases des projets.
- Un diagramme de Gantt pour visualiser la planification des phases et faciliter le suivi de leur calendrier.

Cette page facilite l’identification des phases présentant des écarts et permet d’approfondir l’analyse des projets nécessitant un suivi opérationnel.

**Capture d’écran :**

<img width="1467" height="787" alt="image" src="https://github.com/user-attachments/assets/21437474-ce75-49ac-85ae-5f64381ea69b" />


## 🔐 8. Sécurité des données — Row-Level Security (RLS)

La sécurité au niveau des lignes (*Row-Level Security*, ou RLS) a été configurée dans Power BI Desktop afin d’adapter les données visibles au profil de l’utilisateur.

Trois rôles ont été définis :

| Rôle | Périmètre d’accès |
|---|---|
| `DG_Tous_Projets` | Ensemble des projets et des régions |
| `DR_Western_Europe` | Projets de la région Western Europe |
| `Pays_France` | Projets associés à la France |

Les rôles ont été testés dans Power BI Desktop avec la fonctionnalité **View as roles** afin de vérifier que les données affichées correspondent au périmètre autorisé.

La RLS permet de conserver un tableau de bord commun tout en limitant les données accessibles selon le profil de l’utilisateur.

*Remarque : l’affectation des utilisateurs aux rôles dans Power BI Service constitue une étape distincte lors du déploiement.*

## 📈 9. Lecture des indicateurs

Les écarts doivent être interprétés en tenant compte de leur sens.

| Indicateur | Situation favorable | Situation défavorable |
|---|---|---|
| Coût | Coût réel inférieur au coût prévu | Dépassement du budget |
| Durée | Projet réalisé plus rapidement que prévu | Retard par rapport au planning |
| Livrables | Objectif atteint ou dépassé | Livrables réalisés inférieurs aux prévisions |

Les seuils d’alerte permettent de repérer les situations nécessitant une analyse complémentaire.

## 💡 10. Résultats et valeur ajoutée

Le tableau de bord apporte plusieurs bénéfices :

- **Centralisation** : les principaux indicateurs sont regroupés dans un même environnement.
- **Visibilité** : les projets présentant des écarts importants sont plus faciles à repérer.
- **Analyse multidimensionnelle** : les résultats peuvent être explorés par région, pays, type de projet et phase.
- **Aide à la décision** : les responsables disposent d’informations structurées pour prioriser les analyses et les actions correctives.
- **Sécurité** : les rôles RLS configurés permettent de contrôler le périmètre des données visibles dans Power BI Desktop.

Le tableau de bord facilite ainsi le suivi du portefeuille de projets et contribue à une prise de décision fondée sur les données.

## 🧠 11. Compétences développées

Ce projet m’a permis de développer et de mettre en pratique les compétences suivantes :

- Analyse et formalisation d’un besoin métier.
- Traduction des besoins utilisateurs en indicateurs et visualisations.
- Nettoyage et transformation des données avec Power Query.
- Modélisation relationnelle dans Power BI.
- Création d’indicateurs avec DAX.
- Conception de tableaux de bord interactifs.
- Analyse des écarts entre prévisions et réalisations.
- Mise en place et test de rôles de sécurité RLS.
- Documentation d’un projet de Business Intelligence.

```

## 📚 12. Ce que j’ai appris

Ce projet m’a permis de comprendre les différentes étapes d’un projet de Business Intelligence, depuis le cadrage du besoin jusqu’à la conception d’un tableau de bord interactif.

J’ai notamment appris à structurer un modèle de données, à créer des indicateurs cohérents, à interpréter les écarts de performance et à configurer la sécurité au niveau des lignes pour adapter l’accès aux données.

Il m’a également permis de mieux comprendre l’importance de relier les indicateurs techniques aux besoins concrets des utilisateurs métier.


