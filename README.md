# Zikula on 🐳 Docker + PHP 7.4 + MySQL + Nginx

## Description

This is a complete stack for running Zikula with Symfony 5 into Docker containers using docker-compose tool.

It is composed by 3 containers:

- `nginx`, acting as the webserver.
- `php`, the PHP-FPM container with the 7.4 PHP version.
- `db` which is the MySQL database container with a **MySQL 8.0** image.

## Installation

This assumes, you already have working installations of Docker, Git, Composer, Symfony-CLI, npm & yarn

1. Clone Zikula core
   - `git clone https://github.com/zikula/core.git core`
   - `cd core`
   - `symfony composer install`
   - `yarn install --force`
2. Clone this repository next to `./core`
   - `cd ..`
   - `git clone https://github.com/zikula/core-dev-docker.git core-dev-docker`
3. Start the containers 
   - `cd core-dev-docker`
   - `docker-compose up -d`
      - 3 containers are created and deployed:
         ```
         Creating core-dev-docker_db_1    ... done
         Creating core-dev-docker_php_1   ... done
         Creating core-dev-docker_nginx_1 ... done
         ```
4. Install Zikula using the following information:
   - DB info:
      - type: mysql
      - host: db
      - port: 3306
      - user name: root
      - password: root
      - database name: zikula

### DB manipulation (clear the DB)
set env.local to include (if not already)
 - DATABASE_URL="mysql://root:root@db:3306/zikula?serverVersion=5.7"

jump into the CLI for the php container, then:
 - bin/console doctrine:database:drop --force
 - bin/console doctrine:database:create

#### Credits
Dockerfile created with assistance from https://latteandcode.medium.com/how-to-integrate-docker-into-a-symfony-based-project-f06164dc7944
and generally forked from https://github.com/ger86/symfony-docker
