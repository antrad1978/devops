#
# Ubuntu 14.04 with activiti Dockerfile
#
# Pull base image.
### http://blog.docker.com/2015/03/updates-available-to-popular-repos-update-your-images/
# dockerfile/java renamed to java
### 
FROM openjdk:8
LABEL Author = "Antonio Radesca" 
LABEL email = "antonio@nextgenerationteam.com"

EXPOSE 8080

ENV TOMCAT_VERSION 9.0.12
ENV ACTIVITI_VERSION 6.0.0
ENV MYSQL_CONNECTOR_JAVA_VERSION 5.1.40

# Tomcat
RUN wget -U firefox http://archive.apache.org/dist/tomcat/tomcat-9/v${TOMCAT_VERSION}/bin/apache-tomcat-${TOMCAT_VERSION}.tar.gz -O /tmp/catalina.tar.gz && \
	tar xzf /tmp/catalina.tar.gz -C /opt && \
	ln -s /opt/apache-tomcat-${TOMCAT_VERSION} /opt/tomcat && \
	rm /tmp/catalina.tar.gz && \
	rm -rf /opt/tomcat/webapps/examples && \
	rm -rf /opt/tomcat/webapps/docs

# To install jar files first we need to deploy war files manually
RUN wget https://github.com/Activiti/Activiti/releases/download/activiti-${ACTIVITI_VERSION}/activiti-${ACTIVITI_VERSION}.zip -O /tmp/activiti.zip && \
 	unzip /tmp/activiti.zip -d /opt/activiti && \
	unzip /opt/activiti/activiti-${ACTIVITI_VERSION}/wars/activiti-admin.war -d /opt/tomcat/webapps/activiti-admin && \
	unzip /opt/activiti/activiti-${ACTIVITI_VERSION}/wars/activiti-app.war -d /opt/tomcat/webapps/activiti-app && \
	unzip /opt/activiti/activiti-${ACTIVITI_VERSION}/wars/activiti-rest.war -d /opt/tomcat/webapps/activiti-rest && \
	rm -f /tmp/activiti.zip && \
	rm -f /opt/tomcat/webapps/activiti-app/classes/activiti-app.properties && \
	rm -f /opt/tomcat/webapps/activiti-admin/WEB-INF/classes/META-INF/activiti-admin/activiti-admin.properties

# Add mysql connector to applicd...cation
ADD mysql-connector-java-5.1.40.jar /tmp/mysql-connector-java.jar
RUN	cp /tmp/mysql-connector-java.jar /opt/tomcat/webapps/activiti-app/WEB-INF/lib/ && \
	cp /tmp/mysql-connector-java.jar /opt/tomcat/webapps/activiti-admin/WEB-INF/lib/ && \
	cp /tmp/mysql-connector-java.jar /opt/tomcat/webapps/activiti-rest/WEB-INF/lib/ 

# Add roles
ADD assets /assets
COPY ./assets/config/tomcat-users.xml /assets/config/tomcat/tomcat-users.xml
COPY ./assets/init /assets/init
COPY ./assets/config/activiti-admin.properties /opt/tomcat/webapps/activiti-admin/WEB-INF/classes/META-INF/activiti-admin/activiti-admin.properties
RUN ls /assets/config/tomcat/
RUN cp /assets/config/tomcat/tomcat-users.xml /opt/apache-tomcat-${TOMCAT_VERSION}/conf/

CMD ["/assets/init"]

