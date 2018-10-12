# Table of Contents
- [Thanks](#thanks)
- [Introduction](#introduction)
    - [Version](#version)
    - [Changelog](Changelog.md)
- [Installation](#installation)
- [Quickstart](#quickstart)
- [Configuration](#configuration)
  - [Database](#database)
  - [Available Configuration Parameters](#available-configuration-parameters)

# Thanks

Special thanks to https://github.com/eternnoir/activiti
I used his project as template for this one.

# Introduction

Dockerfile to build an [Activiti 6 BPM](#http://www.activiti.org/) container image.


# Installation

Pull the latest version of the image from the docker hub. 

```bash
docker pull antrad1978/activiti6:latest
```

Every image is tagged, but please use `latest`. For example,

```bash
docker pull antrad1978/activiti6:latest
```

Alternately you can build the image yourself.

```bash
git clone https://github.com/antrad1978/devops.git
cd activiti6_docker
docker build --tag="$USER/activiti6" .
```

# Quickstart

Run the activiti image

```bash
docker run -e DB_TYPE=mysql -e DB_PORT=3306 -e DB_HOST=172.17.0.2 -e DB_NAME=activiti -e DB_USER=root -e DB_PASS=root --name activiti6 -p 8080:8080  -d activiti6
```

Point your browser to `http://localhost:8080/activiti-app` and login using the default username and password:

* username: **kermit**
* password: **kermit**

Point your browser to `http://localhost:8080/activiti-admin` for admin app and login using the default username and password:

* username: **admin**
* password: **admin**

You should now have the Activiti application up and ready for testing. If you want to use this image in production the please read on.


## Database

This Activiti 6 image uses a MySql database backend to store its data.

### MySQL

#### External MySQL Server

The image can be configured to use an external MySQL database instead of starting a MySQL server internally. The database configuration should be specified using environment variables while starting the Activiti image.

 You could find here some useful info:
`https://severalnines.com/blog/mysql-docker-containers-understanding-basics`


Before you start the Activiti image create user and database for activiti. The complete data structure will be created by Hibernate.

```sql
CREATE USER 'activiti'@'%.%.%.%' IDENTIFIED BY 'password';
CREATE DATABASE IF NOT EXISTS `activiti` DEFAULT CHARACTER SET `utf8` COLLATE `utf8_unicode_ci`;
GRANT ALL PRIVILEGES ON `activiti`.* TO 'activiti'@'%.%.%.%';
```

We are now ready to start the Activiti application.

*Assuming that the mysql server host is 192.0.2.1*

```bash
docker run --name=activiti -d \
  -e 'DB_HOST=192.0.2.1’ -e 'DB_NAME=activiti' -e 'DB_USER=activiti’ -e 'DB_PASS=password' \
antrad1978/activiti6:latest
```

#### Linking to MySQL Container

You can link this image with a mysql container for the database requirements. The alias of the mysql server container should be set to **mysql** while linking with the activiti image.

If a mysql container is linked, only the `DB_TYPE`, `DB_HOST` and `DB_PORT` settings are automatically retrieved using the linkage. You may still need to set other database connection parameters such as the `DB_NAME`, `DB_USER`, `DB_PASS` and so on.

By the way this is not the best way to use Docker, better use networking.

### Available Configuration Parameters

*Please refer the docker run command options for the `--env-file` flag where you can specify all required environment variables in a single file. This will save you from writing a potentially long docker run command.*

Below is the complete list of available options that can be used to customize your activiti installation.

- **TOMCAT_ADMIN_USER**: Tomcat admin user name. Defaults to `admin`.
- **TOMCAT_ADMIN_PASSWORD**: Tomcat admin user password. Defaults to `admin`.
- **DB_HOST**: The database server hostname. Defaults to ``.
- **DB_PORT**: The database server port. Defaults to `3306`.
- **DB_NAME**: The database database name. Defaults to ``.
- **DB_USER**: The database database user. Defaults to ``.
- **DB_PASS**: The database database password. Defaults to ``.

# Maintenance

## Shell Access

For debugging and maintenance purposes you may want access the container shell. Since the container does not allow interactive login over the SSH protocol, you can use the [nsenter](http://man7.org/linux/man-pages/man1/nsenter.1.html) linux tool (part of the util-linux package) to access the container shell.

Some linux distros (e.g. ubuntu) use older versions of the util-linux which do not include the `nsenter` tool. To get around this @jpetazzo has created a nice docker image that allows you to install the `nsenter` utility and a helper script named `docker-enter` on these distros.

To install the nsenter tool on your host execute the following command.

```bash
docker run --rm -v /usr/local/bin:/target jpetazzo/nsenter
```

Now you can access the container shell using the command

```bash
sudo docker-enter activiti
```

For more information refer https://github.com/jpetazzo/nsenter

Another tool named `nsinit` can also be used for the same purpose. Please refer https://jpetazzo.github.io/2014/03/23/lxc-attach-nsinit-nsenter-docker-0-9/ for more information.

# References

* https://github.com/eternnoir/activiti
* http://activiti.org/
* http://github.com/Activiti/Activiti
* http://tomcat.apache.org/
* http://dev.mysql.com/downloads/connector/j/5.1.html
* https://github.com/jpetazzo/nsenter
* https://jpetazzo.github.io/2014/03/23/lxc-attach-nsinit-nsenter-docker-0-9/
