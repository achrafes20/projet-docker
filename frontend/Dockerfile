FROM node:18-alpine

# 1. Installer les outils système requis
RUN apk add --no-cache git python3 make g++

# 2. Installer Angular CLI
RUN npm install -g @angular/cli@latest

# 3. Créer et configurer le répertoire de travail
WORKDIR /usr/src/app

# 4. Copier UNIQUEMENT les fichiers de dépendances d'abord
COPY package*.json ./

# 5. Installer les dépendances du projet
RUN npm ci

# 6. Copier le reste des fichiers
COPY . .

# 7. Configurer le port et la commande de démarrage
EXPOSE 4200
CMD ["ng", "serve", "--host", "0.0.0.0", "--poll=1000", "--disable-host-check"]