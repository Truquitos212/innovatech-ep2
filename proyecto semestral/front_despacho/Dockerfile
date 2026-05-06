# ETAPA 1: Construcción (Build) - Capa para instalar y compilar
FROM node:18-alpine AS builder
WORKDIR /app
# Copiar dependencias primero para optimizar la caché de capas (Rendimiento)
COPY package*.json ./
RUN npm install
# Copiar el resto del código y compilar
COPY . .
RUN npm run build

# ETAPA 2: Producción - Capa liviana y segura
FROM nginx:alpine
WORKDIR /usr/share/nginx/html
# Limpiar el contenido por defecto de Nginx (Limpieza de capas)
RUN rm -rf ./*
# Copiar los estáticos compilados desde la Etapa 1
COPY --from=builder /app/dist .  

# Configurar Nginx para correr como USUARIO NO ROOT (Seguridad exigida en pauta)
RUN chown -R nginx:nginx /var/cache/nginx && \
    chown -R nginx:nginx /var/log/nginx && \
    chown -R nginx:nginx /etc/nginx/conf.d && \
    touch /var/run/nginx.pid && \
    chown -R nginx:nginx /var/run/nginx.pid && \
    chown -R nginx:nginx /usr/share/nginx/html

# Cambiamos al usuario de menores privilegios
USER nginx

EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]