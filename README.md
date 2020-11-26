# Traefik

Configuration for Traefik v1.7

## Documentation

[Documentation - Traefik v1.7](https://docs.traefik.io/v1.7)

**View Traefik helper**
```bash
docker run traefik:1.7 --help
```

[Documentation - Docker](https://docs.docker.com/)

## Install Docker & Docker Compose
[Install guide - Docker](https://docs.docker.com/engine/install/)

[Install guide - Docker Compose](https://docs.docker.com/compose/install/) 

## Configuration

**Create Config dir and ssl dir**
```bash
mkdir -p config/certs
```

### Generate Certificat SSL

**Install openssl to Debian or Ubuntu**
```bash
sudo apt-get install openssl
```

**Create private server key**
```bash
sudo openssl genrsa -out server.key 2048
```

**Certificate Signing Request**
```bash
sudo openssl req -new -key server.key -out server.csr
```

**Sign certificat**
```bash
sudo openssl x509 -req -days 365 -in server.csr -signkey server.key -out server.crt
```

Add your server.csr, server.key, server.crt in the path config/ssl

## Config

**Create Network**
```bash
docker network create traefik
```

**Generate htpasswd to TRAEFIK_PASSWORD**
```bash
docker run --rm --name apache httpd:alpine htpasswd -nb YOUR-LOGIN YOUR-PASSWORD
```

**Copy environnement file**
```bash
cp .env.dist .env
```

**Edit environnement file**
```bash
vi .env
```
_Enter your 'TRAEFIK_DOMAIN', 'TRAEFIK_PASSWORD' and 'TRAEFIK_EMAIL'_

**Start Docker composer**
```bash
docker-compose  up # -d to detach container
```

**Add 'TRAEFIK_DOMAIN' to your host**
```bash
sudo echo "127.0.0.1  YOUR_TRAEFIK_DOMAIN"  >> /etc/hosts
```

Open your favorite navigator and enter your 'TRAEFIK_DOMAIN'

Great, your traefik is configure and start !


## Credits

Created by [Matthieu Beurel](https://www.mbeurel.com). Sponsored by [Nexboard](https://www.nexboard.fr).