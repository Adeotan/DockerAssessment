Create a directory on your host system, ./happs

The ./happs:/var/www/html/ part mounts the ./php/happs directory from the underlying host system as /var/www/html inside the container, where apache by default will read the data files.

Create a data directory on your host system, ./datadir

The ./datadir:/var/lib/mysql part mounts the ./datadir directory from the underlying host system as /var/lib/mysql inside the container, where MariaDB by default will write its data files.


The docker compose file has two services configured php-apache-environment and db

php-apache-environment service runs a container which has both apache server and php installed and db service runs a container with mariadb server.

php container exposes port 80 and mariadb container exposes port 3306. We are mapping these ports to ports 80 and 3306 on host system to access the services.

We are building the php image as part of docker compose file to avoid creating image every time there is a change in application code. And, we are using the official mariadb image from the dockerhub.

To bring up the development environment, run below docker compose command:

docker compose up -d

To stop the services, run below docker compose command:

docker compose stop <service name>



Error:

Warning: require(/var/www/html/public/../vendor/autoload.php): failed to open stream: No such file or directory in /var/www/html/public/index.php on line 24

Fatal error: require(): Failed opening required '/var/www/html/public/../vendor/autoload.php' (include_path='.:/usr/local/lib/php') in /var/www/html/public/index.php on line 24