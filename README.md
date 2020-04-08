# LocalApp.dev Docker LEMP Stack

## About

Local Docker LEMP stack for developing secure PHP apps.

- Docker
- SSL/HTTPS
- PHP 7.4
- Nginx 1.16
- Postgres 12
- MariaDB 10.4
- Redis 5

## Installation

```bash
composer create-project pauloelias/docker-php-dev PATH
```

```bash
composer create-project pauloelias/docker-php-dev myapp
```

## Setup

Details TBD.

## Usage

```bash
cd myapp
docker-compose up --build -d
```