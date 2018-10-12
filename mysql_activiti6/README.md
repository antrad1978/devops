# Table of Contents
- [Introduction](#introduction)
- [Installation](#installation)
- [Quickstart](#quickstart)

# Introduction

Dockerfile to build an [Activiti 6 BPM](#http://www.activiti.org/) container image.


# Installation

Pull the latest version of the image from the docker hub. 

```bash
docker pull antrad1978/mysql:latest
```

Alternately you can build the image yourself.

```bash
git clone https://github.com/antrad1978/devops.git
cd mysql
docker build --tag="$USER/mysql" .
```

# Quickstart

Pull image:
```bash
docker pull antrad1978/mysql_activiti6
```

Run the activiti image

```bash
docker run --name mysql_activiti6 -e MYSQL_ROOT_PASSWORD=root -d mysql_activiti6
```


# References

* https://hub.docker.com/_/mysql/
