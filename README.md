
# Détection d'opportunités de missions de conseil à partir d'un FEC

## Contexte

Ce projet a été réalisé dans le cadre d'un cas pratique de **Data Analyst / Data Science**.

L'objectif est d'exploiter un **Fichier des Écritures Comptables (FEC)** anonymisé afin de construire des indicateurs financiers, d'identifier automatiquement des opportunités de missions de conseil et de restituer les résultats sous la forme d'un dashboard destiné aux associés d'un cabinet.

---

## Objectifs

Le projet répond aux quatre étapes demandées dans l'énoncé :

1. Explorer et comprendre les données du FEC.
2. Construire des indicateurs financiers pertinents.
3. Identifier des opportunités de missions de conseil à partir de règles métier.
4. Restituer les résultats dans un dashboard exploitable par un associé non technique.

---

## Structure du projet

```text
numeris_test/
│
├── data/
│   ├── source/
│   │   ├── fec_final_anonyme.csv
│   │   └── clients_anonymises_final.csv
│   │
│   └── parquet/
│       └── fec_final_anonyme.parquet
│
├── notebook/
│   ├── notebook.ipynb
│   └── dashboard_associes.html
│
├── README.md
└── requirements.txt
```
---

## Technologies utilisées

* Python
* Polars
* NumPy
* PyEcharts
* Jupyter Notebook

---

## Indicateurs construits

Les indicateurs suivants sont calculés à partir des écritures comptables du FEC :

* Chiffre d'affaires mensuel et annuel
* Position de trésorerie
* Créances clients
* Dettes fournisseurs
* Besoin en Fonds de Roulement (BFR)
* DSO (Days Sales Outstanding)

Les calculs reposent sur les comptes comptables correspondants et sur des hypothèses explicitement documentées dans le notebook.

---

## Détection des opportunités de missions

Les indicateurs calculés sont utilisés pour détecter automatiquement plusieurs missions de conseil :

* Optimisation du recouvrement clients
* Optimisation du BFR
* Pilotage de la trésorerie
* Accompagnement au pilotage financier
* Optimisation de la structure financière
* Diagnostic financier approfondi

Chaque mission est déclenchée par un ensemble cohérent de signaux financiers et est accompagnée :

* d'un niveau de priorité ;
* d'une explication métier ;
* des indicateurs ayant conduit à cette recommandation.

---

## Dashboard

Le dashboard fournit deux niveaux de lecture :

### Vue globale

* évolution du chiffre d'affaires mensuel ;
* Top 10 des entreprises par chiffre d'affaires ;
* distribution du DSO ;
* distribution du BFR ;
* distribution de la trésorerie ;
* répartition des opportunités par mission ;
* répartition des opportunités par forme juridique.

### Opportunités actionnables

Le tableau final présente, pour chaque opportunité détectée :

* le client ;
* la mission recommandée ;
* le niveau de priorité ;
* les principaux indicateurs financiers ;
* une explication destinée aux associés.

---

## Exécution

1. Installer les dépendances :

```bash
pip install -r requirements.txt
```

2. Ouvrir le notebook :

```bash
jupyter notebook
```

3. Exécuter les cellules dans l'ordre afin de :

   * calculer les indicateurs ;
   * détecter les missions ;
   * générer le dashboard interactif `dashboard_associes.html`.

---

## Référentiel sémantique des KPI

Afin de faciliter la réutilisation des indicateurs par d'autres équipes (Data, BI ou Produit), nous proposons le référentiel sémantique suivant.

| KPI                              | Définition                                      | Méthode de calcul                                                                 | Utilité métier                                                                                                                                  |
| -------------------------------- | ----------------------------------------------- | --------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------- |
| **CA mensuel**                   | Chiffre d'affaires réalisé chaque mois          | Somme des écritures des comptes de produits (classe 7) agrégée par mois           | Suivre l'évolution de l'activité au cours de l'exercice.                                                                                        |
| **CA annuel**                    | Chiffre d'affaires total de l'exercice          | Somme des écritures des comptes de produits (classe 7) par entreprise             | Mesurer le niveau d'activité de chaque entreprise et servir de base au calcul du DSO.                                                           |
| **Trésorerie**                   | Position de trésorerie de l'entreprise          | Solde des principaux comptes de trésorerie (banques, caisse et comptes assimilés) | Identifier les entreprises pouvant rencontrer des tensions de liquidité ou disposant d'excédents de trésorerie.                                 |
| **Créances clients**             | Montants restant à encaisser auprès des clients | Solde des comptes clients (411)                                                   | Évaluer les retards d'encaissement et alimenter le calcul du BFR et du DSO.                                                                     |
| **Dettes fournisseurs**          | Montants restant à payer aux fournisseurs       | Solde des comptes fournisseurs (401)                                              | Évaluer les dettes d'exploitation et participer au calcul du BFR.                                                                               |
| **BFR**                          | Besoin en Fonds de Roulement                    | Créances clients − Dettes fournisseurs                                            | Mesurer le besoin de financement du cycle d'exploitation et détecter les entreprises nécessitant un accompagnement.                             |
| **DSO (Days Sales Outstanding)** | Délai moyen de paiement des clients             | (Créances clients / CA annuel) × 365                                              | Identifier les entreprises présentant des délais de paiement élevés et susceptibles de bénéficier d'une mission d'optimisation du recouvrement. |

### Objectif

Ce référentiel fournit une définition commune des indicateurs utilisés dans le projet. Il facilite leur compréhension, leur réutilisation et leur partage entre les équipes Data, BI et les utilisateurs métier, tout en garantissant une interprétation cohérente des résultats.


## Résultat

Le projet transforme les écritures comptables d'un FEC en un outil d'aide à la décision permettant d'identifier rapidement les entreprises à fort potentiel de missions de conseil grâce à une approche combinant analyse de données, règles métier et visualisation interactive.
