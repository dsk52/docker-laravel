# docker-laravel

## Env

- Docker 19.03.5
- docker-compose 1.24.1
- NGINX 1.16.0
- PHP(php-fpm) 7.4.1
- MySQL 8.0.18
- (Node.js 12.7.0)

8000 -nginx:80-> php-fpm:9000

## Setup

Only first time.

```
$ cd src
$ git clone CLONE_URL project

$ docker-compose up --build -d
```

After that, execute the following.

```
$ docker-compose start

$ docker-compose stop
```

## License

MIT
