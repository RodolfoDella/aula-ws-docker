# Running your Jar Application with docker-compose

The objective of this documentation is to show how to run a Jar application as a service using the Docker and docker-compose.
I'll assume that you have the Docker and docker-compose installed and a jar application, already.
First, you need to create a `docker-compose.yml` file and declare in your file, an image, volumes and command properties.

Declare the official image of Java 8 JDK.
```
image: openjdk:8-jdk
``` 
Declare one volume for your jar file.
```

volumes:
      - ./webservice/aula-swarm.jar:/aula-swarm.jar
```
And finally, in command properties, is where all happens, here you can declare a bash command passing you java command, `java -jar aula-swarm.jar` you can pass other parameters if you need

In the end, you should have something like this file bellow

```
version: '3.3'
services:
  api:
    image: openjdk:8-jdk
    restart: always
    environment:
      - TZ=America/Sao_Paulo
    volumes:
      - ./webservice/aula-swarm.jar:/aula-swarm.jar
      - ./webservice/project-defaults.yml:/project-defaults.yml
    command: bash -c "java -Xmx512m -Xss512m -Djava.net.preferIPv4Stack=true -Djava.net.preferIPv4Addresses -Dfile.encoding=UTF-8 -jar aula-swarm.jar -s project-defaults.yml"
    ports:
      - 8080:8080
```
