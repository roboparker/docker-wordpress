## File Structure
- `docker` contains docker related files
- `docker/bin` contains scripts that docker files need to run during the build
- `docker/mysql` files for the myaql docker container
- `docker/php` files for the php docker container
- `wordpress` wordpress install

*wordpress is not installed to root to prevent sensitive files being accessible to the web*

## Quick Commands Reference
- Dump `docker exec some-mysql sh -c 'exec mysqldump --all-databases -uroot -p"$MYSQL_ROOT_PASSWORD"' > /some/path/on/your/host/all-databases.sql`
- Restore `docker exec -i some-mysql sh -c 'exec mysql -uroot -p"$MYSQL_ROOT_PASSWORD"' < /some/path/on/your/host/all-databases.sql`

## TODO
- add commands about logs
- add documentation about db init
- add documentation about db volume
- add documentation about config
- add documentation about env
- add additional env options
- add production build?
- add ssl?