# Docker images for MongoDB

## BUILD

```
$ docker build --tag my/repo .
```

## RUN

### Before running

Before running this docker image, please make sure to create the following dirs:

```
sudo mkdir -p /srv/mongo/data
sudo mkdir -p /srv/mongo/logs
```

To change the config file, edit `config/mongod.conf`.

### Running with `docker` command

```
# Basic way
# Usage: docker run --name <name for container> -d <user-name>/<repository>
docker run -p 27017:27017 --name mongo_instance_001 -d my/repo

# Dockerized MongoDB, lean and mean!
# Usage: docker run --name <name for container> -d <user-name>/<repository> --noprealloc --smallfiles
docker run -p 27017:27017 --name mongo_instance_001 -d my/repo --smallfiles

# Checking out the logs of a MongoDB container
# Usage: docker logs <name for container>
docker logs mongo_instance_001

# Playing with MongoDB
# Usage: mongo --port <port you get from `docker ps`>
mongo --port 27017

# If using docker-machine
# Usage: mongo --port <port you get from `docker ps`>  --host <ip address from `docker-machine ip VM_NAME`>
mongo --port 27017 --host 192.168.59.103
```

If you want to run two containers on the same engine, then you will need to map the exposed port to two different ports on the host:

```
# Start two containers and map the ports
docker run -p 28001:27017 --name mongo_instance_001 -d my/repo
docker run -p 28002:27017 --name mongo_instance_002 -d my/repo

# Now you can connect to each MongoDB instance on the two ports
mongo --port 28001
mongo --port 28002
```

### Running with `run` script

```
./run [image_name] [container_name]
```

## TODO

* Mount data volume locally
* Build MongoDB Cluster

## LICENSE

MIT
