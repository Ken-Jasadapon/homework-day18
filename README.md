# DemoDockerCompos

This project is a Dockerized Node.js application using Express.js for backend services and PostgreSQL as the database. 
It is part of a homework assignment to demonstrate understanding of how to write a `Dockerfile` and `docker-compose.yaml`.

## Dockerfile Setup

The `Dockerfile` defines the steps to build the Docker image for the Node.js application with Express.js:

```Dockerfile
FROM node:alpine

WORKDIR /app

COPY package.json ./

RUN npm install

COPY . .

EXPOSE 3000

CMD [ "node", "index.js" ]

```

● Uses `node:alpine` as the base image, a lightweight version of Node.js.

● Sets the working directory to `/app`.

● Copies the `package.json` file and installs dependencies with `npm install`.

● Copies the entire project into the container.

● Exposes port 3000 for external connections.

● Starts the application with the command `node index.js`.

## Docker Compose Setup

The `docker-compose.yaml` file defines how to orchestrate the services, including the Express.js app and the PostgreSQL database:

```yaml

version: '3.9'

services:
  express:
    build:
      context: ./backend
      dockerfile: Dockerfile
    ports:
      - "3000:3000"
    environment:
      - PGUSER=postgres
      - PGHOST=postgres
      - PGPASSWORD=password1234
      - PGDATABASE=EcommerceDB
      - PGPORT=5432
    depends_on:
      - postgres

  postgres:
    image: postgres
    volumes:
      - postgres-data:/var/lib/postgresql/data
    environment:
      POSTGRES_PASSWORD: password1234
      POSTGRES_DB: EcommerceDB
    ports:
      - "5432:5432"

volumes:
  postgres-data:

```

● The `express` service is built from the `Dockerfile` and connects to the PostgreSQL database using environment variables (`PGUSER`, `PGPASSWORD`, etc.).

● The `postgres` service uses the `postgres` image, setting up the database and password.

● The `volumes` section ensures that PostgreSQL data persists even when the container is stopped.
