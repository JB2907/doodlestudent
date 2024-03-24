# FROM ubuntu
# COPY . .
# RUN apt-get update && apt-get install --no-install-recommends -y\
#     openjdk-11-jdk
# RUN ./mvnw package -Dmaven.test.skip=true
# EXPOSE 8080
# CMD ["java", "-jar", "target/tlcApp-1.0.0-SNAPSHOT-runner.jar"]

# First stage: Build stage
# FROM maven:3.9.6-eclipse-temurin-17-alpine AS builder

# WORKDIR /app

# # Copy the project files
# COPY . /app

# # Build the project

# RUN mvn dependency:copy-dependencies

# RUN mvn -N io.takari:maven:wrapper -Dmaven=3.9.6

# RUN mvn clean package -Dquarkus.package.type=uber-jar

# # Second stage: Production image
# FROM eclipse-temurin:17-jre-alpine

# # WORKDIR /app

# # Copy only necessary artifacts from the builder stage
# COPY --from=builder /app/target/tlcdemoApp-1.0.0-SNAPSHOT-runner.jar ./target/tlcdemoApp-1.0.0-SNAPSHOT-runner.jar

# # EXPOSE 8080

# CMD java -jar ./target/tlcdemoApp-1.0.0-SNAPSHOT-runner.jar

# Command to run the application
# CMD ["java", "-jar", "./target/tlcApp-1.0.0-SNAPSHOT-runner.jar"]

FROM maven:3.8.5-openjdk-17-slim AS build

# Set the working directory inside the container
WORKDIR /app

# Copy the pom.xml file
COPY pom.xml .

# Copy the source code
COPY src ./src

# Build the application
RUN mvn clean package -Dquarkus.package.type=uber-jar

# Stage 2: Create the runtime image
FROM eclipse-temurin:17.0.10_7-jdk-alpine

# Set the working directory inside the container
WORKDIR /app

# Copy the über-jar file from the build stage
COPY --from=build /app/target/tlcdemoApp-1.0.0-SNAPSHOT-runner.jar /app/app.jar

# Expose the port your application runs on
EXPOSE 8080

# Command to run the application
CMD ["java", "-jar", "app.jar"]