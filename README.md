# React Frontend

Basic Create React App application within a Docker container.

Hosted example here:

## Development

### Build with Docker CLI

    $ docker build -f Dockerfile.dev

### Run with Docker CLI

    $ docker run -it -p 3000:3000 <container_id>

### Run with Docker CLI and Docker Volumes

    $ docker run -it -p 3000:3000 -v /app/node_modules -v $(pwd):/app <container_id>

This will put a bookmark on the node_modules folder (won't map it to anything else), map the /app folder in the container to the current directory (watch for updates). Therefore, you can make use of hot reload for changes in app.

### Run React Test Cases with Docker CLI

    $ docker run -it <container_id> npm run test

### Build and Run with Docker Compose

    $ docker-compose up

### Rebuild and Run with Docker Compose

    $ docker-compose down && docker-compose up --build

### Run React Test Cases with Docker Compose (Not Best Approach)

    $ docker-compose up
    $ docker exec -it <container_id> npm run test

## Production

### Build

    $ docker build .

### Run

    $ docker run -p 8080:80 <container_id>

NOTE: nginx default port is 80
