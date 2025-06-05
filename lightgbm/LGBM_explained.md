# Fonctionnement de LightGBM 

LightGBM est un modèle basé sur le Gradient Boosting, et represente une excellente alternative à XGBoost. 
LightGBM est un modèle basé sur les _arbres de décision_, et est utilisé pour la régression, classification et autres tâches. 

## Gradient Boosting

Le gradient boosting est une méthodologie de Machine Learning, où l'idée est d'utiliser plusieurs modèles utilisant 
le même algorithme d'apprentissage, et de combiner ces modèles indépendants pour créer un modèle plus puissant.
Ces modèles sont très dependants les uns des autres, car sont construits de manière séquentielle. En général ce sont des _arbres de décision_
(les Random Forests créent des arbres de décision de manière indépendante en utilisant le _bagging_ _(bootstrap aggregating)_

### Etapes
1. Créer un modèle de base, qui sera entraîné sur les données.
2. A partir de ce modèle, on va construire un deuxième pour corriger les erreurs du premier. Les erreurs sont minimisées à
   l'aide d'un algorithme de _descente de gradient_. Chaque arbre ajouté va compenser les erreurs commises par le précédent.
3. Cette procédure se poursuit et on rajouté des modèles jusqu'à ce que le modèle prédit correctement les labels, ou que le nombre maximal des modèls soit atteint.
4. Les prédictions du dernier modèle ajouté seront les prédictions globales fournis par les anciens modèles d'arbres.

## Fonctionnement de LightGBM
