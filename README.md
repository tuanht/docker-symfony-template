# Docker/Symfony template

# How to setup

```shell
docker-compose build
docker-compose up -d
```

## Install Symfony CLI

```shell
curl -sS https://get.symfony.com/cli/installer | bash
```

Create Symfony demo application

```shell
symfony new --full symfony_demo
```

Or microservice/console/api application

```shell
symfony new symfony_demo
```

Fix permission

```shell
docker-compose exec php mkdir var/{log,cache}
docker-compose exec php chown www-data:www-data var/{log,cache}
```
