# Changelog

## 1.1.0 - 2020-04-04

### Added

- MariaDB support
- Named volumes for Postgres, MariaDB and Redis

### Changed

- Renamed `app` to `src`
- Renamed LICENSE to LICENSE.md
- Postgres database user credentials

## Removed

- Local `data` directory

## 1.0.3 - 2020-04-03

### Fixed

- Fix version number

## 1.0.2 - 2020-04-03

### Fixed

- Fix path to LICENSE file in `post-create-project-cmd`

## 1.0.1 - 2020-04-03

### Fixed

- Fix malformed `composer.json`

## 1.0.0 - 2020-04-03

### Changed

- Bump version for public release

## 0.0.3 - 2020-04-02

### Added

- Project `composer.json` file
- `/.env` and `/.env.example` files
- nginx config
- php.ini config
- `.gitignore` files to directory placeholders
- `./docker-config/php/Dockerfile` now installs `composer` and `awscli`
- `index.php` at web server root 

### Changed

- Project layout
- `docker-compose.yml` configuration now uses variables from `/.env` 
- Improved [README.md](./README.md)
- Replaced `public` web root with `web`

### Removed

- Dockerfiles for  `postgresql`, `redis`, `adminer` and `mariadb`

## 0.0.2 - 2020-04-02

### Changed

- Project scaffold

## 0.0.1 - 2020-03-19
### Added

- Initial Release