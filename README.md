
# Configuration Docker pour un projet PHP avec Apache et MySQL

Ce projet utilise Docker pour configurer un environnement de développement PHP avec Apache et MySQL. Il inclut un serveur Apache qui sert des fichiers PHP via PHP-FPM et une base de données MySQL.

## Contenu du projet

- **Dockerfile Apache** : Configure Apache avec les modules `proxy` et `proxy_fcgi` pour rediriger les fichiers PHP vers PHP-FPM.
- **VirtualHost Apache** : Configuration du serveur Apache pour un projet en local avec un `DocumentRoot` défini sur `/var/www/html/` et une gestion des fichiers PHP via FastCGI.
- **Dockerfile PHP-FPM** : Installe PHP 8.4-FPM avec les extensions MySQL requises.
- **docker-compose.yaml** : Définit les services Docker pour PHP-FPM, Apache et MySQL.

## Prérequis

- [Docker](https://www.docker.com/get-started) installé sur votre machine
- [Docker Compose](https://docs.docker.com/compose/install/) pour gérer les services

## Structure des fichiers

```
├── apache/
│   ├── Dockerfile       # Configuration Docker pour Apache
│   └── httpd.conf       # Configuration du VirtualHost Apache
├── php/
│   └── Dockerfile       # Configuration Docker pour PHP-FPM
├── mysql/               # Volume MySQL pour les données persistantes
└── docker-compose.yaml  # Configuration des services Docker
```

## Installation

1. Clonez ce repository.

2. Modifiez le fichier `docker-compose.yaml` pour adapter les valeurs des variables d'environnement MySQL si nécessaire.

4. Construisez et démarrez les services Docker :

   ```bash
   docker-compose up --build
   ```

   Cela va créer et lancer les services suivants :
   - **php-fpm** : Service PHP-FPM pour exécuter le code PHP.
   - **apache** : Serveur Apache servant les fichiers PHP via PHP-FPM.
   - **mysql** : Base de données MySQL avec les informations d'accès spécifiées dans le fichier `docker-compose.yaml`.
   - **Dossier App** : Dossier où déposer les fichiers PhP.

## Détails des services

### Apache

Le serveur Apache est configuré pour servir un site local sur le port 8080. Il inclut les modules `proxy` et `proxy_fcgi` pour gérer la redirection des fichiers PHP vers PHP-FPM.

Le fichier de configuration du VirtualHost (`httpd.conf`) inclut :

- **DocumentRoot** : `/var/www/html/`
- **Gestion des fichiers PHP** : Redirigés vers PHP-FPM via FastCGI
- **Logs** : `error.log` et `access.log`

### PHP-FPM

Le service PHP-FPM est configuré avec PHP 8.4 et les extensions MySQL (`mysqli`, `pdo`, `pdo_mysql`) sont installées pour permettre la connexion à la base de données MySQL.

### MySQL

Le service MySQL utilise une image Docker officielle de MySQL. Il expose le port 3308 et persiste les données dans le dossier `./mysql`. Les variables d'environnement pour MySQL sont définies dans `docker-compose.yaml` :

- `MYSQL_ROOT_PASSWORD`
- `MYSQL_DATABASE`
- `MYSQL_USER`
- `MYSQL_PASSWORD`

## Accès

- **Apache** : Accessible sur [http://localhost:8080](http://localhost:8080)
- **MySQL** : Accessible sur le port 3308 avec les identifiants spécifiés dans le fichier `docker-compose.yaml`.

## Logs

- **Apache** :
  - `error.log` : `/usr/local/apache2/logs/error.log`
  - `access.log` : `/usr/local/apache2/logs/access.log`

