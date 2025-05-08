# Data-Analysis-Projects
## Projet 1: Étude de cas : Analyse des tendances d’achats aux États-Unis
## 🎯 Objectif business

Identifier les profils clients les plus rentables et les catégories de produits les plus performantes selon les États, tranches d’âge et périodes d’achat, afin d’optimiser les actions marketing et la gestion des stocks.

## 🔍 Étape 1 : Nettoyage des données
Colonnes à nettoyer :

- email → vérifier doublons, anonymiser si besoin

- purchase date → convertir en format datetime

- customer name → enlever les doublons si des clients apparaissent plusieurs fois

## 📊 Étape 2 : Analyse exploratoire (EDA)
➤ 1. Vue globale
- Nombre total de transactions

- Chiffre d’affaires global

- Répartition par genre (gender)

- Répartition par âge (customer age) → créer des tranches d’âge : 18–30, 30–60, etc.

➤ 2. Analyse par produit
- Top 10 des produits les plus vendus (en volume et CA)

- Top 5 des catégories de produits

- Produits avec valeur moyenne par transaction la plus élevée

➤ 3. Analyse géographique
- Top États par nombre de ventes

- États avec panier moyen le plus élevé

➤ 4. Analyse temporelle
- Mois ou semaine avec pic de ventes

- Comparaison des ventes selon jours de la semaine

- Ventes par saison (printemps, été...)

➤ 5. Analyse démographique
- Habitudes d’achats par genre

- Tranches d’âge les plus rentables

- Existe-t-il une corrélation entre âge et montant dépensé ?

## 📈 Étape 3 : Visualisations (avec Python / Power BI / Tableau)
- Histogramme : répartition âge

- Heatmap : produit × état

- Boxplot : panier moyen par tranche d’âge

- Courbe de tendance des ventes mensuelles

- Pie chart : part de chaque catégorie produit

## 💡 Étape 4 : Insights et recommandations
Insight	Recommandation
Les 26–35 ans achètent surtout des articles électroniques	Cibler cette tranche avec promos personnalisées
Le panier moyen est le plus élevé le dimanche	Lancer des offres spéciales "Sunday Deals"
La Californie génère 30% du CA mais seulement 15% des transactions	Mettre en place des offres de fidélité pour encourager plus d’achats

## 🛠️ Outils recommandés
- Python (Pandas, Matplotlib, Seaborn)

- Excel ou Google Sheets

- Power BI 
