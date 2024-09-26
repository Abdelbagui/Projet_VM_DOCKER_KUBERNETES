# Documentation de Conteneurisation du Projet

## 1. Introduction

Cette documentation décrit le processus de conteneurisation d'un projet utilisant Docker. Le projet est constitué de plusieurs services interconnectés, notamment WordPress, une base de données MySQL, un exportateur MySQL, un exportateur Node, Prometheus et Grafana.

## 2. Composants du Projet

### 2.1. Services

- **WordPress**: Application de gestion de contenu (CMS) pour le développement de sites web.
- **MySQL**: Système de gestion de base de données relationnelle utilisé pour stocker les données de WordPress.
- **MySQLd Exporter**: Outil pour exporter des métriques de performance de MySQL vers Prometheus.
- **Node Exporter**: Outil pour exporter des métriques du système d'exploitation vers Prometheus.
- **Prometheus**: Outil de monitoring et d'alerte qui collecte et stocke les métriques.
- **Grafana**: Plateforme d'analyse et de visualisation de données qui se connecte à Prometheus pour afficher les métriques.

### 2.2. Arborescence des Dossiers

Voici la structure de répertoires du projet :

```
projet_VM_DOCKER_KUBERNETES/
├── docker-compose.yml
├── prometheus.yml
├── my.cnf
└── ...
```

- **docker-compose.yml**: Fichier de configuration pour déployer tous les services.
- **prometheus.yml**: Configuration pour Prometheus.
- **my.cnf**: Fichier de configuration pour l'exportateur MySQL.

## 3. Pré-requis

Avant de commencer, assurez-vous d'avoir installé :

- [Docker](https://docs.docker.com/get-docker/)
- [Docker Compose](https://docs.docker.com/compose/install/)

## 4. Installation

### 4.1. Cloner le dépôt

Clonez le dépôt du projet à l'aide de la commande suivante :

```bash
git clone https://github.com/Abdelbagui/Projet_VM_DOCKER_KUBERNETES.git
cd Projet_VM_DOCKER_KUBERNETES
```

### 4.2. Configuration de l'environnement

Assurez-vous que tous les fichiers de configuration (comme `my.cnf` et `prometheus.yml`) sont correctement configurés selon vos besoins.

### 4.3. Lancer les services

Dans le répertoire du projet, exécutez la commande suivante pour démarrer tous les services :

```bash
docker-compose up -d
```

Cette commande va télécharger les images nécessaires et lancer les conteneurs en arrière-plan.

## 5. Utilisation

### 5.1. Accéder à WordPress

Une fois les conteneurs en cours d'exécution, vous pouvez accéder à WordPress à l'adresse suivante :

```
http://localhost:8080
```

### 5.2. Accéder à Grafana

Pour accéder à Grafana, rendez-vous à l'adresse suivante :

```
http://localhost:3000
```

Identifiants par défaut :
- **Nom d'utilisateur**: `admin`
- **Mot de passe**: `admin` (peut être modifié dans le fichier `docker-compose.yml`)

### 5.3. Accéder à Prometheus

Pour accéder à Prometheus, utilisez l'URL suivante :

```
http://localhost:9090
```

## 6. Configuration de Prometheus

Le fichier `prometheus.yml` doit inclure des configurations pour surveiller l'exportateur MySQL et Node Exporter. Un exemple de configuration pourrait ressembler à ceci :

```yaml
global:
  scrape_interval: 15s

scrape_configs:
  - job_name: 'mysqld-exporter'
    static_configs:
      - targets: ['mysqld-exporter:9104']

  - job_name: 'node-exporter'
    static_configs:
      - targets: ['node-exporter:9100']
```

## 7. Résolution des Problèmes

### 7.1. Problèmes d'accès à MySQL

Si vous rencontrez des erreurs d'authentification, vérifiez que les identifiants dans le fichier `docker-compose.yml` sont corrects.

### 7.2. Conteneurs en échec

Si un conteneur ne démarre pas correctement, consultez les logs avec la commande suivante :

```bash
docker-compose logs <service-name>
```

Remplacez `<service-name>` par le nom du service concerné (par exemple, `db` ou `mysqld-exporter`).

## 8. Conclusion

Cette documentation fournit un guide complet sur la conteneurisation de votre projet avec Docker. Vous pouvez maintenant gérer vos services de manière plus efficace et surveiller leurs performances à l'aide de Prometheus et Grafana.

Pour toute question ou problème, n'hésitez pas à consulter la documentation officielle de Docker ou à poser vos questions sur des forums de développeurs.
