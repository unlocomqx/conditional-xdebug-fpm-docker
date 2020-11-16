# Conditional xdebug loading

Load xdebug only when the **XDEBUG_SESSION** cookie is set to **PHPSTORM** to avoid slowing down page loads unnecessarily

# Backup your sql data
If you intend to use this config with existing mysql data, **make sure to backup all your databases** then import then again.  
I encountered many compatibility issues when changing between mysql or mariadb versions.

# Commands
```shell script
git clone https://github.com/unlocomqx/conditional-xdebug-fpm-docker

cd conditional-xdebug-fpm-docker

# copy sample.env to .env (don't forget to change DOCUMENT_ROOT and MYSQL_DATA_DIR)
cp sample.env .env

docker-compose up -d
```

# Xdebug Helper
Install xdebug helper extension on your preferred browser

# phpMyAdmin
You can access phpmyadmin either via http://localhost:8080 or via http://localhost/phpmyadmin

# Credits
Based on https://github.com/sprintcube/docker-compose-lamp 
