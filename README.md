# Introduction

This repository contains the docker compose file and instructions to initialize a postgresql server, pgadmin and metabase images in a local environment for testing.

# Setting up postgres

## Image Pull

The first step to setup postgres in our containers environment is to pull and download the images:

* postgres
* dpage/pgadmin4

We use the following commands:

```bash
docker pull postgres
docker pull dpage/pgadmin4
```

Then we can start our compose file which contain the relevant information and environment variables for initializing the services.

## Containers Compose

We can use the following command if we have just one compose.yaml file:

```bash
docker compose up -d
```

The `-d` flag can be used to run the container in detached mode and is optional.

With multiple compose.yaml files in the same directory the following command should be used:

```bash
docker compose -f compose_postgres.yaml up
```

The `-f` flag is used to specify the location of the compose file that should be used for deployment.

## Ports

When running the compose file we are exposing the following ports in the local network:

* postgres: 5432
* pg-admin: 82

## Connecting pgAdmin to PostgresDB

### Login

Log in with the credentials defined in the compose file:

* user: david.echajaya@hotmail.com
* password: testing

### Register the Server (First time)

Right click on 'Servers' in the object explorer to register a new server.

![Register Server](src/image.png)

In the 'General' tab of the register window enter a custom name for the server connection.

![Server Name](src/image-1.png)

In the connection tab we should input the following information:

* **Host name/address:** this should be the name or address of the network in which the database is deployed. In this case is the local network so we should input our Ipv4 direction instead of the localhost (remember that localhost refers to the containers environment in this context)
* **Port:** this is the port we mapped in our compose field.
* **Maintenance database:** is the name of the initial database created automatically for maintenance (Do not interact with this DB)
* **Username:** is the username defined in the compose file in the postgres service
* **Password:** is the password defined in the compose file in the postgres service

The information should be filled as following:

![Connection Fields](src/image-3.png)

The user and password should be the same as the ones defined in the compose file:

* **Username:** metabase
* **Password:** testing

Finally we click on save.