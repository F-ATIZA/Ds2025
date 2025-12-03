# AKHARAZ FATIMA ZAHRA
## Photo personnelle

<img src="IMG_5552.png" style="height:464px;margin-right:432px"/>

**Numéro d'étudiant** : 24010341

**Classe** : CAC1

<br clear="left"/>
[compte_rendu_fifa20.md](https://github.com/user-attachments/files/23911189/compte_rendu_fifa20.md)

# Compte rendu d’analyse et modélisation – FIFA 20 Player Dataset

## 1. Introduction

L’objectif de ce travail est d’analyser le dataset complet des joueurs de FIFA 20 et de développer un modèle de machine learning capable de prédire la note globale d’un joueur (*overall*).  
Cette base de données contient des informations démographiques, physiques, financières et techniques.

La problématique principale est :

> **Quels facteurs influencent la performance globale d’un joueur et dans quelle mesure peut-on la prédire via un modèle de régression ?**

Objectifs :
- Préparer et nettoyer le dataset.
- Explorer les données.
- Tester plusieurs modèles de régression.
- Évaluer leurs performances (R², RMSE).
- Discuter des limites et pistes d’amélioration.

---

## 2. Méthodologie

### 2.1 Nettoyage et préparation des données

**Principales étapes :**

- Suppression des colonnes inutiles (identifiants, URL…).
- Imputation des valeurs manquantes (moyenne).
- Conversion des dates (ex : `joined` → `joined_year`).
- Conversion des ratings textuels “68+2” → 70.
- Encodage :
  - One-Hot Encoding (faible cardinalité).
  - Frequency Encoding (haute cardinalité : *club*, *nationality*).
  - Encodage binaire des colonnes multi-valeurs (positions, traits).

Ces choix permettent d’éviter la sparsité, réduire la dimensionnalité et améliorer la robustesse du modèle.

### 2.2 Split des données

- Cible : **overall**  
- Ensemble d’entraînement : 80%  
- Ensemble de test : 20%

### 2.3 Modèles utilisés

- **RandomForestRegressor**
- **GradientBoostingRegressor**
- **Ridge Regression**

### 2.4 Validation croisée

Validation **K-Fold (k=5)** pour évaluer la stabilité des modèles et éviter les biais liés à un seul split.

---

## 3. Résultats & Discussion

### 3.1 Performances des modèles

| Modèle | R² (moy. ± std) | RMSE (moy. ± std) |
|--------|------------------|--------------------|
| RandomForest | Bon R², faible variance | Bon RMSE |
| GradientBoosting | Généralement le meilleur | RMSE plus faible |
| Ridge | Moins performant | RMSE plus élevé |

Le **Gradient Boosting** est globalement le plus performant.

### 3.2 Analyse des erreurs

Les modèles prédisent bien les joueurs “moyens”.  
Les erreurs augmentent pour les joueurs **exceptionnels**, car ils sont rares dans le dataset.

### 3.3 Principales observations exploratoires

- Relation positive *âge → overall*, avec plateau après 28–30 ans.
- Les attributs techniques (shooting, dribbling…) sont très corrélés à `overall`.
- Salaire et valeur de marché sont aussi fortement corrélés.
- Forte multicolinéarité entre attributs techniques.

---

## 4. Conclusion

### Limites du modèle

- Corrélation forte entre variables → difficulté pour les modèles linéaires.
- Présence de caractéristiques subjectives (potential).
- Difficulté à prédire les très hauts niveaux.
- Encodage des positions perfectible.

### Pistes d’amélioration

1. Tester XGBoost ou LightGBM.
2. Ajouter des variables dérivées (scores offensifs/défensifs).
3. Optimiser les hyperparamètres (GridSearchCV).
4. Modéliser séparément par poste (défenseur, milieu, attaquant).
5. Standardiser les données pour améliorer les modèles linéaires.

---
