# Stage 1: Build the application
FROM maven:3.8.5-openjdk-11 AS build

# Set the working directory inside the container
WORKDIR /app

# Copy the Maven project file and download dependencies (caches dependencies)
COPY pom.xml .

# Copy the rest of the application source code
COPY src ./src

# Build the project and skip tests
RUN mvn clean package -DskipTests

# Stage 2: Run the application using a lightweight JRE image
FROM openjdk:11-jre-slim

# Set the working directory for the runtime
WORKDIR /app

# Copy the built JAR file from the build stage
COPY --from=build /app/target/*.jar app.jar

# Expose the necessary port
EXPOSE 8080

# Define the entrypoint command to run the JAR
ENTRYPOINT ["java", "-jar", "app.jar"]
