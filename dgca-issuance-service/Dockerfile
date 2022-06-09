#
# Build Stage
#
FROM maven:3.6.0-jdk-11-slim AS build
COPY src /home/app/src
COPY ./pom.xml /home/app
COPY ./settings.xml /home/app
RUN mvn -s /home/app/settings.xml -f /home/app/pom.xml clean package


#
# Package stage
#
#FROM adoptopenjdk:11-jre-hotspot
#COPY ./target/*.jar /app/app.jar
#COPY ./certs/test /app/certs/test
#COPY ./context/context.json /app/context/context.json
#WORKDIR /app
FROM adoptopenjdk:11-jre-hotspot
COPY --from=build /home/app/target/*.jar /app/app.jar
COPY ./certs/test /app/certs/test
COPY ./context/context.json /app/context/context.json
WORKDIR /app
ENTRYPOINT [ "sh", "-c", "java $JAVA_OPTS -Djava.security.egd=file:/dev/./urandom -jar ./app.jar" ]
