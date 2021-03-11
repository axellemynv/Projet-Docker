# Projet-Muiltimedia
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

> S'assurer que vous avec un compte sur YGGtorrent avant de continuer la configuration

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
5. 
