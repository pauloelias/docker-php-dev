# Docker PHP Develeopment Environment

## About pauloelias/docker-php-dev

Simple local Docker LEMP stack for developing PHP projects.

- Docker
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