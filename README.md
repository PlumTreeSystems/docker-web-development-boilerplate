# Docker web development environment boilerplate
Quick development environment for web projects with nginx proxy and database services.
Nginx proxy/router allows routing based on domain names.

# Installation
1. Intall [Docker](https://www.docker.com/products/docker)
2. Enable Shared Drives / Volume Mounting
3. Clone repository somewhere on the shared drive

# Running Router + MySQL + PhpMyadmin + MailCatcher
1. Cd PATH_TO_BOILERPLATE/service_bundles
2. Run docker-compose up -d
3. Open your hosts file and append new lines:
  - YOUR_DOCKER_IP phpmyadmin.local
  - YOUR_DOCKER_IP mailcatcher.local
4. You should be able to access phpmyadmin on http://phpmyadmin.local and mailcatcher on http://mailcatcher.local

NOTE: YOUR_DOCKER_IP is your docker vm's/network's ip

## Provide custom domains for your app 
Add you custom domain inside VIRTUAL_HOST environmental variable
inside docker-compose.yml
``` YAML
environment:
         - VIRTUAL_HOST=app.local
```
NOTE: don't forget to add new domain to your hosts file

## Provide links to MySQL db
Add external link rmp_mysql_1 and network rmp_default

inside docker-compose.yml
``` YAML
version: '2'
services:    
    app:
        build: ./       
        external_links:
         - rmp_mysql_1
        environment:
         - VIRTUAL_HOST=app.local        
        networks:
         - default
         - rmp_default
networks:
    rmp_default:
        external: true  
```
## Example app
[Symfony app docker files](https://gist.github.com/matas-valuzis/4422edc18cb176eb08713e25f4498395)
