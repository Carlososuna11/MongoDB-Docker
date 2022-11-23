# MongoDB Docker Configuration

> MongoDB is a document database with the scalability and flexibility that you want with the querying and indexing that you need. [MongoDB](https://www.mongodb.com/)

This repository contains the configuration files for running minIO in Docker containers. It is based on the [MongoDB](https://www.mongodb.com/compatibility/docker) tutorial.

## Configuration

1. Set up a MongoDB broker

   The Docker Compose file below will run everything for you via Docker.

```yml
version: "3.8"
services:
  mongo:
    image: mongo:6
    restart: always
    env_file:
      - .env
    volumes:
      - mongo_data:/data/db
    ports:
      - "27017:27017"

volumes:
  mongo_data:
```

2. Start the mongoDB docker

   From a directory containing the `docker-compose.yml` file created in the previous step, run this command to start all services in the correct order.

```bash
docker-compose up -d
```

3. Create a user

```
docker-compose exec mongo mongosh -u <root-user> -p <root-password>
```

```
use admin
```

```js
db.createUser(
    {
        user: "carlos",
        pwd: passwordPrompt(),
        roles:[
                {
                    role: "userAdminAnyDatabase",
                    db: "admin"
                },
                "readWriteAnyDatabase"
            ]
    }
)
```
