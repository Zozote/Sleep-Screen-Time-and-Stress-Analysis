# Bien-être Numérique — Impact du Temps d'Écran sur le Sommeil et le Stress

Projet Kaggle — Master 1 MIASHS, Université Paul Valéry Montpellier III  
**Enzo Nguyen** — Mai 2026

---

## Présentation

Ce projet analyse l'impact du temps d'écran sur la qualité du sommeil et le niveau de stress à partir d'un jeu de données de **15 000 observations** comportant 13 variables comportementales et démographiques. Il suit une démarche en trois temps : état de l'art, identification d'un biais structurel, puis proposition d'une contribution originale — le **STSI** (*Screen Time Sensitivity Index*).

---

## Données

| Fichier | Description |
|---|---|
| `sleep_mobile_stress_dataset_15000.csv` | Données brutes (15 000 observations, 13 variables) |
| `dataset_clean.csv` | Données après nettoyage et winsorisation |
| `dataset_engineered.csv` | Données après feature engineering |
| `selected_features.json` | Variables sélectionnées par vote |

**Variables principales :** identifiant, âge, genre, profession, temps d'écran quotidien, utilisation du téléphone avant le coucher, durée et qualité du sommeil, niveau de stress, consommation de caféine, activité physique, notifications, score de fatigue mentale.

---

## Structure des notebooks

| Notebook | Contenu |
|---|---|
| `00_etat_de_lart.ipynb` | Exploration des données, revue des méthodes de la littérature |
| `02_feature_engineering.ipynb` | Création de variables dérivées (ratios, scores, interactions) |
| `03_feature_selection.ipynb` | Sélection par vote (variance, corrélation, test F, RFE) |
| `04_regression_lineaire.ipynb` | Régression MCO, Ridge, Lasso — durée du sommeil et stress |
| `05_regression_non_lineaire.ipynb` | Forêt aléatoire, Gradient Boosting, SVM RBF + PDP |
| `06_classification_supervisee.ipynb` | Classification du niveau de stress (3 classes) |
| `07_classification_non_supervisee.ipynb` | ACP, K-means, DBSCAN — profils d'usagers |
| `08_tests_statistiques.ipynb` | Pearson, Spearman, Mann-Whitney, ANOVA, χ², Cramér V |
| `09_biais_et_limites.ipynb` | Test de Chow, test F sur interactions, biais silencieux |
| `10_contribution_nouvelle.ipynb` | Calcul du STSI, quadrant de risque, évaluation |

---

## Contribution originale — STSI

Le **STSI** (*Screen Time Sensitivity Index*) personnalise l'effet du temps d'écran en fonction du profil de chaque individu, en s'appuyant sur les termes d'interaction d'un modèle MCO :

$$\beta^{(i)} = \beta_{\text{base}} + \sum_j \gamma_j \cdot Z_{ij}$$

$$\text{STSI}_i = s_i \cdot \max(0,\; -\beta^{(i)})$$

Ce cadre permet d'identifier une **population silencieuse** (faible temps d'écran mais haute sensibilité) que les modèles homogènes de l'état de l'art ne peuvent pas détecter.

---

## Rapport

Le mémoire complet est disponible dans `Rapport/memoire_bien_etre_numerique.pdf`.  
Le source LaTeX se trouve dans `Rapport/memoire_bien_etre_numerique.tex`.

---

## Environnement

```
Python 3.x
pandas, numpy, scikit-learn, statsmodels
matplotlib, seaborn
scipy
```
