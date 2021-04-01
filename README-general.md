# Projet-Multimedia
Ynov Docker Project

Ce projet consiste à créer un environnement multimédia avec des films et séries.

> :red_circle: **IMPORTANT !** :red_circle: Utiliser une distribution Linux, dans notre cas Ubuntu, et utiliser un utilisateur qui se nomme ***administrateur***.
> Sinon, modifier la deuxième ligne du fichier script_bash `cd /home/administrateur` par `cd /home/[votre_nom_utilisateur]`. 

## 1/ Installation Docker Engine + Docker-Compose sous Ubuntu

Mettre à jour apt:
```
$ sudo apt-get update
```

Ajouter le répertoire:
```
$ sudo apt-get update
$ sudo apt-get install \
    apt-transport-https \
    ca-certificates \
    curl \
    gnupg \
    lsb-release
```

Ajouter la clé GPG officielle Docker:
```
$ curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
```

Installer la version stable du répertoire Docker-Engine:
```
$ echo \
  "deb [arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```

Mettre à jour apt:
```
$ sudo apt-get update
```

Installer Docker Engine:
```
$ sudo apt-get install docker-ce docker-ce-cli containerd.io
```

Vérifier sa bonne installation en lançant l'image `hello-world`:
```
$ sudo docker run hello-world
```

Télécharger et installer la version stable de Docker Compose:
```
$ sudo curl -L "https://github.com/docker/compose/releases/download/1.28.5/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
```

Se donner les droits d'éxecution sur le binaire:
```
$ sudo chmod +x /usr/local/bin/docker-compose
```

Vérifier sa bonne installation en vérifiant la version:
```
$ docker-compose --version
```
Le résultat doit être le suivant: `docker-compose version 1.28.5, build 1110ad01`.


## 2/ Lancer les scripts

Récupérer les scripts `docker-compose.yml` et `script_bash` dans `/home`.

Lancer le script:
```
$ sudo bash /home/script_bash.sh
```
Les dossiers sont créés.

Lancer le docker-compose.yml afin de créer et lancer les containers:
```
$ sudo docker-compose -f /home/docker-compose.yml up -d
```

Vérifier que les containers sont crées et lancés:
```
$ sudo docker ps -a
```


## 3/ Configuration des containers

### 1- Jackett

> Assurrez-vous d'avoir un compte sur YGGtorrent avant de continuer la configuration

1. Aller sur `http://[Adresse IP de votre machine]:9117/`.

2. En bas de page, dans la section `Jackett Configuration` et dans le champs `FlareSolverr API URL` renseigner l'URL de FlareSolverr: `"http://[Adresse Ip de votre machine]:8191/"`.
3. Cliquer sur `Apply server settings` en haut de section.

4. En haut de page, cliquer sur `Add indexer`.
5. Trouver l'indexer `YGGtorrent`puis cliquer sur la clé à molette à droit pour le configurer.
6. Dans `Username`et `Password` rentrer vos logins de votre compte YGGtorrent, puis cliquer sur `Okay`.

7. Cliquer à nouveau sur `Add indexer`.
8. Trouver l'indexer `GkTorrent`puis cliquer sur le bouton '+' pour l'ajouter.

### 2- Radarr et Sonarr

1. Aller sur `http://[Adresse IP de votre machine]:8989/` et `http://[Adresse IP de votre machine]:7878/`.

 > La configuration qui suit est identique pour Radarr et Sonarr.

2. Aller dans `Settings > Indexers`.
3. Dans la section `Indexers` cliquer sur le bouton '+'.
4. Trouver l'option `Torznab` puis cliquer sur `Custom`.
5. Pour le nom rentrer `YGGtorrent`.
6. Retourner dans Jackett et dans la liste des indexers, cliquer sur `Copy Torznab Feed` pour `YGGtorrent`.
7. Sur Radarr ou Sonarr, faire **Ctrl-V** ou clique droit et coller l'URL.
8. Retourner dans Jackett et copier la clé API en haut à droite de la page.
9. Sur Radarr ou Sonarr, coller la clé API dans le champs `API Key`.
10. Dans `Categories` rentrer *5000*.
11. Puis cliquer sur `Save`.
12. Refaire les étapes 3 à 11 pour **GkTorrent**.
13. Passer dans la section `Download Client`et cliquer sur le bouton '+'.
14. Cliquer sur `Transmission`.
15. Pour le nom rentrer `Transmission`.
16. Dans `Host` remplacer `localhost` par l'adresse IP de votre machine.
17. Dans `Username` rentrer `username`.
18. Dans `Password` rentrer `password`.
19. Cliquer sur `Save`.

### 3- Jellyfin

1. Aller sur `http://[Adresse IP de votre machine]:8096/`.
2. Choisir votre langue préférée puis cliquer sur `Suivant`.
3. Rentrer un nom d'utilisateur puis mot de passe avant de cliquer sur `Suivant`.
4. Cliquer sur `Ajouter une médiathèque`.
5. Comme `Type de contenu` sélectionner `Films`.
6. Donner un nom à votre médiathèque dans la section `Nom d'affichage`.
7. Cliquer sur le bouton '+' dans `Dossier`.
8. Sélectionner `/data/movies` puis cliquer sur `OK`.
9. Aller en bas de page et cocher `Activer l'extraction des images de chapitres`, puis cliquer sur `OK`.
10. Cliquer à nouveau sur `Ajouter une médiathèque`.
11. Refaire les étapes 5 à 9 en changeant le type de contenu à `TV` et en sélectionnant `/data/tvshows`
12. Cliquer sur `Suivant`.
13. Choisir une langue et un pays pour les métadonnées puis cliquer sur `Suivant`.
14. Laisser la configuration à l'accès à distance par défaut puis cliquer sur `Suivant`.
15. Cliquer sur `Terminer`.
16. Identifiez-vous.
