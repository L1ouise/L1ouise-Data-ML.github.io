--- 
layout: default 
title: "Prédiction du nombre de médailles olympiques — Projet ML end‑to‑end"
---
#Prédiction du nombre de médailles olympiques — Projet ML end‑to‑end
##  Objectif du projet
Construire un modèle capable de prédire le nombre total de médailles qu’un pays remportera aux Jeux Olympiques, en utilisant des données historiques sur les athlètes, les résultats, les disciplines et les pays hôtes.

Ce projet a été réalisé en groupe, mais j’ai personnellement pris en charge **toute la partie prétraitement, feature engineering, fusion des datasets et préparation du dataset final pour la modélisation**.

---

#  1. Compréhension & Exploration des données

### Sources de données utilisées :
- Athlètes olympiques  
- Résultats par épreuve  
- Médailles  
- Pays hôtes  
- Jeux olympiques (été/hiver)

### Travail réalisé :
- Inspection initiale (`df.info()`, `df.head()`)
- Analyse des types, valeurs manquantes, incohérences
- Détection des colonnes bruitées ou inutiles

---

#  2. Nettoyage avancé des données athlètes

###  Transformations clés
- Conversion propre de `athlete_year_birth` en `Int64`
- Nettoyage complexe de `athlete_medals` (extraction numérique, gestion erreurs)
- Création de `has_medal` (feature binaire)
- Extraction de `first_game_year` depuis `first_game`
- Nettoyage de `bio`
- Calcul de `age_at_first_game`

###  Imputation intelligente
- Reconstruction de l’année de naissance manquante via :
  - `first_game_year`
  - `age_at_first_game`
- Remplissage des valeurs restantes par médiane
- Recalcul cohérent de `age_at_first_game`

 **Résultat :** un dataset athlètes propre, cohérent, sans valeurs critiques manquantes.

---

#  3. Préparation des autres datasets
- Chargement et vérification de `medals_clean`, `hosts_clean`, `results_clean`
- Sélection de colonnes pertinentes
- Déduplication intelligente (athlètes, résultats)
- Imputation ciblée :
  - `rank_position` → numérique + remplissage par `max+1`
  - `medal_code`, `num_athletes` → 0
  - `games_participations`, `age_at_first_game` → médiane

---

#  4. Fusion multi‑tables & Feature Engineering massif

##  Fusion
- Fusion `results` + `athletes`
- Ajout des informations des pays hôtes (saison, année)

##  Création de nouvelles features
### Niveau athlète :
- `athlete_experience`  
- `athlete_age`  
- `cumulative_athlete_medals`  

### Niveau discipline :
- `athletes_per_discipline`
- `athletes_per_discipline_sum`
- `disciplines_count`

### Niveau pays‑année :
- `total_medals`, `gold`, `silver`, `bronze`
- `total_athletes`, `medalist_athletes`
- `avg_athlete_experience`, `avg_athlete_age`
- `avg_games_participations`
- `n_disciplines`, `n_events`
- **Features dérivées :**
  - `medals_per_athlete`
  - `medalist_ratio`
  - `gold_ratio`
  - `experience_score`

 **C’est ici que tu montres ton vrai niveau : tu as construit un dataset riche, structuré, et très informatif.**

---

#  5. Construction du dataset final pour la modélisation

### Étapes clés :
- Filtrage des pays invalides
- Sélection des Jeux d’été 2000–2023 pour l’entraînement
- Encodage One‑Hot (`country_3_letter_code`, `season`)
- Split train/test
- Définition :
  - **Features** : toutes les variables enrichies
  - **Target** : `total_medals`

---

#  6. Modélisation — XGBoost Regressor

###  Modèle initial
- Entraînement d’un `XGBRegressor` par défaut
- Évaluation : RMSE, MAE

###  Optimisation
- `RandomizedSearchCV` pour tuner :
  - `n_estimators`
  - `max_depth`
  - `learning_rate`
  - `subsample`
  - `colsample_bytree`
- Sélection du meilleur modèle (`best_xgb_model`)

###  Résultats
- Amélioration significative du RMSE et du MAE
- Modèle plus stable et généralisable

---

#  7. Prédiction pour les JO 2024

### Étapes :
- Construction d’un dataset 2024 cohérent avec les transformations précédentes
- Application du modèle optimisé
- Export des prédictions (`olympics_2024_predictions_2.xlsx`)
- Analyse comparative avec les données réelles 2022
- Sauvegarde du modèle (`.pkl`)

---

#  Compétences démontrées

###  Data Cleaning avancé
- Gestion des incohérences
- Reconstruction de valeurs manquantes
- Harmonisation multi‑sources

###  Feature Engineering
- Création de features athlètes, disciplines, pays
- Agrégations multi‑niveaux
- Ratios, scores, cumulatives

###  Data Engineering
- Pipelines de fusion
- Structuration de datasets complexes
- Export & versioning

###  Machine Learning
- XGBoost
- Hyperparameter tuning
- Évaluation & analyse d’erreurs

###  Outils
Python, Pandas, NumPy, XGBoost, Scikit‑learn, Excel, GitHub

---

#  Lien GitHub
*(ajoute ici le lien vers le repo du projet)*
