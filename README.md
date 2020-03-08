# docker-laravel

## Env

- Docker
  - docker-compose
- NGINX 1.16.0
- PHP(php-fpm) 7.3.15
- MySQL 8.0.18
- (Node.js 12.7.0)
- memcached 1.5.22

8000 -nginx:80-> php-fpm:9000

## Setup

Only first time.

1. create laravel project dir

```
$ cd code

$ mkdir project // create laravel project dir (recommend another repository)
or
$ git clone CLONE_URL project
```

2. create docker container

```
$ docker-compose up --build -d
```

After that, execute the following.

```
$ docker-compose start

$ docker-compose stop
```

## License

MIT
