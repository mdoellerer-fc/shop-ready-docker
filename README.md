# shop-ready-docker
Docker-compose project with apache, php7, mysql, mailhog and phpMyAdmin

## Overview

- Apache 2.4 container PHP 7.3 ([Dockerfile](container/apache_php7/Dockerfile))
- MySQL 5.7 container ([Dockerfile](https://github.com/docker-library/mysql/blob/883703dfb30d9c197e0059a669c4bb64d55f6e0d/5.7/Dockerfile))
- MailHog container ([Dockerfile](https://github.com/mailhog/MailHog/blob/master/Dockerfile))
- phpMyAdmin container ([Dockerfile](https://hub.docker.com/r/phpmyadmin/phpmyadmin/~/dockerfile/))

## Quickstart
1. Install [docker engine](https://docs.docker.com/engine/installation/)
2. Add `127.0.0.1 localhost` to your etc/hosts file (if needed eg. windows)
3. Fire up container
```bash
# enter the repo folder:
cd shop-ready-docker
# create container
docker-compose build
# fire up container
docker-compose up
```
4. Go to your browser and type http://localhost/info.php


## Configuration


### Container
- If you would like to run container in background, use `docker-compose up -d` for starting container and `docker logs -f shop_apache` for log information (eg. composer information).

### Data
- Data (`www` and `mysql`) is storend on host: `data` directory

### Credentials
- You can change all credentials (domain, ports, database, ...) in `.env` file.



