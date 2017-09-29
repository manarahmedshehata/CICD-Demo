FROM openjdk:8u111-jdk-alpine 

EXPOSE 8080
RUN adduser -D demo
#RUN adduser demo sudo
USER demo
RUN apk update
RUN apk upgrade
RUN apk add bash-completion
VOLUME /tmp
ADD employees-app-1.0-SNAPSHOT-jar-with-dependencies.jar demo-app.jar
ENTRYPOINT ["java","-Djava.security.egd=file:/dev/./urandom","-Xmx512M","-jar","/demo-app.jar","--debug"]
