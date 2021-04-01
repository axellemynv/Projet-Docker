# Projet-Muiltimedia
Ynov Docker Project

Pull image
`docker pull traefik`

Start Traefik
`docker run -d -p 8080:8080 -p 80:80 \
-v $PWD/traefik.yml:/etc/traefik/traefik.yml \
-v /var/run/docker.sock:/var/run/docker.sock \
traefik:v2.0`
