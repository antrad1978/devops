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
I used his project a template for this one.

# Introduction

Dockerfile to build an [Activiti 6 BPM](#http://www.activiti.org/) container image.


# Installation

Pull the latest version of the image from the docker hub. 

```bash
docker pull antrad1978/mysql:latest
```

Alternately you can build the image yourself.

```bash
git clone https://github.com/antrad1978/activiti6.git
cd activiti
docker build --tag="$USER/activiti6" .
```

# Quickstart

Run the activiti image

```bash
docker run -e DB_TYPE=mysql -e DB_PORT=3306 -e DB_HOST=172.17.0.2 -e DB_NAME=activiti -e DB_USER=root -e DB_PASS=root --name activiti6 -p 8080:8080  -d activiti6
```



# References

* https://github.com/eternnoir/activiti
* http://activiti.org/
* http://github.com/Activiti/Activiti
* http://tomcat.apache.org/
* http://dev.mysql.com/downloads/connector/j/5.1.html
* https://github.com/jpetazzo/nsenter
* https://jpetazzo.github.io/2014/03/23/lxc-attach-nsinit-nsenter-docker-0-9/
