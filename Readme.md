# PHP docker based DEV environment

---

Maintainer: Eike Henrik Drost (MCEikens)

`This docker containers are only for dev environment.`

---
## Install
To install clone or download this container and remove the .git folder of project.


## Using

### Preparation
At first you need to copy .env.dist file and save as .env

In this file we configure our credentials for database connection, and our exposing ports.

### Where is my project root?
In the **app** folder you can put your PHP app. That will be synced to the php and nginx containers.

### How can i start my containers?
At first you should run following command on the same layer where your docker-compose file is saved.
> docker-compose build

This command builds your php container, if there isn't exists.

To start your containers in detached mode you can run:
> docker-compose up -d

To see logs in tail mode: 
> docker-compose logs -f

To stop containers:
> docker-compose stop

To remove containers:
> docker-compose down

To remove all containers and with orphan containers
> docker-compose down --remove-orphans

With the attribute `--remove-orphans` we remove also all not persistent saved files from containers.

To connect to your container:
> docker-compose exec CONTAINER_NAME TYPE

TYPE: bash / sh <br/>
CONTAINER_NAME: db, php, nginx, maildev

e.g.
> docker-compose exec php bash

### Database connection

> mysql://YOUR_USER_NAME:YOUR_PASSWORD@db/YOUR_DATABASE_NAME
