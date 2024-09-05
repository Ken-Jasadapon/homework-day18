# DemoDockerCompos

This project is a Dockerized Node.js application using Express.js for backend services and PostgreSQL as the database. It is part of a homework assignment to demonstrate understanding of how to write a `Dockerfile` and `docker-compose.yaml`.

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

● Uses node:alpine as the base image, a lightweight version of Node.js.

● Sets the working directory to /app.

● Copies the package.json file and installs dependencies with npm install.

● Copies the entire project into the container.

● Exposes port 3000 for external connections.

● Starts the application with the command node index.js.
