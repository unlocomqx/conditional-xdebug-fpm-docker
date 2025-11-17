# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Overview

Docker-based development environment with Apache httpd + PHP-FPM and conditional xdebug loading. Xdebug only loads when XDEBUG_SESSION cookie matches configured value (PHPSTORM by default), preventing performance degradation during normal development.

## Architecture

**Conditional PHP Routing**: Apache proxy module routes PHP requests to different PHP-FPM containers based on cookie presence:
- Cookie `XDEBUG_SESSION=${XDEBUG_COOKIE_VALUE}` → php_xdebug container
- No cookie → php container (faster, no xdebug overhead)
- Config: `bin/httpd/conf/extra/httpd-fpm.conf:8-18`

**Container Structure**:
- `php`: Production PHP-FPM (currently PHP 8.2), includes Composer + npm + Puppeteer Chrome
- `php_xdebug`: Debug PHP-FPM with xdebug 3.2.0 + imagick extension
- `httpd`: Apache 2.4.59 with custom configs

**PHP Build Variants**:
- `bin/php8X-fpm/`: Standard PHP without xdebug
- `bin/php8X-xdebug/`: PHP with xdebug + imagick
- Config: `bin/php*/etc/php/` for php.ini and extension configs

## Commands

```bash
# Initial setup
cp sample.env .env  # Configure DOCUMENT_ROOT and MYSQL_DATA_DIR first

# Start/stop
docker-compose up -d
docker-compose down

# Rebuild after Dockerfile changes
docker-compose build
docker-compose up -d --force-recreate

# Logs
docker-compose logs -f php
docker-compose logs -f php_xdebug
```

## Configuration

- `.env`: Project settings (COMPOSE_PROJECT_NAME, XDEBUG_COOKIE_VALUE, DOCUMENT_ROOT, etc.)
- `sample.env`: Template showing available PHP versions (5.4-8.2) and database options (mariadb/mysql/mysql8)
- Xdebug helper browser extension required for triggering debug mode

## Important Notes

- MySQL data compatibility issues exist between versions - backup before switching MySQL/MariaDB versions
- Port conflicts: Configurable via .env (default: 80, 443, 3306, 9090, 6379)
- phpMyAdmin: http://localhost:9090 or http://localhost/phpmyadmin