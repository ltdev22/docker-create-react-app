# docker-create-react-app

Scaffold a new React app with Docker. This guide here shows how to (dockerize your React app)[https://mherman.org/blog/dockerizing-a-react-app/], but in order to make a fresh installation you need to have node, npm etc also installed locally. Using this simple docker container, that does only one thing, we install _create-react-app_ and we can use it to generate create-react-app scaffold without having to install anything else locally.

#### How to use

To build the docker image run
```
docker build . -t react-cli
```

To scaffold a new React app using the `create-react-app` command run
```
docker run -v ${PWD}:/app react-cli create-react-app myAppName
```

_NOTE:_ After running the above command you will also need to run `docker run -v ${PWD}:/app react-cli npm i` to generate the package-lock.json file - for some reason this file is not generated at the moment.


Also using the image I've already push on (dockerhub)[https://hub.docker.com/repository/docker/ltweb22/react-cli/general]
```
docker run -v ${PWD}:/app ltweb22/react-cli create-react-app myAppName
```

#### Using docker-compose (not tested, but hopefully should do the trick ;-p )

Add the following in the docker-compose.yml
```
version: '3'
services:
  rcli:
    build: .
    image: react-cli
    container_name: react-cli
    volumes:
      - .:/app
```

To create a new app run
```
docker-compose run rcli create-react-app myAppName
```
