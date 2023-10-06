## streaming-ye

# Etape 1: Préparation de la Base de Données

Commencez par élaborer votre dictionnaire de données pour définir la structure de votre base de données.

créez ensuite le modèle conceptuel de données (MCD), suivi du modèle logique de données (MLD) et enfin du modèle physique de données (MPD).

# Étape 2 : Configuration de MySQL avec Docker

Allez sur Docker Hub pour récupérer l'image de MySQL en utilisant la commande suivante : 

docker run --name some-mysql -e MYSQL_ROOT_PASSWORD=my-secret-pw -d mysql:tag

# Étape 3 : Création de la Base de Données

Créez votre base de données (BDD) en utilisant MySQL.

# Étape 4 : Remplissage de la Base de Données

Utilisez un jeu de données fictif (mock) pour remplir la base de données avec des données d'exemple.

# Étape 5 : Écriture et Test des Requêtes

Rédigez des requêtes SQL pour interagir avec la base de données, effectuer des opérations de lecture, d'écriture, de mise à jour, etc.
Testez ces requêtes pour vous assurer qu'elles fonctionnent correctement avec votre base de données.


