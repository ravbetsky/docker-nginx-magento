#docker-nginx-magento
Docker NGINX + Magento container


## About

This container is optimized for running Magento using NGINX and PHP-FPM, with enabled ionCube PHP loader for encrypted modules.

## Usage by example

### Install on Ubuntu

```sh
docker-compose up -d
```

### Install on OS X

```sh
docker-machine-nfs
docker-compose up -d
```
Activates NFS on docker-machine virtualbox:
https://github.com/adlogix/docker-machine-nfs

### Import database

Put "dump.sql.gz" to project root folder and execute script:

```sh
docker exec -it kmplzt_web_1 /scripts/import.sh
```

Where kmplzt_web_1 the project cotainer name, for show list of containers in current directory use:

```sh
docker-compose ps
```


### My /etc/hosts on my Mac looks like:

```sh
127.0.0.1    localhost
192.168.59.103	  dockerhost mysql kmplzt.dev
```

### using with ionCube extensions

Some extensions require ionCube and this docker image has pre-installed ionCube module. But you need to set server_name in `/etc/ngnix/conf.d/sites-enabled/default` (inside the container) corresponding to allowed domain names. For example for allowed domains like `*.allow-site.dev` server_name can be like this:

```sh
# Make site accessible from http://docker.allow-site.dev/
server_name docker.allow-site.dev;
```

### On a Linux box, it will look like this:

```sh
127.0.0.1    localhost kmplzt.dev
```

#### XDebug start/stop:

```shell
./scripts/xdebug-start.sh
./scripts/xdebug-stop.sh
```

## Comments

In our example the magento container is linked to the mysql container under the alias db.
This means that you'll have to edit your config file in such a way that the mysql host is no longer localhost but db.


Regards,
