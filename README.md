# hit-counter

A basic Golang hit counter API to demonstrate linking docker containers based
on [https://github.com/bchav/hit-counter](https://github.com/bchav/hit-counter)
(but written in golang!)

## Installation

Clone this repository for use with:

    $ git clone https://github.com/apackeer/hit-counter

## Getting Started Using Docker Compose

Build and start the hit-counter and redis containers:

    $ docker-compose up -d --build

### Using Docker

Run a redis container, the container will export port 6379:

    $ docker run --name redis -d redis

Build the hit-counter api container:

    $ docker build -t hitcounter-api .

Run the hit-counter api container:

    $ docker run -d --publish 8080:8080 --name hitcounter-api --rm \
     --link redis:redis hitcounter-api

### Using Hit-Counter
The web app should now be listening on port 5000 on your docker daemon, we can
visit it:

    # Inside Docker Host
    $ curl localhost:8080
    {"count":1}
    $ curl localhost:5000
    {"count":2}

    # Outside Docker host
    $ curl <docker host>:8080
    {"count":3}