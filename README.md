# docker-php7.1.3-apache-mariadb-xdebug
Working PHP 7.1.3(apache) with mariadb database, phpmyadmin and xdebug for local debugging (development environment)

# Please note
- The intended use of this collection, is for rapidly starting a develop environment with Xdebug working out of the box, while also having phpmyadmin and mariadb (mysql) running. 

- Phpmyadmin: http://localhost:8080/ (put in "db" in database server. It works because of container linking in Docker)
- Application: http://localhost/ 
- MariaDB data: Stored inside docker-volume "db" (same name as the docker-container using it. If you need a backup, use phpmyadmin or in production: A docker container could mount it with --volumes-from and copy data elsewhere)

# Tested using
- Windows 10 x64 before anniversary update (may/may not work out of the box on linux/mac)
- Docker Community Edition Version 17.03.0-ce-win1 (10296)
- PHPStorm 2016.3.3

# You may want to (before running)
- Change the random MYSQL_ROOT_PASSWORD in docker-compose.yml (on first run, this will be added to the root user in the mariadb data-volume.
- Install the Xdebug helper plugin if you use Chrome: https://chrome.google.com/webstore/detail/xdebug-helper/eadndfjplgieldjbigjakmdgkmoaaaoc (1 click debugging)

# If you change the Dockerfile or docker-compose.yml:
- Run "docker-compose build" before running "docker-compose up" again.
