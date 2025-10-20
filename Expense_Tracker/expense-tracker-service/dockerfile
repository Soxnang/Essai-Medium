# Étape 1 : Build du projet avec Maven + Java 21(jdk 21)
FROM maven:3.9.6-eclipse-temurin-21 AS build
WORKDIR /app

# 1. Copier seulement le pom.xml et télécharger les dépendances
COPY pom.xml .
RUN mvn dependency:go-offline

# 2. Copier le code source et builder
COPY src ./src
RUN mvn clean package -DskipTests

# Étape 2 : Création de l'image finale avec Java 21 légère
FROM eclipse-temurin:21-jre-alpine
WORKDIR /app
COPY --from=build /app/target/*.jar app.jar
EXPOSE 8080
ENTRYPOINT ["java", "-jar", "app.jar"]