#
# Build Stage
#
FROM maven:3.6.0-jdk-11-slim AS build
COPY src /home/app/src
COPY certs/ /app/certs/
COPY ./pom.xml /home/app
COPY ./settings.xml /home/app
COPY ./certs/signing.jks /home/app/certs/
RUN mvn -s /home/app/settings.xml -f /home/app/pom.xml -U clean install -Dcheckstyle.skip


#
# Package stage
#
FROM adoptopenjdk:11-jre-hotspot
COPY --from=build /home/app/target/*.jar /app/app.jar
WORKDIR /app
ENTRYPOINT [ "sh", "-c", "java $JAVA_OPTS -Djava.security.egd=file:/dev/./urandom -jar ./app.jar" ]
