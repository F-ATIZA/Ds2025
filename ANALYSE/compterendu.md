## Photo personnelle

<img src="akharazfatimazahra.jpeg" style="height:464px;margin-right:432px"/>

**Numéro d'étudiant** : 24010341

**Classe** : CAC1
[compte_rendu_iris (1).md](https://github.com/user-attachments/files/23912996/compte_rendu_iris.1.md)
# Compte rendu de projet : Classification & Analyse du dataset Iris

## 1. Introduction

**Contexte :**\
Le dataset *Iris* est un jeu de données classique utilisé pour illustrer
des tâches de classification supervisée.\
Il contient des mesures de sépales et pétales de trois espèces d'iris :
*Setosa*, *Versicolor* et *Virginica*.

**Problématique :**\
L'objectif est de comprendre la distribution des variables, de préparer
les données puis de tester différents modèles prédictifs.

**Objectifs :** - Nettoyer et préparer le dataset. - Justifier les choix
méthodologiques. - Entraîner des modèles. - Évaluer leurs performances
(Accuracy, F1, RMSE, ROC-AUC selon les modèles). - Analyser les erreurs
et proposer des pistes d'amélioration.

------------------------------------------------------------------------

## 2. Méthodologie

### 2.1 Prétraitement des données

-   **Suppression de la colonne `Id`** : variable inutile pour
    l'apprentissage supervisé.\
-   **Visualisation exploratoire** pour confirmer la séparation
    naturelle entre les classes.\
-   **Encodage des labels** (`LabelEncoder`) pour convertir les classes
    en valeurs numériques.\
-   **Standardisation** (`StandardScaler`) : normalisation nécessaire
    pour les modèles sensibles aux échelles comme la régression linéaire
    ou les méthodes à régularisation.

### 2.2 Justification des choix techniques

-   **Nettoyage minimaliste** : dataset propre, aucune valeur
    manquante.\
-   **Standardisation** : améliore la convergence et la performance des
    modèles.\
-   **Régression Linéaire & Lasso** : utilisés ici pour étudier les
    liens linéaires entre variables.
    -   *Lasso* permet une sélection automatique des variables via la
        pénalisation L1.\
-   **Split Train/Test** : 75% apprentissage, 25% test pour garantir une
    évaluation honnête.

------------------------------------------------------------------------

## 3. Résultats & Discussion

### 3.1 Modèle Lasso

-   Cross-validation réalisée pour différents hyperparamètres `alpha`.\
-   L'objectif était de minimiser l'erreur absolue moyenne (MAE).\
-   Le modèle n'est pas adapté à une tâche de classification multiclasse
    mais offre un aperçu des relations linéaires.

### 3.2 Régression Linéaire

Exemple réalisé : prédiction de *PetalLengthCm* à partir de
*SepalLengthCm*.\
- Modèle très simple → RMSE relativement élevé car la relation n'est pas
strictement linéaire.\
- Graphiquement, la dispersion indique qu'un modèle plus complexe serait
préférable.

### 3.3 Métriques usuelles (rappel pour un modèle de classification)

*Le code fourni ne va pas jusqu'à l'entraînement complet d'un modèle de
classification. Voici les métriques qui auraient été utilisées :*

-   **Accuracy** : proportion de bonnes prédictions.\
-   **F1-Score** : utile en cas de classes déséquilibrées.\
-   **Matrice de confusion** : visualisation des erreurs par classe.\
-   **ROC-AUC** : applicable surtout en mode un-vs-all.

### 3.4 Analyse des erreurs

-   Les espèces *Versicolor* et *Virginica* sont les plus difficiles à
    distinguer car proches dans l'espace des caractéristiques.\
-   Le choix d'un modèle simple (linéaire) limite la capacité de capture
    des frontières non linéaires entre classes.

------------------------------------------------------------------------

## 4. Conclusion

### Limites du modèle

-   Les modèles testés (Lasso, régression linéaire) ne sont pas adaptés
    à la classification multiclasse.\
-   Relation linéaire insuffisante pour modéliser correctement les
    interactions entre variables.

### Pistes d'amélioration

-   Entraîner de vrais modèles de classification : **SVM**, **Random
    Forest**, **kNN**, **Logistic Regression multinomiale**.\
-   Optimisation des hyperparamètres via **GridSearchCV**.\
-   Ajout de métriques complètes pour analyser la performance.\
-   Exploration de modèles non linéaires pour de meilleures séparations
    entre classes.

------------------------------------------------------------------------

*Document généré automatiquement à partir de l'analyse du code fourni,
sans copier-coller direct du script.*
