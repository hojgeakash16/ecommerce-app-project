# -----------Stage 1 : Build the app------------------

# Get the base image
FROM maven:3.9-eclipse-temurin-17 AS build

# Set the working directory 
WORKDIR /app

# Copy the source code
COPY pom.xml . 
COPY src ./src

# Install the dependencies
RUN mvn clean package -DskipTests

# ------------Stage 2 : Run with optimised image----------

# Get  the optimised image
FROM eclipse-temurin:17-jre-alpine AS run

# Create the working directory
WORKDIR /app

# Copy from the builder
COPY --from=build /app/target/server-0.0.1-SNAPSHOT.jar app.jar

# Expose the port
EXPOSE 8080

# Run the application
CMD ["java", "-jar", "app.jar"]
