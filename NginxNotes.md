# Nginx Notes

### Table of contents

- 1 [What is Nginx](#nginx)
- 2 [Setting up Nginx](#setup)


### What is nginx?

Nginx is a web server that can be used as a reverse proxy, load balancer, mail proxy, HTTP cache. Its developed by Igor Sysoev, and released in 2004. Its free and open source.


### Setting up Nginx


### Setting up Nginx with docker

Open en new folder and inside the new folder run the command `docker pull nginx` to pull an image from the docker site.
This will automatically create an image inside docker that we can now run.

To run the container use the following command: `docker run --name nginx-webserver -it --rm -d -p 8000:80 nginx`

`--name` Gives the server a name

`-it` Will tell docker to allocate a sudo connection so that we can interact with the terminal.

`--rm` Removes or stops any containers that might already be running

`-d` Runs it as a deamon (background process)

`-p` Defines the port of the server

This will start a docker container that listens from port 80 and we can access the website by going to `localhost:8000`

#### Checking the status of the server

To check the status of the server you can check if it runs by going to `localhost:8000` or curl it in the temrinal by using `curl localhost:8000` or in powershell `curl https://localhost:8000`.











