#
# Ubuntu 14.04 with activiti Dockerfile
#
# Pull base image.
### http://blog.docker.com/2015/03/updates-available-to-popular-repos-update-your-images/
# dockerfile/java renamed to java
### 
FROM tomcat:9.0.12-jre8
LABEL Author = "Antonio Radesca" 
LABEL email = "antonio@nextgenerationteam.com"

ADD ./apache-tomcat-9.0.12/webapps/activiti-admin.war /usr/local/tomcat/webapps/
ADD ./apache-tomcat-9.0.12/webapps/activiti-app.war /usr/local/tomcat/webapps/
ADD ./apache-tomcat-9.0.12/webapps/activiti-rest.war /usr/local/tomcat/webapps/

COPY ./assets/config/tomcat-users.xml /usr/local/tomcat/conf/
#Set correct permissions for production environment
RUN chmod 777 /usr/local/tomcat/webapps/

EXPOSE 8080

