#  LAMP stack built with Docker Compose


A basic LAMP stack environment built using Docker Compose. It consists of the following:

* PHP
* Apache
* MySQL
* phpMyAdmin

##  Installation
 
* Clone this repository on your local computer
* configure .env as needed 
* Run the `docker-compose up -d`.

```shell
git clone https://github.com/logeshg5/docker-compose-lamp.git
cd docker-compose-lamp/
// modify .env as needed
docker-compose up -d
// visit localhost
```

Your LAMP stack is now ready!! You can access it via `http://localhost`.

##  Configuration and Usage

### General Information 
This Docker Stack is build for local development and not for production usage.

### Configuration
This package comes with default configuration options. You can modify them by updating `.env` file in your root directory.

### Configuration Variables
There are following configuration variables available and you can customize them by overwritting `.env` file.

#### PHP

`PHP_VERSION`
Is used to specify which PHP version you want to use. Defaults always to latest PHP Version. 

`PHP_INI`
Define your custom `php.ini` modification to meet your requirments. 

#### Apache 

`APACHE_VERSION`
Is used to specify which Apache version you want to use. Defaults always to latest Apache Version. 

`DOCUMENT_ROOT`
It is a document root for Apache server. The default value for this is `./www`. All your sites will go here and will be synced automatically.

`VHOSTS_DIR`
This is for virtual hosts. The default value for this is `./config/vhosts`. You can place your virtual hosts conf files here.

> Make sure you add an entry to your system's `hosts` file for each virtual host.

`APACHE_LOG_DIR`
This will be used to store Apache logs. The default value for this is `./logs/apache2`.


#### Database

`DATABASE`
Define which MySQL or MariaDB Version you would like to use. 

`MYSQL_VERSION`
Is used to specify which MySQL version you want to use. Defaults always to latest MySQL Version. 

`MYSQL_DATA_DIR`
This is MySQL data directory. The default value for this is `./data/mysql`. All your MySQL data files will be stored here.

`MYSQL_LOG_DIR`
This will be used to store Apache logs. The default value for this is `./logs/mysql`.

## Web Server

Apache is configured to run on port 80. So, you can access it via `http://localhost`.

#### Apache Modules

If you want to enable  modules, just update `./apache/Dockerfile`. 

> You have to rebuild the docker image by running `docker-compose build` and restart the docker containers.

#### Connect via SSH

You can connect to web server using `docker exec` command to perform various operation on it. Use below command to login to container via ssh.

```shell
docker exec -it lamp-apache bash

# or if you use alpine based images
docker exec -it lamp-apache sh
```

> Use the right container name instead of `lamp-apache`

## PHP

The installed version of depends on your `.env` file. 

#### Extensions

Default extensions may differ based on the version and image type that you choose.

To install more extensions take a look at ![Official PHP docker](https://hub.docker.com/_/php) which gives reference to ![install-php-extensions](https://github.com/mlocati/docker-php-extension-installer) project. 

Based on that more extenstions can be installed. Here gd, zip and mysqli are installed for example. 

```
ADD https://raw.githubusercontent.com/mlocati/docker-php-extension-installer/master/install-php-extensions /usr/local/bin/
RUN chmod uga+x /usr/local/bin/install-php-extensions && sync && \
       install-php-extensions gd zip mysqli
```

> You have to rebuild the docker image by running `docker-compose build` and restart the docker containers.

## phpMyAdmin

phpMyAdmin is configured to run on port 8080. Use following default credentials.

http://localhost:8080/

username: root

password: tiger

## Credits
This repository is a result of a combination of these repositories,

https://github.com/sprintcube/docker-compose-lamp.git

https://github.com/mzazon/php-apache-mysql-containerized

Explanations can be found ![here](https://www.cloudreach.com/en/resources/blog/ct-apache-docker-containers/).

## Contributing
We are happy if you want to create a pull request or help people with their issues. If you want to create a PR, please remember that this stack is not built for production usage, and changes should be good for general purpose and not overspecialized. 

> Thank you! 

## Why you shouldn't use this stack unmodified in production
We want to empower developers to quickly create creative Applications. Therefore we are providing an easy to set up a local development environment for several different Frameworks and PHP Versions. 
In Production you should modify at a minimum the following subjects:

* php handler: mod_php=> php-fpm
* secure mysql users with proper source IP limitations

