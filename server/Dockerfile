# -----------Stage 1 : Build the app------------------

FROM maven:3.9-eclipse-temurin-17 AS build

WORKDIR /app/server

COPY pom.xml .
COPY src ./src

RUN mvn package -DskipTests -Dcheckstyle.skip=true

# ------------Stage 2 : Run with optimised image----------

FROM eclipse-temurin:17-jre AS run

WORKDIR /app

COPY --from=build /app/server/target/server-0.0.1-SNAPSHOT.jar app.jar

EXPOSE 8080

CMD ["java", "-jar", "app.jar"]