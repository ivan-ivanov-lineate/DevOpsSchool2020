FROM centos

MAINTAINER iivanov@lineate.com

RUN mkdir /opt/tomcat/

WORKDIR /opt/tomcat
RUN curl -O https://apache-mirror.rbc.ru/pub/apache/tomcat/tomcat-8/v8.5.61/bin/apache-tomcat-8.5.61.tar.gz
RUN tar xvfz apache*.tar.gz
RUN mv apache-tomcat-8.5.61/* /opt/tomcat/.
RUN yum -y install java
RUN java -version

WORKDIR /opt/tomcat/webapps
RUN curl -O -L https://github.com/AKSarav/SampleWebApp/raw/master/dist/SampleWebApp.war

EXPOSE 8080

CMD ["/opt/tomcat/bin/catalina.sh", "run"]
