## File Structure
- `docker` contains docker related files
- `docker/bin` contains scripts that docker files need to run during the build
- `docker/mysql` files for the mysql docker container
- `docker/php` files for the php docker container
- `wordpress` wordpress install

*wordpress is not installed to root to prevent sensitive files being accessible to the web*

## MySQL

### Configuration
Some configuration options are in the env file. you can define additional config values for mysql in `docker/mysql/local.cnf`

### initiliaze db
When starting up the container for the first time, the sql scripts in the `docker/mysql/init` folder will run in alphabetical order.
This can be used to load in initial data for your application.

After the first startup you will need to run dockers exec shell command to dump and run mysql commands.

- Dump `docker exec db sh -c 'exec mysqldump --all-databases -uroot -p"$MYSQL_ROOT_PASSWORD"' > /some/path/on/your/host/all-databases.sql`
- Restore `docker exec -i db sh -c 'exec mysql -uroot -p"$MYSQL_ROOT_PASSWORD"' < /some/path/on/your/host/all-databases.sql`

### Where are the files
The database files are stored in a docker volume instead of being a mounted volume for performance and security. 

You can determine the volume name with `docker volume ls` and delete it with `docker volume rm name`

## Adminer
Adminer is used instead of PHPMyAdmin for its simplicity and it does not depend on PHP. 

### configuration
The port can be changed in the env file.

## WordPress
Uses the latest version of wordpress with php 7.4 with xdebug enabled.

### Configuration
The port is defined in the env file. Some more common options are in the docker-compose file. Once the container is up you can edit the wp-config file as needed.

### Logs
You can view PHP logs with `docker logs -f wordpress >/dev/null`