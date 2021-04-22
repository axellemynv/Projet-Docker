# Projet-Multimedia
Ynov Docker Project

## Déploiement du container

> :red_circle: **IMPORTANT !** :red_circle: Si vous avez déjà lancer le *script-bash* ainsi que le *docker-compose.yml*, passez à l'étape suivante.




Pull image
`docker pull traefik`

Start Traefik
`docker run -d -p 8080:8080 -p 80:80 \
-v $PWD/traefik.yml:/etc/traefik/traefik.yml \
-v /var/run/docker.sock:/var/run/docker.sock \
traefik:v2.0`
