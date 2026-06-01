# Etapa 1: Compilación de la aplicación con Maven
FROM maven:3.8.5-openjdk-17 AS build
WORKDIR /app

# Copiar dependencias y código fuente
COPY pom.xml .
COPY src ./src

# Compilar saltándose los tests para ahorrar tiempo en GitHub
RUN mvn clean package -DskipTests

# Etapa 2: Imagen final de ejecución
FROM openjdk:17-jdk-slim
WORKDIR /app

# Copiar el JAR generado desde la etapa anterior
COPY --from=build /app/target/*.jar app.jar

# Exponer el puerto por defecto de Spring Boot
EXPOSE 8080

ENTRYPOINT ["java", "-jar", "app.jar"]