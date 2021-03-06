# imixs/postgres

The imixs/postgres Docker image runs a backup service for [Postgres Databases](https://www.postgresql.org/) using the [official postgres image](https://hub.docker.com/_/postgres). 

The image runs version Postgres 12.2 and provides an backup and restore scripts. The backup feature can be configured in the same way as the imixs/backup image. See details [here](../backup/README.md). The image does not start a postgres database. The goal of the image is providing a backup/restore service for postgres services. 


## Features
* inherit form official postgres image
* backup script to backup a database locally
* restore script to restore from a local backup
* remote backup script to create a remote rolling backup on a ftp space
* remote restore script to restore a remote backup from a ftp space



## 1. Install Docker
Follow the [Docker installation instructions](https://docs.docker.com/engine/installation/) for your host system.


## 2. Running and stopping a container
You can start an instance of the postgres service with the Docker run command:

	docker run --name="postgres" -it --rm \
	    -e SETUP_CRON="* 5 * * *" \
	    -e BACKUP_DB_PASSWORD="xxxxxxxxxxx" \
	    -e BACKUP_DB_HOST="db" \
	    -e BACKUP_DB_TYPE="POSTGRES" \
	    -e BACKUP_DB="wordpress" \
	    imixs/postgres
 

     
# Contribute

The source is available on [Github](https://github.com/imixs/imixs-docker). Please [report any issues](https://github.com/imixs/imixs-docker/issues).


## Development

To build the image from the Dockerfile source file run: 

    docker build --tag=imixs/postgres .
    
To test the backup service in interactive mode start the docker service: 

	docker run --name="postgres" -it --rm \
	    -e SETUP_CRON="*/1 * * * *" \
	    -e BACKUP_DB_PASSWORD="xxxxxxxxxxx" \
	    -e BACKUP_DB_HOST="db" \
	    -e BACKUP_DB_TYPE="POSTGRES" \
	    -e BACKUP_DB="wordpress" \
	    imixs/postgres

This will trigger the backup every minute. 