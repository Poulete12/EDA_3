# Analyse multivariée des élections présidentielles : Méthodes PCA et CCA

**Auteurs :** Asso et Antony  
**Date :** 2025  
**Cours :** Homework III - SVD methods and Elections Data

## Description du projet

Ce projet propose une analyse multivariée approfondie des élections présidentielles parisiennes de 2007 à 2022 en mobilisant deux méthodes statistiques principales :
- **PCA (Principal Component Analysis)** : pour explorer la structure politique de chaque élection
- **CCA (Canonical Correlation Analysis)** : pour mesurer la stabilité électorale entre scrutins consécutifs

L'objectif est de comprendre l'évolution du paysage politique parisien sur quinze années à travers l'analyse des résultats par bureau de vote.

## Objectifs

1. **Extraction et nettoyage** des données électorales multi-formats (Parquet/Excel)
2. **Analyse PCA** pour révéler les structures politiques et leur évolution temporelle
3. **Analyse CCA** pour quantifier la stabilité électorale entre scrutins
4. **Identification** des bureaux de vote les plus stables/instables
5. **Quantification** de l'évolution du paysage électoral parisien

## Données

### Sources
- **OpenData Paris** (opendata.paris.fr)
- **data.gouv.fr**
- **Formats** : Parquet (élections européennes, présidentielles, régionales) et Excel (municipales, législatives)

### Périmètre temporel
- **Élections présidentielles** : 2012, 2017, 2022 (1er tour)
- **Granularité** : Par bureau de vote parisien
- **Variables** : Résultats regroupés en 7 familles politiques

### Classification politique
Les candidats sont regroupés en sept familles politiques :
- **Extrême gauche** : EXG
- **Gauche** : COM, SOC, LFI
- **Écologistes** : ECO
- **Centre** : ENS
- **Droite** : LR, DVD
- **Extrême droite** : RN, REC
- **Divers** : DSV, REG

## Structure du projet

```
├── Data/
│   ├── Election/
│   │   ├── parquet/          # Données électorales format Parquet
│   │   ├── Municipale/       # Données municipales (Excel)
│   │   └── Legislative/      # Données législatives (Excel)
│   └── Nuance/              # Fichiers CSV de mapping candidat → famille
├── DataClean/               # Données nettoyées (format Parquet)
├── rapport.qmd             # Rapport principal (Quarto)
├── rapport.html            # Rapport généré
└── README.md               # Ce fichier
```

## Méthodologie

### 1. Pipeline d'extraction
- **Formats multiples** : Traitement adaptatif Parquet (arrow) et Excel (readxl)
- **Standardisation** : Harmonisation des noms de colonnes et structures
- **Mapping** : Correspondance candidat → famille politique via CSV

### 2. Nettoyage des données
- Suppression des colonnes non-pertinentes (métadonnées, géolocalisation)
- Harmonisation des variables (bulletins nuls/blancs)
- Gestion des valeurs manquantes (remplacement par 0)
- Conversion des candidats individuels en familles politiques

### 3. Analyses statistiques

#### PCA (Analyse en Composantes Principales)
- **Standardisation** des variables par famille politique
- **Visualisation** : graphiques des valeurs propres, variables et individus
- **Interprétation** : structures politiques sous-jacentes

#### CCA (Analyse des Corrélations Canoniques)
- **Normalisation** : conversion en pourcentages par bureau
- **Jointure** : appariement des données par identifiant de bureau
- **Stabilité** : mesure de fidélité électorale entre scrutins
- **Identification** : bureaux de vote instables

## Dépendances R

```r
# Packages principaux
library(CCA)           # Analyse des corrélations canoniques
library(tidyverse)     # Manipulation de données
library(arrow)         # Lecture fichiers Parquet
library(readxl)        # Lecture fichiers Excel
library(factoextra)    # Visualisation PCA
library(corrplot)      # Matrices de corrélation
library(knitr)         # Tableaux formatés
```

## Installation et exécution

### Prérequis
- R (≥ 4.0)
- RStudio (recommandé)
- Quarto

### Installation des packages
```r
install.packages(c("CCA", "tidyverse", "arrow", "readxl", 
                   "corrplot", "knitr", "factoextra"))
```

### Exécution
1. **Cloner le repository**
```bash
git clone [URL_DU_REPOSITORY]
cd [NOM_DU_PROJET]
```

2. **Lancer l'analyse**
```r
# Dans RStudio
quarto::quarto_render("rapport.qmd")
```

## Auteurs et contact

**Asso et Antony**  
Projet réalisé dans le cadre du cours "SVD methods and Elections Data"  
Date de rendu : 29 mai 2025  
Présentation : 3 juin 2025

## Licence

Ce projet est réalisé dans un cadre académique. Les données électorales utilisées sont publiques et accessibles via les sources mentionnées. 