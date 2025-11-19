📝 Compte Rendu — Descriptif de la Base de Données Wine Quality (White)
📌 1. Introduction

La base de données Wine Quality provient du UCI Machine Learning Repository.
Elle contient des informations sur des vins blancs portugais, décrits par des mesures physico-chimiques ainsi qu’un score de qualité attribué par des experts.

Elle est couramment utilisée pour des tâches de régression ou classification, notamment l’apprentissage d’un modèle permettant de prédire la qualité du vin.

📦 2. Chargement du Dataset
from ucimlrepo import fetch_ucirepo

wine_quality = fetch_ucirepo(id=186)

X = wine_quality.data.features
y = wine_quality.data.targets

print(wine_quality.metadata)
print(wine_quality.variables)

📊 3. Description Générale

Nombre total d’observations : 4 898 vins blancs

Nombre de variables explicatives : 11

Variable cible : quality (score de 0 à 10)

Ces données décrivent les propriétés physico-chimiques du vin et son appréciation par des dégustateurs.

🧪 4. Les Variables (Features)
Variable	Description
fixed acidity	Acide fixe (g/dm³)
volatile acidity	Acide volatil (g/dm³)
citric acid	Acide citrique (g/dm³)
residual sugar	Sucre résiduel (g/dm³)
chlorides	Chlorures (g/dm³)
free sulfur dioxide	SO₂ libre (mg/dm³)
total sulfur dioxide	SO₂ total (mg/dm³)
density	Densité (g/cm³)
pH	Acidité du vin
sulphates	Sulfates (g/dm³)
alcohol	Teneur en alcool (%)
quality (cible)	Score de qualité (0 à 10)
🎯 5. Transformation de la Variable Cible

Pour former un problème de classification binaire, la qualité est regroupée :

Y = [0 if val <= 5 else 1 for val in y["quality"]]


0 = vin de mauvaise qualité

1 = vin de bonne qualité

Cette transformation est standard dans les études utilisant ce dataset.

📈 6. Analyse Statistique et Visualisations
🔹 6.1 Boxplots

Ils révèlent :

de fortes différences d’échelles entre variables,

la présence possible de valeurs extrêmes,

des distributions très asymétriques (ex : residual sugar).

🔹 6.2 Matrice de Corrélation

Les corrélations les plus fortes observées sont :

density ↗ residual sugar

free sulfur dioxide ↗ total sulfur dioxide

alcohol ↘ density

Ces observations justifient :

l’utilisation d’une normalisation avant classification,

une attention particulière lors de la sélection des modèles sensibles aux distances.

⚙ 7. Préparation des Données
✔ Séparation en trois ensembles
from sklearn.model_selection import train_test_split

Xa, Xt, Ya, Yt = train_test_split(X, Y, test_size=1/3, stratify=Y)
Xa, Xv, Ya, Yv = train_test_split(Xa, Ya, test_size=0.5, stratify=Ya)


Train (Da) : apprentissage

Validation (Dv) : choix des hyperparamètres

Test (Dt) : mesure finale

La stratification garantit la même proportion de classes dans chaque ensemble.

✔ Normalisation
from sklearn.preprocessing import StandardScaler

sc = StandardScaler().fit(Xa)
Xa_n = sc.transform(Xa)
Xv_n = sc.transform(Xv)


Objectifs :

annuler l'effet des différences d’échelle,

améliorer la performance des modèles basés sur la distance (k-NN).

🧠 8. Modèle de Classification : k-Nearest Neighbors (k-NN)
Étapes réalisées :

Test du k-NN pour k = 3

Calcul de l’erreur sur le validation set

Recherche du k optimal via un balayage de k ∈ [1, 40]

Cette approche permet :

d’observer les phénomènes de surapprentissage pour les petits k,

d’identifier la zone où le modèle généralise le mieux.

Choix du meilleur k
err_min, idx_opt = error_val.min(), error_val.argmin()
k_star = k_vector[idx_opt]

🧾 9. Conclusion

La base de données Wine Quality (White) :

est complète, propre et bien structurée ;

permet des analyses statistiques riches ;

met en évidence l’importance de la normalisation ;

constitue un excellent support pédagogique pour :

la classification supervisée,

l’analyse exploratoire,

la validation croisée,

la sélection d’hyperparamètres.

Elle représente un cas d’étude idéal pour l’apprentissage du modèle k-NN et des techniques de prétraitement.
