# CitoyKaidi - gestion des démarches administratives

CitoyKaidi semble être une plateforme de gestion des démarches administratives en ligne, 
inspirée de services existants comme ceux proposés par le gouvernement français et 
plusieurs autres pays. Voici les éléments clés du projet et 
quelques suggestions pour t'aider à l'adapter :

## Objectif du projet :
Créer une application qui permet aux citoyens de :

- Accéder à leur espace personnel contenant leurs documents.
- Faire des demandes de documents administratifs.
- Suivre l'état de leurs demandes via des notifications.
- Accéder à des informations sur les démarches administratives.

## Fonctionnalités principales :
- Espace membre : Chaque citoyen a un profil avec accès à ses documents.
- Panier : Pour suivre les demandes de documents en cours.
- Moteur de recherche : Permet de trouver rapidement les démarches disponibles.
- Espace de renseignement : Pour guider les utilisateurs sur les démarches.
- Notifications : Pour tenir les citoyens informés de l'état de leurs demandes.
- Blog : Pour publier des actualités liées aux démarches administratives.

## Prérequis

Avant de commencer, assurez-vous d'avoir les éléments suivants installés sur votre machine :

- **Node.js et npm** (ou Yarn)
- **Docker et Docker Compose**
- **WSL 2** (si vous êtes sous Windows)


## Installer WSL et configurer l'environnement: 
- Ouvre PowerShell en mode administrateur.
- Exécute la commande pour installer WSL et une distribution Linux (par exemple, Ubuntu) :
```bash
wsl --install
```
- Une fois installé, redémarre ton ordinateur.
- Après le redémarrage, ouvre Ubuntu ou une autre distribution via WSL.
- Une fois que tu es dans ton terminal WSL (Ubuntu ou autre) :
```bash
sudo apt update && sudo apt upgrade -y
```

## Installer les prérequis sous WSL

Assure-toi que tu as installé WSL 2 sur ta machine. Ensuite, installe les outils nécessaires sous WSL :

- **Docker** : Docker Desktop pour Windows est nécessaire. Docker Desktop doit être configuré pour 
utiliser WSL 2 comme backend. Une fois installé, Docker fonctionne directement dans WSL.
	- Installe Docker Desktop depuis le site officiel.
	- Active l'intégration avec WSL 2 via les paramètres de Docker Desktop (Settings > Resources > WSL Integration), 
	en choisissant ta distribution WSL (par exemple, Ubuntu).
	```bash
	sudo apt install docker.io
	sudo usermod -aG docker $USER
	exit
	```
- **Node.js, npm, Git** : Installe ces outils dans ton environnement WSL si ce n'est pas déjà fait.
	- Installe Node.js et npm (via nvm, le gestionnaire de versions Node.js) :
	```bash
	curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.1/install.sh | bash
	source ~/.bashrc
	nvm install --lts
	```
	- Installe Git :
	```bash
	sudo apt install git
	```
- **NestJS**: Installer NestJS CLI :
```bash
npm install -g @nestjs/cli
```

- **PostgreSQL**: 
```bash
# Installe PostgreSQL
sudo apt install postgresql postgresql-contrib

# Démarre PostgreSQL et configure un utilisateur et une base de données
sudo service postgresql start
sudo -u postgres createuser --interactive
sudo -u postgres createdb citoykaidi

# configure un utilisateur PostgreSQL avec un mot de passe :
sudo -u postgres psql
ALTER USER your_user_name WITH PASSWORD 'your_password';
\q
```

## Cloner le Dépôt
Commencez par cloner le dépôt de votre projet :

```bash
git clone https://github.com/souleymanetimbidiallo/citoykaidi
cd citoykaidi
```

## Configurer les variables d'environnement
Ajoutez les variables d'environnement nécessaires pour le fichier .env (backend)
```bash
# backend/.env
DATABASE_URL=postgresql://user:password@localhost:5432/citoykaidi
JWT_SECRET=your_jwt_secret
AUTH0_CLIENT_ID=your_auth0_client_id
AUTH0_CLIENT_SECRET=your_auth0_client_secret
AUTH0_DOMAIN=your_auth0_domain

```

## Installation et exécution avec Docker

### Construire et démarrer les conteneurs
Depuis le répertoire racine du projet :

```bash
docker-compose up --build -d
```
Docker Compose va construire et démarrer les services suivants :
- backend : Serveur NestJS (port 3000)
- frontend : Application React.js (port 3001)
- PostgreSQL : Base de données (port 5432)

### Accéder à l'application
- Frontend : http://localhost:3001
- Backend API : http://localhost:3000

## Installation manuelle sans Docker
Si vous préférez exécuter les services localement sans Docker, suivez ces étapes :

### a. Backend (NestJS)

```bash
cd backend

# Installez les dépendances :
npm install

# Démarrez le serveur de développement :
npm run start:dev

```

### b. Frontend (React.js)
```bash
cd frontend

# Installez les dépendances :
npm install

# Démarrez l'application React :
npm start

```
Accédez à l'application via http://localhost:3000.

## Configuration de PostgreSQL
Si vous n'utilisez pas Docker pour PostgreSQL, configurez votre base de données PostgreSQL localement. 
Créez une base de données nommée citoykaidi.
```bash
# Se connecter à PostgreSQL en tant que super-utilisateur
psql -U postgres

# Créer la base de données
CREATE DATABASE citoykaidi;
```
Assurez-vous que la variable *-DATABASE_URL-* dans le fichier backend/.env pointe vers votre base de 
données locale.

## Tests
### a. Backend (NestJS)
Pour exécuter les tests du backend :
```bash
cd backend
npm run test
```
### b. Frontend (React.js)
Pour exécuter les tests du frontend :
```bash
cd frontend
npm run test
```
## Déploiement
Une fois que vous avez testé vos changements en local, vous pouvez déployer l'application sur 
un serveur de production. Utilisez **Docker Compose** pour orchestrer les conteneurs en production, 
ou déployez sur un service cloud comme **AWS, Azure, ou Google Cloud**.

Si vous souhaitez déployer l'application en production, vous pouvez utiliser Kubernetes. 
Voici les étapes de base pour déployer les conteneurs sur un cluster Kubernetes (par exemple, AWS EKS).
1. Créez les fichiers de déploiement Kubernetes (deployment.yaml et service.yaml).
2. Déployez sur Kubernetes avec :
```bash
kubectl apply -f deployment.yaml
```

## Contribution: 
Si vous souhaitez contribuer au projet, vous pouvez créer une branche et proposer vos modifications via 
des pull requests. Avant de soumettre une contribution, merci de respecter les conventions de commit et 
de code du projet.

## Documentation et Support
Gardez la documentation à jour pour toutes les nouvelles fonctionnalités ou changements dans l'architecture.