# ETAPA 1: Construcción (Build) - Capa para compilar con Maven
FROM maven:3.9.4-eclipse-temurin-17-alpine AS builder
WORKDIR /app
# Copiar POM y descargar dependencias primero (Optimización de caché)
COPY pom.xml .
RUN mvn dependency:go-offline
# Copiar código fuente y empaquetar el .jar
COPY src ./src
RUN mvn clean package -DskipTests

# ETAPA 2: Producción - Capa ultra liviana solo para ejecutar Java
FROM eclipse-temurin:17-jre-alpine
WORKDIR /app

# Crear un USUARIO NO ROOT por seguridad (Mínimo privilegio)
RUN addgroup -S appgroup && adduser -S appuser -G appgroup

# Extraer el .jar de la Etapa 1 sin traer todo Maven (Multi-stage limpio)
COPY --from=builder /app/target/*.jar app.jar

# Asignar permisos al usuario creado
RUN chown -R appuser:appgroup /app

# Ejecutar como el usuario sin privilegios root
USER appuser

EXPOSE 8080
CMD ["java", "-jar", "app.jar"]