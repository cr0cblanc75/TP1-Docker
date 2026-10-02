# TP1 — Application Docker multi-conteneurs

## Description

Ce projet est une application composée de **3 services Docker** :

- **Frontend** : application web servie avec Apache/httpd
- **Backend** : API de l'application
- **Database** : base de données PostgreSQL

Les trois services communiquent entre eux grâce à **Docker Compose** et à des réseaux Docker dédiés.

Les images Docker sont disponibles sur Docker Hub :

- `eugenelallain/tp1-front:1.0`
- `eugenelallain/tp1-backend-api:1.0`
- `eugenelallain/tp1-db:1.0`

---

## Architecture

```text
                           Frontend
                               │
                        frontend-network
                    ┌─────────────────────┐
                    │      Frontend       │
                    │       httpd         │
                    │      port 80        │
                    └──────────┬──────────┘
                               │
                        backend-network
                               │
                    ┌──────────▼──────────┐
                    │       Backend       │
                    │        API          │
                    └──────────┬──────────┘
                               │
                        backend-network
                               │
                    ┌──────────▼──────────┐
                    │      Database       │
                    │     PostgreSQL      │
                    └─────────────────────┘

                    
```

### Réseaux

Deux réseaux Docker sont utilisés :

- `frontend-network` : réseau dédié au frontend
- `backend-network` : permet la communication entre le frontend, le backend et la base de données

### Ordre de démarrage

Docker Compose utilise `depends_on` afin de démarrer les services dans l'ordre :

```text
Database
    ↓
Backend
    ↓
Frontend
```

---

## Prérequis

Pour lancer le projet, il faut avoir installé :

- [Docker](https://www.docker.com/)
- Docker Compose, inclus dans les versions récentes de Docker Desktop

Vérifier l'installation :

```bash
docker --version
docker compose version
```

---

## Installation

### 1. Cloner le projet

```bash
git clone <URL_DU_REPOSITORY>
```

Puis entrer dans le dossier :

```bash
cd TP1-Docker
```

---

## 2. Télécharger les images Docker

Les images sont hébergées sur Docker Hub.

Pour les télécharger manuellement :

```bash
docker compose pull
```
or
```bash
docker compose build
```

Cette commande récupère automatiquement les trois images :

```text
eugenelallain/tp1-front:1.0
eugenelallain/tp1-backend-api:1.0
eugenelallain/tp1-db:1.0
```

---

## 3. Lancer le projet

Une fois les images téléchargées :

```bash
docker compose up -d
```

Docker démarre alors les trois conteneurs et crée automatiquement les réseaux et le volume nécessaires.

Pour vérifier que les conteneurs fonctionnent :

```bash
docker compose ps
```

---

## Accéder à l'application

Le frontend est exposé sur le port `80` de la machine.

L'application est donc accessible à l'adresse :

```text
http://localhost
```

---

## Arrêter le projet

Pour arrêter les conteneurs :

```bash
docker compose down
```

Le volume PostgreSQL n'est pas supprimé par cette commande. Les données de la base sont donc conservées.

Pour supprimer également le volume :

```bash
docker compose down -v
```

**Attention :** cette commande supprime les données persistées de PostgreSQL.

---

## Gestion des images

Les trois images utilisées par le projet sont :

| Service  | Image Docker                        |
| -------- | ----------------------------------- |
| Frontend | `eugenelallain/tp1-front:1.0`       |
| Backend  | `eugenelallain/tp1-backend-api:1.0` |
| Database | `eugenelallain/tp1-db:1.0`          |

Pour voir les images présentes localement :

```bash
docker images
```

Pour télécharger les dernières images définies dans le `docker-compose.yml` :

```bash
docker compose pull
```

Pour démarrer le projet après la récupération :

```bash
docker compose up -d
```

---

## Persistance des données

PostgreSQL utilise un volume Docker nommé :

```text
postgres-data
```

Il est monté dans le conteneur à :

```text
/var/lib/postgresql/data
```

Cela permet de conserver les données de PostgreSQL lorsque le conteneur est supprimé puis recréé.

Pour voir les volumes :

```bash
docker volume ls
```

---

## Commandes utiles

### Voir les conteneurs

```bash
docker compose ps
```

### Voir les logs

Tous les services :

```bash
docker compose logs
```

Suivre les logs en temps réel :

```bash
docker compose logs -f
```

Logs d'un service particulier :

```bash
docker compose logs backend
docker compose logs database
docker compose logs httpd
```

### Redémarrer le projet

```bash
docker compose restart
```

### Arrêter le projet

```bash
docker compose down
```

### Télécharger les images

```bash
docker compose pull
```

### Démarrer en arrière-plan

```bash
docker compose up -d
```

---

## Structure du projet

```text
TP1/
│
├── docker-compose.yml
│
├── backend/
│   └── Dockerfile
│
├── db/
│   └── Dockerfile
│
└── http/
    └── Dockerfile
```

Les répertoires `backend`, `db` et `http` contiennent les fichiers nécessaires à la construction des différentes images.

Les images versionnées `1.0` utilisées par le `docker-compose.yml` sont cependant déjà disponibles sur Docker Hub.

---

## Arrêt et nettoyage complet

Pour arrêter les services et supprimer les conteneurs, réseaux et autres ressources créées par Compose :

```bash
docker compose down
```

Pour supprimer également le volume PostgreSQL :

```bash
docker compose down -v
```

Pour repartir complètement de zéro et récupérer les images :

```bash
docker compose down -v
docker compose pull
docker compose up -d
```

---

## Auteur

**Eugene Lallain**

Projet réalisé dans le cadre du TP1 de Docker à l'Efrei - Paris.
