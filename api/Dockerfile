FROM maven:3.8.5-openjdk-17-slim AS build

WORKDIR /app

COPY pom.xml .

COPY src ./src

RUN mvn clean package -Dquarkus.package.type=uber-jar

FROM eclipse-temurin:17.0.10_7-jdk-alpine

WORKDIR /app

COPY --from=build /app/target/tlcdemoApp-1.0.0-SNAPSHOT-runner.jar /app/app.jar

EXPOSE 8080

CMD ["java", "-jar", "app.jar"]