# HAPROXY

## Installation + Configuration sans utilisation du script

### 1/ Configuration du fichier : haproxy.cfg

Créer puis ouvrir le fichier haproxy.cfg :
```
root@srv-ubuntu:/home/administrateur/project-haproxy/config/haproxy# nano haproxy.cfg
```

Ajouter la configuration suivante :
```
global
    log localhost local0
    log localhost local1 notice
    daemon
defaults
    mode http
    stats uri /haproxy?stats
    option forwardfor
    option httpchk
frontend php_apache_frontend
    bind *:80
    default_backend php_apache_backend
backend php_apache_backend
    server php_apache_01 php_apache_01:80 check
    server php_apache_02 php_apache_02:80 check
    server php_apache_03 php_apache_03:80 check
    server php_apache_04 php_apache_04:80 check
```

### 2/ Configuration du fichier : docker-compose.yml

Ouvrir le fichier : 
```
root@srv-ubuntu:/home/administrateur# nano docker-compose.yml
```

Ajouter la configuration suivante :
```
---
version: "3"

services:
  haproxy:
    container_name: project-haproxy_haproxy
    image: haproxy
    depends_on:
      - php_apache_01
      - php_apache_02
      - php_apache_03
      - php_apache_04
    volumes:
      - /var/run/docker.sock:/var/run/docker.sock
      - /home/administrateur/project-haproxy/config/haproxy:/usr/local/etc/haproxy:ro
    ports:
      - 80:80
  php_apache_01:
    container_name: php_apache_01
    image: php:7-apache
    volumes:
      - /home/administrateur/project-haproxy/www:/var/www/html
    ports:
      - 81:80
  php_apache_02:
    container_name: php_apache_02
    image: php:7-apache
    volumes:
      - /home/administrateur/project-haproxy/www:/var/www/html
  php_apache_03:
    container_name: php_apache_03
    image: php:7-apache
    volumes:
      - /home/administrateur/project-haproxy/www:/var/www/html
  php_apache_04:
    container_name: php_apache_04
    image: php:7-apache
    volumes:
      - /home/administrateur/project-haproxy/www:/var/www/html
```

## Installation + Configuration avec utilisation du script

Télécharger le fichier `script_bash` et le lancer avec la commande `bash script.bash`.

Naviguer dans le dossier **/home/administrateur** avec la commande `cd /home/administrateur`.

Lancer la commande `docker-compose up -d` pour déployer les containers.
