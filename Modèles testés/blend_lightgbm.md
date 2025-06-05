# Blending de modèles LightGBM

## Objectif 
Nous avons testé une stratégie de **blending(moyenne des prédictions)** entre :
- Le **LightGBM 'optimisé' de base** : notre meilleur modèle sans pondération
- Un **LightGBM pondéré** : modèle avec 'class_weight' ajusté manuellement pour renforcer les classes sous_représentées.

## Analyse préalable
En analysant les labels de la base d'entraînement, nous avons remarqué que certaines classes étaient **moins fréquentes** :

"""Insertion de graphique ? """

Mais surtout, dans les **prédictions**, ces classes peu fréquentes étaient **encore moins souvent prédites**, ce qui est révelateur d'un **biais de prédiction vers les classes majoritaires**.

## Analyse des matrices de confusion

**Recall** = mesure la capacité du modèle à retrouver toutes les occurrences d'une classe. Parmi tous les élements qui devraient être classés dans la classe , combien le modèle a-t-il réellement retrouvés.
**Precision** = parmi ce que je prédis, est-ce que j'ai raison ? 
**Modèle sans Pondération :**
- Forte concentration sur 2, 4
- Peu de prédictions en 0 et 5
- Bonne précision globale mais faible **rappel(recall) = Vrai Positifs/(Vrai Positifs + Faux Négatifs)** sur les classes minoritaires
