# Zikula on 🐳 Docker + PHP 7.4 + MySQL + Nginx + PhpMyAdmin

## Description

This is a complete stack for running Zikula with Symfony 5 into Docker containers using docker-compose tool.

It is composed by 4 containers:

- `nginx`, acting as the webserver.
- `php`, the PHP-FPM container with the 7.4 PHP version.
- `db` which is the MySQL database container with a **MySQL 8.0** image.
- `phpmyadmin` for database web access.

## Installation

This assumes, you already have working installations of Docker and Git.
It might happen that default ports are already in use and containers will not run.
You can use .env file and uncomment custom port declarations
All services are covered.

1. Create project directory and Clone Zikula core
   - `mkdir zikula_project`
   - `cd zikula_project`
   - `git clone https://github.com/zikula/core.git core`
2. Clone this repository next to `./core`
   - `git clone https://github.com/zikula/core-dev-docker.git core-dev-docker`
3. Start the containers 
   - `cd core-dev-docker`
   - `docker-compose up -d`
   - 4 containers are created and deployed:
      ```
      Starting core_nginx_1 ... done
      Starting core_php_1   ... done
      Starting core_db_1    ... done
      Starting core_phpmyadmin_1 ... done
      ```
4. Log in to php container and install dependencies
   - `docker exec -it core_php_1 bash`
   - `composer install`
   - `yarn install --force`

Your zikula dev enviroment is ready!
### Zikula installation
 Your zikula installation should be accessible under zikula.localhost, by default it listens on port 80
 PhpMyAdmin is accessible by default under zikula.localhost:8080

 Composer, nvm, npm, yarn and symfony console are installed in container you can access them by logging into php container
   - `docker exec -it core_php_1 bash`

 You might need to adjust permissions for all directories.

   For installation visit zikula.localhost

   Install Zikula using the following information:
   - DB info:
      - type: mysql
      - host: db
      - port: 3306
      - user name: root
      - password: root
      - database name: zikula

## Multiple projects
 In case you want to have multiple core projects running simuntanously. 
 Create project 1

      ```
      mkdir project1
      cd project1
      git clone https://github.com/zikula/core.git project1
      git clone https://github.com/zikula/core-dev-docker.git core-dev-docker
      cd core-dev-docker

      // Edit your .env file change COMPOSE_PROJECT_NAME to project1 and APP_PATH to project1
      // uncomment port variables. Use ports available on your host. Change project url.

      PORT_HTTP=3000
      PORT_HTTPS=3001
      PORT_DATABASE=3002
      PORT_PHPMYADMIN=3003
      PORT_PHPDEV=3004

      NGINX_HOST=project1.localhost

      // Start containers

      Starting project1_nginx_1 ... done
      Starting project1_php_1   ... done
      Starting project1_db_1    ... done
      Starting project1_phpmyadmin_1 ... done
      ```

   Create project 2

      ```
      mkdir project2
      cd project2
      git clone https://github.com/zikula/core.git project2
      git clone https://github.com/zikula/core-dev-docker.git core-dev-docker
      cd core-dev-docker

      // Edit your .env file change COMPOSE_PROJECT_NAME to project2 and APP_PATH to project2
      // uncomment port variables. Use ports available on your host. Change project url.

      PORT_HTTP=3100
      PORT_HTTPS=3101
      PORT_DATABASE=3102
      PORT_PHPMYADMIN=3103
      PORT_PHPDEV=3104

      NGINX_HOST=project2.localhost

      // Start containers

      Starting project2_nginx_1 ... done
      Starting project2_php_1   ... done
      Starting project2_db_1    ... done
      Starting project2_phpmyadmin_1 ... done
      ```

#### Credits
This docker enviroment was created from various docker examples and based on code below.

Dockerfile created with assistance from https://latteandcode.medium.com/how-to-integrate-docker-into-a-symfony-based-project-f06164dc7944
and generally forked from https://github.com/ger86/symfony-docker
