# Nginx Notes

### Table of contents

- 1 [What is Nginx](#nginx)
- 2 [Setting up Nginx](#setup)
  - 2.1 [Setting up Nginx with docker](#docker)
  - 2.2 [Checking the server status](#serverstatus)
  - 2.3 [SSH into running docker container](#dockerSSH)
  - 2.4 [Nginx commands](#nginxcommands)
  - 2.5 [Nginx default directory](#nginxdefaultdir)

<div id="nginx"></div>

### What is nginx?

Nginx is a web server that can be used as a reverse proxy, load balancer, mail proxy, HTTP cache. Its developed by Igor Sysoev, and released in 2004. Its free and open source.


<div id="setup"></div>

### Setting up Nginx


<div id="docker"></div>

#### Setting up Nginx with docker

Open en new folder and inside the new folder run the command `docker pull nginx` to pull an image from the docker site.
This will automatically create an image inside docker that we can now run.

To run the container use the following command: `docker run --name nginx-webserver -it --rm -d -p 8000:80 nginx`
`--name` Gives the server a name,
`-it` Will tell docker to allocate a sudo connection so that we can interact with the terminal,
`--rm` Removes or stops any containers that might already be running,
`-d` Runs it as a deamon (background process),
`-p` Defines the port of the and exposes it so that we can access it.

This will start a docker container that listens from port 80 and we can access the website by going to `localhost:8000`

<div id="serverstatus"></div>

#### Checking the status of the server

To check the status of the server you can check if it runs by going to `localhost:8000` or curl it in the temrinal by using `curl localhost:8000` or in powershell `curl https://localhost:8000`.

<div id="dockerSSH"></div>

#### SSH into running docker container

Accessing the shell can be done inside docker desktop itself or the docker extension itself. But if you want to attach the shell throught the command line use the following command: `docker exec -it <conatainer name> /bin/bash`
If you want to directly execute a command inside the container you can use the same command except instead of using `/bin/bash` you type in whatever command you want to excute. Example: `docker exec -it <container name> ls` to list all directories in the current working directory.

<div id="nginxcommands"></div>

#### Nginx commands

To open the help list of nginx type `nginx -h` or `nginx -?`. To see the version of nginx `nginx -v` can be used or `nginx -V` form extended information.
To test the `nginx.conf` file you can use the command `nginx -t` or `nginx -T` for a more extended test and inside.
To stop nginx and the container itself within the container itself you can use `nginx -s stop` to send a signal to stop the process.

<div id="nginxdefaultdir"></div>

#### Nginx default directory

Nginx will serve all the file inside the default directory. This directory can be found with this path `/usr/share/nginx/html` and this will contain a `index.html` file by default which will will contain the the html that you see displayed when you navigate to the website. There is also a `50x.html` file which will be displayed if an `500` error has occured. (But not if the index.html is missing then it will display `403 forbidden`)

#### Setting up a Dockerfile to make out own images

In our docker file we want to tell docker all the things we want to do inside the container. We want to first specify the image we want to use. We can tell docker which image to use by using: `FROM nginx:latest` then we want to make sure our local files for the website are copied to the nginx default directory inside our container
we can do that by using the `COPY` command. and it should look something like this:

```Dockerfile
FROM nginx:latest
COPY /html/index.html /usr/share/nginx/html/index.html
```


#### Setting up a docker-compose.yaml to set up services

In this file we can set up many configurations that will let docker behave the way we want. One of them is to set up services. Services are mostly miscroservices that run in a larger application. for example `nginx` being the microservice will be able 
run inside `debian` a larger application. We can configure these microservices in our `docker-compose.yaml` file. Were going to set up the service for `nginx` like this:

```yaml
services:
  nginx:
    build:
      context: .
    ports:
      - 8000:80
    volumes:
      - ./html/:/usr/share/nginx/html/
```
Here we define the keyword `services:` this will be the place where all our services will be defined. then we name our first service by name `nginx:` but this can basically be any name. The `build:` keyword will be a list of instructions when the image is build. So in this case we want to refer to the `Dockerfile` we have set up where we defined our image that we want to use. To refer to where the `Dockerfile` is whe use the keyword `context:` and then define the directory where its in. In this case that is going to be the current working directory and that represented by a `.`. You can also make use of the `dockerfile:` keyword to explicitly define the path to a docker file.

With `ports:` we can define which ports we want to docker to expose so that we can reach it through localhost.

With `volumes:` you can refer to data that can be used by the container. In this case we want to map 2 different directories, on of them being the path to the website that is on your local machine `/html/` and the other one being the default directory for nginx `/usr/share/nginx/html/` so we can use it to copy data form local to the container. 
