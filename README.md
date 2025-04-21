# php-k8s-ci-cd-app

## Descripción
Este proyecto es una aplicación PHP desplegada en un clúster de Kubernetes utilizando un pipeline CI/CD. La aplicación se conecta a una base de datos MySQL y muestra una lista de personas almacenadas.

## Estructura del Proyecto

- **`Dockerfile`**: Define la imagen Docker para la aplicación PHP.
- **`public/index.php`**: Código fuente principal de la aplicación PHP.
- **`k8s/deployment.yml`**: Manifiestos de Kubernetes para desplegar la aplicación y la base de datos MySQL.
- **`.github/workflows/deploy.yml`**: Configuración del pipeline CI/CD utilizando GitHub Actions.

## CI/CD Pipeline

El pipeline CI/CD está configurado en el archivo deploy.yml y realiza los siguientes pasos:

1. **Detección de cambios en la rama principal**: El pipeline se activa automáticamente cuando se realiza un push a la rama `main`.

2. **Construcción y publicación de la imagen Docker**:
   - Se clona el repositorio.
   - Se configura Docker Buildx para la construcción de imágenes.
   - Se autentica en Docker Hub utilizando credenciales almacenadas como secretos.
   - Se construye la imagen Docker de la aplicación y se publica en Docker Hub con el tag `latest`.

3. **Despliegue en Minikube**:
   - Se clona nuevamente el repositorio en el runner local.
   - Se aplican los manifiestos de Kubernetes para desplegar la aplicación y sus dependencias.
   - Se fuerza un reinicio del despliegue de la aplicación para garantizar que se utilice la última versión de la imagen Docker.

Este pipeline asegura que los cambios realizados en el código se reflejen automáticamente en el clúster de Kubernetes. 
