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

# Les requête sql nécessaire

les titres et dates de sortie des films du plus récent au plus ancien: 
SELECT title, releaseDate FROM movies ORDER BY releaseDate DESC;

les noms, prénoms et âges des acteurs/actrices de plus de 30 ans dans l'ordre alphabétique:
SELECT lastName, firstName, TIMESTAMPDIFF(YEAR, birthDate, CURDATE()) AS age FROM actors WHERE TIMESTAMPDIFF(YEAR, birthDate, CURDATE()) > 30 ORDER BY lastName, firstName;


la liste des acteurs/actrices principaux pour un film donné :
SELECT actors.lastName, actors.firstName FROM actors INNER JOIN plays_in ON actors.Id_actors = plays_in.Id_actors INNER JOIN movies ON plays_in.Id_movies = movies.Id_movies WHERE movies.title = 'Viking’' AND plays_in.role = 'main_actor';

la liste des films pour un acteur/actrice donné:
SELECT movies.title
FROM movies
INNER JOIN plays_in ON movies.Id_movies = plays_in.Id_movies
INNER JOIN actors ON plays_in.Id_actors = actors.Id_actors
WHERE actors.lastName = 'Brenna';

ajouter un film:

INSERT INTO movies (title, length, releaseDate)
VALUES ('Nouveau film', '02:30:00', '2023-10-05');

ajouter un acteur/actrice:

INSERT INTO actors (lastName, firstName, birthDate)
VALUES ('Nouvel', 'Acteur', '1990-01-01');

modifier un film:

UPDATE movies
SET title = 'Nouveau titre', releaseDate = '2023-12-31'
WHERE title = 'Nom du film';

supprimer un acteur/actrice:

DELETE FROM actors
WHERE lastName = 'Nom de l'acteur';

afficher les 3 derniers acteurs/actrices ajouté(e)s:

SELECT lastName, firstName, birthDate
FROM actors
ORDER BY Id_actors DESC
LIMIT 3;








