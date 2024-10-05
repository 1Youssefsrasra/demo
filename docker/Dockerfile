# Use a base image with JDK and Maven pre-installed
FROM maven:3.8.6-openjdk-17 AS build

# Set the working directory inside the container
WORKDIR /demo

# Copy the pom.xml and the source code to the working directory
COPY pom.xml .
COPY src ./src

# Run Maven to build the application
RUN mvn clean package

# Use a smaller base image for running the application
FROM openjdk:17-jdk-slim

# Set the working directory in the runtime container
WORKDIR /demo

# Copy the built JAR file from the previous stage
COPY --from=build /demo/target/demo-0.0.1-SNAPSHOT.jar demo.jar

# Expose the port the application runs on
EXPOSE 8081

# Command to run the application
ENTRYPOINT ["java", "-jar", "demo.jar"]
