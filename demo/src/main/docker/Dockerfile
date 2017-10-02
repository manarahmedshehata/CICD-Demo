FROM openjdk:8u111-jdk-alpine
RUN adduser -D demo
RUN chown demo:root -R /usr/lib/jvm/java-1.8-openjdk/ 
WORKDIR /home/demo
EXPOSE 8080
USER demo	
VOLUME /tmp
ADD employees-app-1.0-SNAPSHOT-jar-with-dependencies.jar demo-app.jar
ENTRYPOINT ["java","-Djava.security.egd=file:/dev/./urandom","-Xmx512M","-jar","demo-app.jar","--debug"]