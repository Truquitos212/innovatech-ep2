# 📦 Innovatech: Sistema de Ventas y Despachos

Sistema de **ventas y despachos** con dos APIs REST en Spring Boot y un frontend en React. Se despliega en **AWS EC2** con Docker Compose mediante un pipeline de GitHub Actions.

Proyecto de la asignatura **Ingeniería DevOps (ISY1101)**, Evaluación Parcial 2, DuocUC.

## Stack

- **Backend:** Java 17, Spring Boot (Web, Data JPA, Validation), MySQL
- **Frontend:** React + Vite, Tailwind CSS, React Router, React Hook Form, Axios
- **Infra:** Docker, Docker Compose, AWS EC2
- **CI/CD:** GitHub Actions (SCP + SSH al servidor)

## APIs

| Servicio | Ruta base | Operaciones |
|---|---|---|
| Ventas | `/api/v1/ventas` | listar, obtener, crear, actualizar, eliminar |
| Despachos | `/api/v1/despachos` | listar, obtener, crear, actualizar, eliminar |

## Pipeline CI/CD

`.github/workflows/deploy.yml`:

1. Descarga el código
2. Copia los archivos a la instancia EC2 (SCP)
3. Levanta los servicios con `docker compose` por SSH

Las credenciales del servidor se guardan como **GitHub Secrets**.

## Estructura

```
back-Ventas_SpringBoot/     API de ventas
back-Despachos_SpringBoot/  API de despachos
front_despacho/             frontend React
docker-compose.yml
```

## Ejecución local

```bash
docker compose up --build
```

## Capturas

<img width="1910" height="807" alt="image" src="https://github.com/user-attachments/assets/0e133acd-0912-4de7-b88f-c134ba38380e" />

<img width="1365" height="727" alt="Captura de pantalla 2026-05-08 211341" src="https://github.com/user-attachments/assets/a035dff4-a823-48e5-9ba7-6ba111694686" />

<img width="4080" height="2296" alt="20260508_210415" src="https://github.com/user-attachments/assets/1dc7ff21-85f6-427a-8a11-f43d80532e78" />

<img width="4080" height="2296" alt="20260508_210420" src="https://github.com/user-attachments/assets/1cea2236-0c35-424c-a45e-fb12b0237000" />

<img width="4080" height="2296" alt="20260508_210410" src="https://github.com/user-attachments/assets/dc54cb67-9dc8-4f86-83a1-0f9a1d79f4a2" />
