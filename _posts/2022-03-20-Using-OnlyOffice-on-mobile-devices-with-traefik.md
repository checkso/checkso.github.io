---
title: Using OnlyOffice on mobile devices with traefik
date: 2022-03-20
categories: [Nextcloud, OnlyOffice, ]
tags: [nextcloud, onlyoffice, docker, traefik]    
---

Since Ascensio decided to remove the support for mobile editing of documents using the Nextcloud app or browser, the community created a fork of OnlyOffice which brings this feature back.

A big thanks goes to Alexander Hofbauer for building this container: [link to github](https://github.com/aleho/onlyoffice-ce-docker-license)

As I am using traefik as reverse proxy I wanted to show my docker-compose file for getting OnlyOffice and Traefik working.

My Docker-Compose File

```yaml
version: '3.3'

services:
  onlyoffice-documentserver:
    image: alehoho/oo-ce-docker-license
    container_name: onlyoffice-documentserver
    environment:
      # Uncomment strings below to enable the JSON Web Token validation.
      - JWT_ENABLED=true
      - JWT_SECRET=ReallySecretPassword
      - JWT_HEADER=Authorization
      - JWT_IN_BODY=true
    networks:
       - traefik_proxy
       - default
    stdin_open: true
    restart: always
    ports:
       - "8889:80"
    volumes:
       - /docker/onlyoffice/data:/var/www/onlyoffice/Data
    labels:
       - "traefik.enable=true"
       - "traefik.http.routers.only-office.service=only-office"
       - "traefik.http.routers.only-office.entrypoints=web"
       - 'traefik.http.routers.only-office.rule=Host("onlyoffice.domain.tld")'
       - "traefik.http.middlewares.https-office-redirect.redirectscheme.scheme=https"
       - "traefik.http.routers.only-office.middlewares=https-office-redirect"
       - "traefik.http.routers.only-office-secure.middlewares=oo-header"
       - "traefik.http.routers.only-office-secure.entrypoints=web-secure"
       - 'traefik.http.routers.only-office-secure.rule=Host("onlyoffice.domain.tld")'
       - "traefik.http.middlewares.onlyoffice-redirectregex.redirectregex.regex=^http://(.*)"
       - "traefik.http.middlewares.onlyoffice-redirectregex.redirectregex.replacement=https://$$1"
       - "traefik.http.routers.only-office-secure.tls.certresolver=default"
       - "traefik.http.services.only-office.loadbalancer.server.port=80"
       - "traefik.http.middlewares.oo-header.headers.referrerPolicy=no-referrer"
       - "traefik.http.middlewares.oo-header.headers.stsSeconds=31536000"
       - "traefik.http.middlewares.oo-header.headers.forceSTSHeader=true"
       - "traefik.http.middlewares.oo-header.headers.stsPreload=true"
       - "traefik.http.middlewares.oo-header.headers.stsIncludeSubdomains=true"
       - "traefik.http.middlewares.oo-header.headers.browserXssFilter=true"
       - "traefik.http.middlewares.oo-header.headers.customRequestHeaders.X-Forwarded-Proto=https"

networks:
  traefik_proxy:
    external:
      name: traefik_proxy
  default:
    driver: bridge
```
