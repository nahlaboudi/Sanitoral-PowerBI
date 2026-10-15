# 📊 Sanitoral : Tableau de bord de pilotage de projets (Power BI)

> **Projet de formation Business Intelligence Analyst (OpenClassrooms, diplôme niveau 6)**
> Tableau de bord Power BI pour suivre la performance de 104 projets IT et Marketing d'une entreprise fictive internationale, avec sécurité des données par rôle (RLS).

| | |
|---|---|
| **Outils** | Power BI Desktop, Power Query, DAX, Excel |
| **Compétences** | Cadrage du besoin, modélisation, mesures DAX, visualisation, RLS |
| **Données** | Jeu de données fictif fourni par OpenClassrooms |
| **Résultat clé** | 41 projets sur 104 identifiés à risque (≈ 39 %), dépassement de coût global de 7,29 % (≈ 4,1 M€) |

<img width="1455" height="802" alt="image" src="https://github.com/user-attachments/assets/95646f7d-d70b-4ab1-a15e-364debeee422" />


---

## 🎯 1. Contexte et problématique

Sanitoral est une entreprise fictive spécialisée dans les produits d'hygiène bucco-dentaire. Sa direction veut suivre l'avancement et la performance de ses projets IT et Marketing à l'échelle internationale.

**Questions auxquelles le tableau de bord répond :**
- Les coûts réels dépassent-ils les coûts prévus ?
- Les projets respectent-ils leur calendrier ?
- Les livrables prévus sont-ils réalisés ?
- Quels projets, régions et pays nécessitent une action corrective ?

**Seuil d'alerte : 15 %**, avec une règle adaptée au sens de chaque indicateur.

---

## 🧭 2. Cadrage du besoin : Product Strategy Canvas

Avant de construire le dashboard, j'ai formalisé le besoin dans un Product Strategy Canvas (3 profils utilisateurs, 9 user stories).

<img width="1001" height="576" alt="image" src="https://github.com/user-attachments/assets/301a01e9-64e8-4854-8a89-b6673075d2cf" />


| Profil | Besoin principal |
|---|---|
| **Directeur Général (DG)** | Vue globale, alertes sur les projets avec écart ≥ 15 %, décisions de poursuivre ou d'arrêter |
| **Directeur Régional (DR)** | Filtrer par région, carte avec code couleur, détail des alertes de sa zone |
| **Directeur Pays (DP)** | Avancement phase par phase, filtres par type et par date, infobulles de détail |

---

## 🗂️ 3. Préparation et modélisation des données

**Power Query :** vérification des colonnes, nettoyage, typage, intégration des informations géographiques et des types de projet.

**Clé de liaison `Project_Phase_Key` :** colonne créée pour identifier chaque combinaison projet + phase et relier le prévisionnel au réalisé.

### Modèle de données

<img width="1445" height="702" alt="image" src="https://github.com/user-attachments/assets/10c24dba-39fa-4ee2-aa89-1bd5a040b7d6" />



