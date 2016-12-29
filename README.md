# Docker-compose nginx, php-fpm(with xdebug), mysql, phpmyadmin for symfony

Run nginx, php-fpm and mysql using Docker for symfony
## Requirements
Install [Docker] and [Compose]

## Usage
Set your envirement variables in /docker/config/.env

For production set your domain in /docker/config/nginx/default.conf

Default database password is root

All database filse will be in .data folder
```
docker-compose up -d
docker-compose logs
docker-compose stop
docker-compose rm
```
Open url http://localhost:8085 and you will see a phpinfo page
Open url http://localhost:8086 and you can use phpmyadmin for your database

To access the docker console run: 
```
docker exec -ti container_php sh
```

Run composer you must run:
```
docker exec -ti startup_php sh -c 'cd ../ && composer update'
```

[Docker]:                      https://www.docker.io/
[Compose]:                     http://docs.docker.com/compose/install/ 