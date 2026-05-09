# ==========================================
# ETAPA 1: Construcción (Builder)
# ==========================================
FROM node:18-alpine AS builder

# Establecemos el directorio de trabajo dentro del contenedor
WORKDIR /app

# Copiamos solo los archivos de dependencias primero (aprovecha la caché de Docker)
COPY package*.json ./

# Instalamos las dependencias
RUN npm install

# Copiamos el resto del código fuente
COPY . .

# Compilamos la aplicación para producción
RUN npm run build 
# Nota: Si tu proyecto usa Create React App, la carpeta generada se llama "build". 
# Si usa Vite, se llama "dist". Ajusta la línea de abajo si es necesario.

# ==========================================
# ETAPA 2: Producción (Mínimo Privilegio)
# ==========================================
# Usamos una imagen oficial de Nginx preconfigurada para no ser root
FROM nginxinc/nginx-unprivileged:alpine

# Copiamos los archivos estáticos generados en la Etapa 1
# Cambia /app/build por /app/dist si usas Vite
COPY --from=builder /app/dist /usr/share/nginx/html

# Exponemos el puerto (esta imagen usa el 8080 por defecto por ser no-root)
EXPOSE 8080

# Comando para iniciar Nginx
CMD ["nginx", "-g", "daemon off;"]
