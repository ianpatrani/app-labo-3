FROM maven:3.8.4-openjdk-11-slim AS build

WORKDIR /app

COPY pom.xml .
COPY src ./src

RUN mvn clean package -DskipTests

FROM openjdk:11-jre-slim

COPY --from=build /app/target/myapp.jar /app.jar

RUN apt-get update && apt-get install -y mysql-client && rm -rf /var/lib/apt/lists/*

COPY application.properties /app/application.properties

EXPOSE 8080

CMD java -jar /app.jar --spring.config.location=file:/app/application.properties
