# Table of Contents
- [Introduction](#introduction)
- [Installation](#installation)
- [Quickstart](#quickstart)


# Introduction

Dockerfile to build an [Activiti 6 BPM](#http://www.activiti.org/) container image configuration-ready. YAML file contains a full template for Activiti 6 that eventually you could customize for your needs.

# Installation

You can submit template file to Openshift using this command:

```bash
oc create -f template.yaml
```

# Quickstart

It is possible to create your custom docker image simply changing configuration files attached and adding your custom wars.

# References

* http://activiti.org/
* http://github.com/Activiti/Activiti
* http://tomcat.apache.org/
* http://dev.mysql.com/downloads/connector/j/5.1.html
* https://docs.openshift.com/container-platform/3.11/dev_guide/index.html