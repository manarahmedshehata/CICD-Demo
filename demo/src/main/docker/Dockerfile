FROM deploymentcoe/openjdk:8u111-jdk-alpine
WORKDIR /home/demo
EXPOSE 8080
USER demo
#RUN cd /home/demo
VOLUME /tmp
ADD employees-app-1.0-SNAPSHOT-jar-with-dependencies.jar demo-app.jar
ENTRYPOINT ["java","-Djava.security.egd=file:/dev/./urandom","-Xmx512M","-jar","demo-app.jar","--debug"]
