# Projet-Multimedia
Ynov Docker Project

## Déploiement du container Traefik

> :red_circle: **IMPORTANT !** :red_circle: Si vous avez déjà lancer le *script-bash* ainsi que le *docker-compose.yml*, passez à l'étape suivante.

### Avec Docker-Compose

Télécharger le fichier *script_bash* et le lancer avec la commande `bash script.bash`.
Télécharger le fichier *docker-compose.yml* et le lancer avec la commande `docker-compose up -d`.

### Sans Docker-Compose

Récupérer l'image avec la commande `docker pull traefik`.

Démarrer le container avec la commande:
`docker run -d -p 8080:8080 -p 80:80 \
-v $PWD/traefik.yml:/etc/traefik/traefik.yml \
-v /var/run/docker.sock:/var/run/docker.sock \
traefik:v2.0`

## Configurer l'environnement

Pour chaque container que nous souhaitons faire passer par Traefik, faire les étapes suivantes:

Dans notre cas nous prendrons comme exemple 
