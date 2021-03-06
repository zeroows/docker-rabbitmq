# RabbitMQ Dockerfile

A Dockerfile that produces a Docker Image for [RabbitMQ](https://www.rabbitmq.com/).

## RabbitMQ version

The `master` branch currently hosts RabbitMQ 3.6.0

The Dockerfile can be founded [here](https://github.com/zeroows/docker-rabbitmq).

## Usage

### Build the image

To create the image `zeroows/rabbitmq`, execute the following command on the `docker-rabbitmq` folder:

```
$ docker build -t zeroows/rabbitmq .
```

### Run the image

To run the image and bind to host port 5672:

```
$ docker run -d --name rabbitmq -p 5672:5672 zeroows/rabbitmq
```

If you want also to expose the RabbitMQ Management interface, you will need also to expose port 15672:

```
$ docker run -d --name rabbitmq -p 5672:5672 -p 15672:15672 zeroows/rabbitmq
```

The first time you run your container, a new user `rabbitmq` with all privileges will be created with a random password.
To get the password, check the logs of the container by running:

```
docker logs <CONTAINER_ID>
```

You will see an output like the following:

```
========================================================================
RabbitMQ User: "rabbitmq"
RabbitMQ Password: "8psfzXmp6t23rKr6"
RabbitMQ Virtual Host: "/"
========================================================================
```

#### Credentials

If you want to preset credentials instead of a random generated ones, you can set the following environment variables:

* `RABBITMQ_USERNAME` to set a specific username
* `RABBITMQ_PASSWORD` to set a specific password
* `RABBITMQ_VHOST` to set a specific Virtual Host

On this example we will preset our custom username and password:

```
$ docker run -d \
    --name rabbitmq \
    -p 5672:5672 \
    -e RABBITMQ_USERNAME=myusername \
    -e RABBITMQ_PASSWORD=mypassword \
    -e RABBITMQ_VHOST=myvhost \
    zeroows/rabbitmq
```

## Copyright

Copyright (c) 2016 Abdulrhman Alkhodiry. See [LICENSE](https://github.com/zeroows/docker-rabbitmq/blob/master/LICENSE) for details.

Thanks to [Ferran Rodenas](https://github.com/frodenas/docker-rabbitmq)
