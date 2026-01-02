# OCR – Projet 7
## Conception, restauration et sécurisation d’une base de données NoSQL

Projet réalisé dans le cadre de la formation **Data Engineer – OpenClassRooms**  
**Decembre 2025**

---

## Contexte du projet (situation fictive)

L’association NosCités analyse l’impact des plateformes de locations de courte durée sur l’offre de logements à Paris et Lyon. Les données sont collectées par scraping (ex. Airbnb) et stockées sur des serveurs physiques.

Un crash total de la base MongoDB des locations parisiennes est survenu. Une sauvegarde étant disponible, le projet vise à :

restaurer la base de données,

vérifier l’intégrité des données,

fiabiliser et pérenniser l’architecture pour éviter de futurs incidents.

---

## Travail réalisé
### 1.Chargement et analyse des données
Insertion des données scrapées dans MongoDB
Ajout du champ city (Paris / Lyon)
Requêtes d’analyse et de contrôle via Mongo Shell et Polars (Python).

### 3. Visualisation
Connexion de MongoDB à Power BI
Utilisation :
 -  du **MongoDB ODBC Driver**
 -  du **Power BI Connector**
Création de visualisations pour analyser l’offre de logements par ville

### 4. Mise en place d’une architecture distribuée

#### a. Sharding (distribution des données)

* Mise en place d’une **stratégie de sharding** pour répartir les données
* Clé de sharding : `city`
* Répartition logique :

  * **Shard 1** : données de Paris
  * **Shard 2** : données de Lyon

Objectifs :

* Réduction de la charge sur un serveur unique
* Amélioration des performances de requêtage
* Scalabilité horizontale

---

#### b. Réplication avec Replica Sets

* Mise en place de **Replica Sets** pour chaque shard
* Architecture :

  * 1 nœud **Primary** (écritures)
  * 2 nœuds **Secondary** (réplication automatique)
* Répartition géographique simulée entre Paris et Lyon

Objectifs :

* Haute disponibilité
* Tolérance aux pannes
* Prévention des pertes de données en cas de crash

---

### 5. Simulation locale de l’architecture

* Simulation d’une architecture multi‑serveurs en local :

  * Plusieurs instances MongoDB
  * Ports distincts
  * Répertoires de données séparés
* Configuration manuelle des Replica Sets :

  * Initialisation avec `rs.initiate()`
  * Attribution des rôles primary / secondary
* Vérification de la réplication et de la cohérence des données

---

## Résultats et bénéfices

* Base de données restaurée et fonctionnelle après incident
* Données sécurisées grâce à la réplication
* Architecture scalable et résiliente
* Données exploitables pour l’analyse décisionnelle
* Préparation à l’ajout de nouvelles villes ou à une montée en charge

---

## Outils et technologies

* **MongoDB** (NoSQL, sharding, replica sets)
* **Mongo Shell**
* **Python**
* **Polars**
* **Power BI**
* **MongoDB ODBC Driver**
* **Power BI Connector**
* **PowerShell** (lancement multi‑instances MongoDB)

---
