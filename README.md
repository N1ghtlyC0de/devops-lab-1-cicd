# DevOps Lab 01: CI/CD con GitHub Actions y Amazon ECS

## Objetivo
Este proyecto tiene como objetivo automatizar el ciclo de integración y despliegue continuo (CI/CD) de una aplicación contenerizada escrita en Python con FastAPI. El despliegue se realiza hacia AWS ECS (Elastic Container Service) sobre instancias EC2 administradas por un Auto Scaling Group, utilizando un Pipeline de GitHub Actions.

## La Aplicación
La aplicación que se despliega es una API REST construida con FastAPI que expone dos endpoints principales:
* **`GET /`**: Saludo personalizado recibiendo `first_name` y `last_name` por query parameters.
* **`GET /health`**: Endpoint de monitoreo de salud para el orquestador de contenedores.

El contenedor utiliza una imagen ligera basada en `python:3.12-slim` y ejecuta la aplicación internamente con Uvicorn expuesto en el puerto 8000.

## Etapas del Pipeline (GitHub Actions)
El flujo de trabajo automatizado cuenta con 4 etapas:
1. **Linter**: Análisis estático de código utilizando Pylint.
2. **Pruebas Unitarias**: Ejecución de pruebas automatizadas utilizando Pytest.
3. **Construcción y Publicación de Contenedor**: Empaquetado de la imagen de Docker y su publicación en Amazon ECR (Elastic Container Registry).
4. **Despliegue a AWS ECS**: Despliegue automatizado e idempotente sobre un cluster ECS en instancias EC2 `t3.micro` asociadas a un Auto Scaling Group.