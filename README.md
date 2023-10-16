## streaming-ye

# Etape 1: Préparation de la Base de Données

Commencez par élaborer votre dictionnaire de données pour définir la structure de votre base de données.

créez ensuite le modèle conceptuel de données (MCD), suivi du modèle logique de données (MLD) et enfin du modèle physique de données (MPD).

![Alt text](MCD/MLD/Merise1.png)
![Alt text](MCD/MLD/Merise2.png)

# Étape 2 : Configuration de MySQL avec Docker

Allez sur Docker Hub pour récupérer l'image de MySQL en utilisant la commande suivante : 

```bash docker run --name some-mysql -e MYSQL_ROOT_PASSWORD=my-secret-pw -d mysql:tag ```

# Étape 3 : Création de la Base de Données

Créez votre base de données (BDD) en utilisant MySQL.

# Étape 4 : Remplissage de la Base de Données

Utilisez un jeu de données fictif (mock) pour remplir la base de données avec des données d'exemple.

# Étape 5 : Écriture et Test des Requêtes

Rédigez des requêtes SQL pour interagir avec la base de données, effectuer des opérations de lecture, d'écriture, de mise à jour, etc.
Testez ces requêtes pour vous assurer qu'elles fonctionnent correctement avec votre base de données.

# Les requête sql nécessaire

## les titres et dates de sortie des films du plus récent au plus ancien: 

``` SQL
SELECT title, releaseDate FROM movies ORDER BY releaseDate DESC;
```

## les noms, prénoms et âges des acteurs/actrices de plus de 30 ans dans l'ordre alphabétique:

``` SQL
SELECT lastName, firstName, TIMESTAMPDIFF(YEAR, birthDate, CURDATE()) AS age FROM actors WHERE TIMESTAMPDIFF(YEAR, birthDate, CURDATE()) > 30 ORDER BY lastName, firstName;
```


## la liste des acteurs/actrices principaux pour un film donné :

```SQL
SELECT actors.lastName, actors.firstName FROM actors INNER JOIN plays_in ON actors.Id_actors = plays_in.Id_actors INNER JOIN movies ON plays_in.Id_movies = movies.Id_movies WHERE movies.title = 'Viking’' AND plays_in.role = 'main_actor';
```

## la liste des films pour un acteur/actrice donné:

``` SQL
SELECT movies.title
FROM movies
INNER JOIN plays_in ON movies.Id_movies = plays_in.Id_movies
INNER JOIN actors ON plays_in.Id_actors = actors.Id_actors
WHERE actors.lastName = 'Brenna';
```

## ajouter un film:

``` SQL
INSERT INTO movies (title, length, releaseDate)
VALUES ('Nouveau film', '02:30:00', '2023-10-05');
```

## ajouter un acteur/actrice:
```SQL
INSERT INTO actors (lastName, firstName, birthDate)
VALUES ('Nouvel', 'Acteur', '1990-01-01');
```

## modifier un film:
``` SQL
UPDATE movies
SET title = 'Nouveau titre', releaseDate = '2023-12-31'
WHERE title = 'Nom du film';
```

## supprimer un acteur/actrice:
``` SQL
DELETE FROM actors
WHERE lastName = 'Nom de l'acteur';
```

## afficher les 3 derniers acteurs/actrices ajouté(e)s:
``` SQL
SELECT lastName, firstName, birthDate
FROM actors
ORDER BY Id_actors DESC
LIMIT 3;
```


##  Procedure
``` SQL
DELIMITER //
CREATE PROCEDURE ListMoviesByDirector(IN directorName VARCHAR(50))
BEGIN
  SELECT movies.title, movies.releaseDate
  FROM movies
  INNER JOIN directs ON movies.Id_movies = directs.Id_movies
  INNER JOIN directors ON directs.Id_directors = directors.Id_directors
  WHERE directors.lastName = directorName;
END;'
//
DELIMITER ;
```

CALL ListMoviesByDirector('Nom du réalisateur');
```SQL

DELIMITER //
CREATE TRIGGER UserUpdateTrigger
AFTER UPDATE ON users
FOR EACH ROW
BEGIN
  INSERT INTO archives (updateDate, id_users, oldvalue, newvalue)
  VALUES (NOW(), NEW.Id_users, JSON_OBJECT('firstName', OLD.firstName, 'lastName', OLD.lastName, 'email', OLD.email), JSON_OBJECT('firstName', NEW.firstName, 'lastName', NEW.lastName, 'email', NEW.email));
END;
//
DELIMITER ;
```


# Docker Hub 
https://hub.docker.com/r/yassineelz/streaming-image-ye)https://hub.docker.com/r/yassineelz/streaming-image-ye
 










