# Etapa 1: Construcción (Usamos temurin para obligar a una descarga nueva y limpia)
FROM maven:3.9-eclipse-temurin-17 AS builder
WORKDIR /app

# Copiamos todo el código fuente
COPY . .

# Compilamos directamente saltando los tests
RUN mvn clean package -DskipTests

# Etapa 2: Ejecución
FROM eclipse-temurin:17-jdk-alpine
WORKDIR /app

# Copiamos el archivo .jar generado
COPY --from=builder /app/target/*.jar app.jar
EXPOSE 8080
ENTRYPOINT ["java", "-jar", "app.jar"]
