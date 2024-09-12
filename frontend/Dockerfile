# Utiliser une image Node.js
FROM node:16-alpine

# Définir le répertoire de travail
WORKDIR /app

# Copier package.json et installer les dépendances
COPY package*.json ./
RUN npm install

# Copier le reste de l'application
COPY . .

# Construire l'application React pour la production
RUN npm run build

# Exposer le port sur lequel le serveur React fonctionne
EXPOSE 3000

# Commande de démarrage du serveur
CMD ["npm", "start"]
