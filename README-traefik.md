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

> Dans notre cas nous prendrons comme exemple *Radarr*.

1. Modifier le docker-compose.yml en supprimant la précision du port.
2. Ajouter à la suite les labels suivants:  
 ![image](https://user-images.githubusercontent.com/37578277/115683857-24370580-a357-11eb-94c1-9d77bf02b6ba.png)
3. Sauvegarder et quitter le fichier en ayant ce rendu:  
 ![image](https://user-images.githubusercontent.com/37578277/115684420-9f002080-a357-11eb-9186-c94f858bb1f6.png)
5. Relancer la commande `docker-compose up -d` pour appliquer les changements.
6. Sur votre poste, aller modifier le contenu du fichier `C:\Windows\System32\drivers\etc\hosts` en ajoutant l'entrée suivante:  
    adresse_IP_de_votre_VM_avec_docker radarr.project-traefik.lab
7. Ouvrir un navigateur web et taper `https://radarr.project-traefik.lab/` et vérifier que vous atteignez la page de radarr.

> Afin de réaliser les mêmes étapes pour d'autres containers, pensez à modifier les labels avec le nom et le port du service concerné. Ajouter également l'entrée dans le fichier host de votre poste avec le bon URL. 
  

