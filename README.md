# Symfony docker template
A Docker compose template designed for creating a Symfony application, optimizing the development process by setting up essential services like PHP-FPM, nginx and a data base with minimal configuration effort.

### Features
Core containers:
- nginx - handles HTTP requests and serves static files
- php-fpm - processes PHP scripts
- postgres - database for persistent data storage

Optional containers:
- redis - caching layer 
- redisinsight - GUI for managing and monitoring redis
- mongodb - NoSQL database
- mongo-express - web-based interface for MongoDB
- pgAdmin - GUI for managing PostgreSQL databases

### Status
In progress

### Usage
To run core containers only
```
docker compose up --build -d
```

Running optional containers by using dockers profiles 
```
#example: include mongodb when composing
docker compose --profile mongodb up --build -d
```
List of default assigned profiles can be found in compose.yaml file. 

Generating APP_SECRET
```
php -r 'echo bin2hex(random_bytes(32));'
```

### To-do list
- opcache configuration: 
    + ini settings
    + preload
    + composer post install script to reset opcache
- k8s charts and config


