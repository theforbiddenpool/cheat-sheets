When applications start to grow, it starts to become harder to run that application on another machine. **Containers** come in to help us run our apps in all the environments possible.

Instead of having one big monolithic application, larger companies break their apps into different layers, also considered **services**. Each layer is in its own container, and communicate with each other to make the system work.

Container services came in to popularize the **microservices architecture**. Additionally, they also make it easier for new developers to set up the project in their own machines with one command.

## VMs vs Containers
Before Docker, we used Virtual Machines. They are **sandbox environments** - each one contains a full-fledge computer, with their own operating system. They could take minutes to boot up. Docker changed this idea – its containers wrap up the software in a complete file system that only bundle the libraries and settings required for the application to run, and the application itself. They use the host operating system, making them fast and easily accessible.

We can create as many containers as we want, making it very easy to scale and grow. As the number of containers grow, we start getting into **container orchestrastion**, *e.g.* Kubernetes.

# Docker
__Containers__ → lightweight alternative to the virtual machines. The container is run on top of the operating system - the environment inside the contianer is completely isolated from the OS. Each container consists of an image.

__Image__ → way to bundle our application into a standalone package. The image describes what the container should do. It's then read by Docker, which generates a container that will run what we'd specified.

__Volume__ → writable file system, added on automatically inside of the container.

[Docker Hub](https://hub.docker.com/) provides a way to search and download images to use, pre-written by people. They are already setup for us, so the only thing left for us to do is to run them.

## Docker CLI
#### Build an image
```
$ docker build -t <tag-name> <directory>
```

#### Running a container
```
$ docker run -it <container-name>
```
- `-it` → gives us a TDY environment, allowing us to enter our container.
- `-d` → runs the container in the background.
- `-p <origin>:<destination>` → port forwarding from host machine to the container. Our host machine has no knowledge of the container, so we need to tell it where to expose a port - this is called **port binding**.

Always check your containers to make sure whatever we've set up is actually there. Everytime we run a container, Docker will generate a new container hash (container id).

#### Check what containers we have running
```
$ docker ps
```

#### Access a container
```
$ docker exec -it <container-id> bash
```

#### Stop container
```
$ docker stop <container-id>
```

## Dockerfile
The *Dockerfile* is our image, and it should be located at the root of our project.

#### Include another image:
```
FROM node:carbon
```

#### `CMD`
```
CMD ["/bin/bash"]
```
This is what will be executed by default when we lauch the build image. It's usually place at the end of the file. A Dockerfile can only have one `CMD` command.

#### Specify the directory we want to work out of
```
WORKDIR /usr/src/our-app
```

#### Copy something into the container
```
COPY <source> <destination>
```
We can specify a file or a directory to copy. If we want to copy something to our working directory we use `./`.

#### Run a command in the container
```
RUN <command>
```
This command is commited to the Docker image. A Dockerfile can run many run steps that layer on top of one another.\
After we have copied our project into the container, one command we can run is `npm install`.

## Docker Compose
**Docker Compose** → used to orchestrate our application services during development. It allows us to define and run multi-container Docker applications, *e.g.* API, Database, and Redis. It uses a YAML file to configure our application services.

The configuration file is named *docker-compose.yml*.

```yml
version: '3.6'

services: # what we're going to ochestrate, *e.g. API service
  backend-api: # name of the service
    container_name: backend
    build: ./ # allows us to build from our own Dockerfile instead of the default image
    command: npm start # command to run when the container is created
    working_dir: /usr/src/backend-api
    ports:
      - "3000:3000" # port forwarding
    environment: # environmental variables
      POSTGRES_USER: root
      POSTGRES_PASSWORD: 12345
      POSTGRES_DB: app-db-docker
      POSTGRES_HOST: postgres
    volumes: # allows us access to the file system
      - ./:/usr/src/backend-api # maps our project to the container. Used to listen to changes when in development
    
  postgres:
    environment:
        POSTGRES_USER: root
        POSTGRES_PASSWORD: 12345
        POSTGRES_DB: app-db-docker
        POSTGRES_HOST: postgres
    image: postgres
    ports:
      - "5432:5432"
```

#### Build our services
```
$ docker-compose build
```
Everytime we change something in your app, we have to re-build it.

#### Run one-time command against a service
```
$ docker-compose run <service-name> [command]
```
The command starts in a new container. It can override the command defined in the service configuration.

#### Shut off all containers
```
$ docker-compose down
```
Useful to avoid any conflicts we may have when changing files.

#### Build & Run our services
```
$ docker-compose up --build
```
- `--build` → also builds our services.
- `-d` → run in the background.
It will start all the services defined in the *docker-compose.yml*.

#### Run commands in service
```
$ docker-compose exec <service-name> <command>
```

### Connecting Containers
In the past, we needed to use a `links` property to be able to reference other containers. This was deprecated in favor of **networks**.

By default, Compose sets up a single network for our app. Each container for a service joins the default network. The containers are both reachable by others on that network, and discoverable by them at a hostname identical to the container name.

### Databases
When we create a container with a image of a database, we don't have any databases in it. We can create a custom image, according to the image's documentation.

# Keywords
__Monolithic Application__ → single-tiered software application in which different components are combined into a sinble program from a single platform.

__Load Balancer__ → distributes traffic to the different API servers, so no server is too clogged.

# Sources
[The Complete Junior to Senior Web Developer Roadmap (2020)](https://www.udemy.com/course/the-complete-junior-to-senior-web-developer-roadmap/), by Andrei Neagoie