| Type | Tables |
|---|---|
| **Table de faits (prévisionnel)** | `Projects_plans` |
| **Tables du réalisé** | `Actual_Costs`, `Actual_Duration`, `Actual_Deliverable` |
| **Dimensions** | `Projects_Locations`, `Country_Profiles`, `Project type` |
| **Tables techniques** | `mesure` (toutes les mesures DAX), `Choix KPI` (sélecteur d'indicateur) |

---

## 📐 4. Indicateurs et règle de risque

| Indicateur | Favorable | Défavorable |
|---|---|---|
| **Écart de coût** | Coût réel inférieur au prévu | Dépassement du budget |
| **Écart de durée** | Projet plus rapide que prévu | Retard sur le planning |
| **Écart de livrables** | Objectif atteint ou dépassé | Livrables inférieurs aux prévisions |

**Un projet est « à risque » si au moins une condition est remplie :**
- écart de coût **> +15 %**
- écart de durée **> +15 %**
- écart de livrables **< −15 %**

### Exemple de mesure DAX

```dax
--Projets à risque = 
COUNTROWS(
    FILTER(
        VALUES(Projects_plans[Project ID]),
        [Écart de coût (%)] > 0.15
            || [Écart de durée (%)] > 0.15
            || [Écart des livrables (%)] < -0.15
    )
)

```



## 📊 5. Le tableau de bord

### Page 1 : Vue globale et régionale (DG et DR)

KPI (projets, projets à risque, coûts, écarts), projets par région, projets en alerte par région, répartition par type, coûts prévus vs réels par année, tableau par région, carte du monde des projets à risque, filtres (région, pays, type, KPI).
<img width="1455" height="802" alt="image" src="https://github.com/user-attachments/assets/7662feff-c261-402f-8e10-00a0db0e5cf0" />


### Page 2 : Analyse détaillée par projet et par phase (DP)

Tableau des écarts par projet et par phase (mise en forme conditionnelle), coûts par année, diagramme de Gantt des phases, filtre par projet.

<img width="1442" height="786" alt="image" src="https://github.com/user-attachments/assets/e8a8776f-069e-44f4-a419-bde4543c0a6c" />

### Page 3 : Documentation

Le rapport contient une page de documentation : définitions des indicateurs,
lecture des couleurs, rôles RLS et procédure de mise à jour.

**Mise à jour avec un nouveau fichier :**
1. Accueil → Transformer les données
2. Vérifier ou changer la source
3. Supprimer les lignes et colonnes vides
4. Utiliser la première ligne comme en-têtes
5. Vérifier les types de données
6. Recréer la colonne `Project_Phase_Key` (Projet + Phase)
7. Fermer et appliquer, puis actualiser le rapport

## 🔐 6. Sécurité des données : Row-Level Security (RLS)

Un seul rapport, trois vues différentes selon le profil.

| Rôle | Périmètre | Règle DAX |
|---|---|---|
| `DG_Tous_Projets` | Tous les projets et toutes les régions | *(aucun filtre)* |
| `DR_Western_Europe` | Projets de la région Western Europe | `[Region] = "Western Europe"` |
| `Pays_France` | Projets en France | `[Country] = "France"` |



<img width="402" height="387" alt="image" src="https://github.com/user-attachments/assets/b0d1779c-9a31-463e-b097-d4ebce4a3daa" />




---

## 💡 7. Résultats et enseignements



- **41 projets sur 104 (≈ 39 %)** dépassent un seuil d'alerte.
- **Budget :** 60,2 M€ de coûts réels pour 56,1 M€ prévus, soit **+7,29 % (≈ 4,1 M€)**.
- **Régions :** Central/Eastern Europe–Middle East–Africa concentre **22 alertes sur 56 projets** ; Western Europe en compte **14 sur 33**, soit le taux d'alerte le plus élevé (≈ 42 %).
- **Écarts par région :** dépassement de coût de 9,11 % (CEEMEA), 5,64 % (Western Europe) et 9,43 % (North & Latin America), alors que l'Asie-Pacifique est sous budget (−10,64 %).
- **Durée :** l'écart moyen est de −13,43 %, donc globalement les projets finissent plus tôt que prévu ; les alertes viennent surtout des coûts et des livrables.
- **Pays :** la Turquie, la Suisse et la Suède arrivent en tête du graphique des projets à risque.


---

## 🧠 8. Compétences démontrées

- Analyse et formalisation d'un besoin métier (Canvas, user stories)
- Nettoyage et transformation avec Power Query
- Modélisation relationnelle (clé `Project_Phase_Key`, schéma en étoile étendu)
- Mesures DAX et indicateurs conditionnels
- Conception de dashboards interactifs (filtres, carte, Gantt, mise en forme conditionnelle)
- Sécurité des données avec RLS
- Documentation d'un projet BI

---

## 📁 9. Contenu du dépôt et utilisation

```
├── README.md
├── Sanitoral_dashboard.pbix     ← rapport Power BI
├── images/                      ← captures d'écran
├── docs/                        ← Product Strategy Canvas, modèle de données
└── data/                        ← données fictives (si autorisé)
```

**Pour ouvrir le projet :** Power BI Desktop (Windows) est nécessaire. Ouvre le fichier `.pbix`, puis utilise *Modélisation > Afficher en tant que* pour tester les rôles.

---

## 📚 10. Ce que j'ai appris

Ce projet m'a fait parcourir toutes les étapes d'un projet BI : du cadrage du besoin à la sécurisation du dashboard. J'ai appris à structurer un modèle de données, à définir des indicateurs cohérents avec leur sens métier, et à adapter l'accès aux données selon le profil. J'ai aussi mesuré l'importance de relier chaque visuel à un besoin concret d'utilisateur.

---



