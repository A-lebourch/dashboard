# Setup du Projet Home Dashboard

## Prérequis
- **Docker** installé sur ton PC : [Docker installation guide](https://docs.docker.com/get-docker/)
- **Git** installé : [Git installation guide](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git)
- **Node.js** et **npm** installés : [Node.js installation guide](https://nodejs.org/)

## Étapes de Configuration

### 1. **Cloner le projet**

Clone le repository dans le dossier où tu veux travailler :

```bash
git clone <URL_REPO>
cd home-dashboard
```

### 2. Initialiser les dossiers du projet
#### Backend (Flask)
- Va dans le dossier backend :
    ```bash
    cd backend
    ```

- Crée un environnement virtuel Python et active-le :
    ```bash
    python3 -m venv venv
    source venv/bin/activate 
    ```

- Installe les dépendances Python :
    ```bash
    pip install -r requirements.txt
    ```

- Lance l'application Flask pour tester :
    ```bash
    python app.py
    ```

#### Frontend (Vue.js)
- Va dans le dossier frontend :
    ```bash
    cd frontend
    ```

- Installe les dépendances de Vue.js :
    ```bash
    npm install
    ```

- Lance l'application Vue.js pour tester :
```bash
npm run dev
```

#### MQTT (Mosquitto)
- Va dans le dossier mqtt :
    ```bash
    cd mqtt
    ```
    Aucune configuration nécessaire, le service MQTT utilise l'image Docker officielle de Mosquitto.

### 3. Configurer Docker avec Docker Compose
1. Créer le fichier .gitignore
    Crée un fichier .gitignore à la racine et ajoute ce contenu :
    ```gitignore
    # Python
    __pycache__/
    *.pyc
    *.pyo
    .venv/
    venv/
    .env

    # Node.js
    node_modules/
    npm-debug.log
    yarn-error.log
    .npm/
    .yarn/

    # Vue.js
    dist/
    .vite/

    # Docker
    .docker/
    docker-compose.override.yml

    # IDEs
    .idea/
    .vscode/

    # Logs
    *.log
    ```

2. Créer un fichier docker-compose.yml
    À la racine du projet, crée le fichier docker-compose.yml avec le contenu suivant :

    ```yaml
    version: '3.8'

    services:
    backend:
        build: ./backend
        ports:
        - "5000:5000"
        volumes:
        - ./backend:/app
        environment:
        - FLASK_ENV=development
        depends_on:
        - mqtt

    frontend:
        build: ./frontend
        ports:
        - "8080:8080"
        volumes:
        - ./frontend:/app
        depends_on:
        - backend

    mqtt:
        image: eclipse-mosquitto:latest
        ports:
        - "1883:1883"
        - "9001:9001"
        volumes:
        - ./mqtt/config:/mosquitto/config
        - ./mqtt/data:/mosquitto/data
        - ./mqtt/log:/mosquitto/log
    ```

3. Créer les Dockerfiles
    Backend (Flask) : Crée un fichier Dockerfile dans le dossier backend avec ce contenu :

    ```dockerfile
    FROM python:3.9-slim

    WORKDIR /app
    COPY requirements.txt .
    RUN pip install -r requirements.txt
    COPY . .

    EXPOSE 5000
    CMD ["python", "app.py"]
    ```

    Frontend (Vue.js) : Crée un fichier Dockerfile dans le dossier frontend avec ce contenu :

    ```dockerfile
    FROM node:16

    WORKDIR /app
    COPY package*.json ./
    RUN npm install
    COPY . .

    EXPOSE 8080
    CMD ["npm", "run", "dev"]
    ```
4. Construire et lancer les conteneurs Docker
    À la racine du projet, lance les services en arrière-plan avec Docker Compose :

    ```bash
    docker-compose up --build -d
    ```
Cela va construire les images et démarrer les services.

4. Accéder à l'application
    Frontend (Vue.js) : Accède à l'application à http://localhost:8080.

    Backend (Flask) : Accède à l'API backend à http://localhost:5000.

    Mosquitto (MQTT) : Accède à l'interface de Mosquitto à http://localhost:9001.

5. Arrêter les services Docker
    Pour arrêter et supprimer les conteneurs Docker :

    ```bash
    docker-compose down
    ```
6. Nettoyage
    Si tu veux supprimer les volumes et les données persistantes des conteneurs :

    ```bash
    docker-compose down --volumes
    ```
## Notes supplémentaires
Modification du .gitignore** : Ajoute tous les fichiers/dossiers temporaires ou spécifiques à ton environnement local à ignorer dans .gitignore`.

Docker sur Raspberry Pi : Si tu passes sur Raspberry Pi, assure-toi que les images Docker sont compatibles avec l'architecture ARM.

Voilà ! Ton projet est maintenant configuré et prêt à fonctionner. Si tu rencontres un problème, fais-le moi savoir. 😊
