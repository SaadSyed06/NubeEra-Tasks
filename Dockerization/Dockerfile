FROM centos
#Installing Java
#################
# RUN yum -y install java-1.8.0-openjdk-devel
RUN cd /etc/yum.repos.d/
RUN sed -i 's/mirrorlist/#mirrorlist/g' /etc/yum.repos.d/CentOS-*
RUN sed -i 's|#baseurl=http://mirror.centos.org|baseurl=http://vault.centos.org|g' /etc/yum.repos.d/CentOS-*
RUN yum -y install java
RUN java -version

#Installing Tomcat
##################
RUN mkdir /opt/tomcat/
WORKDIR /opt/tomcat/
# RUN curl -O https://dlcdn.apache.org/tomcat/tomcat-8/v8.5.84/bin/apache-tomcat-8.5.84-deployer.tar.gz
ENV TOMCAT_MAJOR 8
ENV TOMCAT_VERSION 8.5.0
ENV TOMCAT_TGZ_URL https://archive.apache.org/dist/tomcat/tomcat-$TOMCAT_MAJOR/v$TOMCAT_VERSION/bin/apache-tomcat-$TOMCAT_VERSION.tar.gz

#https://archive.apache.org/dist/tomcat/tomcat-8/v8.5.0/bin/apache-tomcat-8.5.0.tar.gz
RUN curl -O "$TOMCAT_TGZ_URL"
RUN tar xvzf apache-tomcat*.tar.gz
RUN mv apache-tomcat*/* /opt/tomcat/.

#Deploy Application
#####################
RUN file="$(ls /opt/tomcat/)" && echo $file
WORKDIR /opt/tomcat/webapps
RUN curl -O -L https://github.com/NubeEra-Samples/codecommit-demo/blob/master/target/ccdemo.war
EXPOSE 8083
CMD [ "/bin/bash","/opt/tomcat/bin/catalina.sh","run" ]

## http://localhost:8083/ccdemo/welcome
##Build Image
# docker build -t centos-tomcat85-image .
##Run Image as Container
# docker run -d -u root -p 8083:8083 -v /C/DockerVolumes/Centos-Tomcat85:/opt/tomcat --name centos-tomcat85-container centos-tomcat85-image:latest 