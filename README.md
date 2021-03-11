# Projet-Muiltimedia
Ynov Docker Project

Ce projet consiste à créer un environnement multimédia avec des films et séries.

## 1/ Installation Docker Engine + Docker-Compose sous Ubuntu

Mettre à jour apt
```
$ sudo apt-get update
```

Ajouter le répertoire
```
$ sudo apt-get update
$ sudo apt-get install \
    apt-transport-https \
    ca-certificates \
    curl \
    gnupg \
    lsb-release
```

Ajouter la clé GPG officielle Docker
```
$ curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
```

Installer la version stable du répertoire Docker-Engine
```
$ echo \
  "deb [arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```

Mettre à jour apt
```
$ sudo apt-get update
```

Installer Docker Engine
```
$ sudo apt-get install docker-ce docker-ce-cli containerd.io
```

Vérifier sa bonne installation en lançant l'image `hello-world`
```
$ sudo docker run hello-world
```

Télécharger et installer la version stable de Docker Compose
```
$ sudo curl -L "https://github.com/docker/compose/releases/download/1.28.5/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
```

Se donner les droits d'éxecution sur le binaire
```
$ sudo chmod +x /usr/local/bin/docker-compose
```

Vérifier sa bonne installation en vérifiant la version
```
$ docker-compose --version
```
Le résultat doit être le suivant: `docker-compose version 1.28.5, build 1110ad01`