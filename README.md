# 📈 Prédiction de la prochaine place de transaction boursière

## 📌 Description
Ce projet a été réalisé dans le cadre du **CFM Data Challenge**  
(*Where will the next trade take place?* – ENS Challenge Data).

L’objectif est de **prédire sur quelle bourse (parmi six) la prochaine transaction aura lieu**, à partir des informations issues des **carnets d’ordres** et des **transactions récentes**.  
Ce problème s’inscrit dans un contexte de **microstructure des marchés financiers**, où la liquidité et la dynamique des ordres jouent un rôle central.

Lien du challenge :  
https://challengedata.ens.fr/participants/challenges/40/

---

## 📊 Données
Les données sont composées de deux sources principales :

### Carnets d’ordres (Order Books)
Pour chaque bourse :
- prix et volumes **ask** (ordres de vente)
- prix et volumes **bid** (ordres d’achat)
- informations disponibles sur les **5 premiers niveaux** du carnet

### Transactions récentes
- 10 dernières transactions
- timestamp
- bourse (venue)
- prix
- quantité échangée

---

## 🎯 Objectif & Métrique
- **Problème de classification multi-classes (6 bourses)**
- Objectif : prédire la **venue** de la prochaine transaction
- Évaluation basée sur le **score du challenge**

---

## 🧠 Méthodologie

### Feature Engineering
Création de variables décrivant la **liquidité**, la **pression acheteur/vendeur** et la dynamique des marchés :

- Fréquence d’apparition des venues :
  - `venue_frequence_10`
  - `venue_frequence_5`
  - `venue_frequence_3`

- Indicateurs de liquidité :
  - `liquidity_bid` (0 à 5)
  - `liquidity_ask` (0 à 5)
  - `total_liquidity` (0 à 5)

- Variables liées au carnet d’ordres :
  - `venue_with_max_bidsize`
  - `venue_with_max_asksize`
  - `venue_with_best_bid`
  - `venue_with_best_ask`
  - `venue_with_min_spread`
  - `venue_with_min_spread1`

- Variables binaires :
  - `matching_venue` : 6 colonnes indiquant si `ask_size = bid_size` pour une venue

Ces features permettent de capturer la structure du marché et le niveau de concurrence entre les différentes bourses.

---

## 🧪 Modèles testés
- **LightGBM (modèle principal)**
  - Score local ≈ **0.505**
  - Score final ≈ **0.4947**
  - Classement : **24ᵉ position** au challenge

- CatBoost  
  - Performances similaires, score final légèrement inférieur

- XGBoost  
  - Résultats proches, mais temps de calcul plus élevé

### Blending
Un **blending de deux modèles LightGBM** a été mis en place :
- un modèle non pondéré, performant sur les classes fréquentes
- un modèle pondéré, plus efficace sur les classes rares

Le blending permet d’obtenir des prédictions **plus équilibrées**, comme observé via la matrice de confusion.

---

## 📈 Évaluation
- Train / test split
- Analyse via **matrice de confusion**
- Étude de l’importance des features
- Tests de pondération des classes (`class_weight`) avec impact limité

---

## 🧠 Interprétations clés
- Plus un actif est liquide, plus il peut être échangé rapidement et à un prix proche du marché
- Un spread faible indique une forte concurrence entre acheteurs et vendeurs
- Un carnet profond (volumes élevés à différents niveaux de prix) est un signe de liquidité
- Le **Trade Price** (différence entre le prix du trade et le mid-price agrégé) reflète la pression acheteur/vendeur

---

## 🔍 Perspectives d’amélioration
- Ajout de nouvelles variables :
  - moyenne du trade price
  - écart-type du trade price
- Étude dynamique du carnet via `ts_last_update`
- Analyse temporelle plus fine de la liquidité

---

## 📂 Contenu du repository
- notebooks et scripts : préparation des données, feature engineering, entraînement et évaluation
- `README.md` : description du projet

---

## 🛠️ Technologies utilisées
- Python
- Pandas, NumPy
- LightGBM
- CatBoost
- XGBoost
- Scikit-learn

---

## 👩‍💻 Auteure
Capucine Brisson  

Projet réalisé dans le cadre du **CFM Data Challenge**

