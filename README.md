### PyCaret Insurance App (Docker + Web App)

Este proyecto implementa una aplicación web basada en Machine Learning utilizando **PyCaret**, desplegada mediante **Docker**., busca desarrollar una aplicación web que sea capaz de brindar a los usuarios de una compañía de seguros repuestas de cual es el los cargos a los pacientes que que se asigna a cada uno según las características, datos demográficos y métricas básicas. 

La aplicación permite a los usuarios ingresar datos a través de una interfaz web y obtener predicciones en tiempo real, demostrando cómo llevar un modelo de Machine Learning desde el desarrollo hasta un entorno productivo

Objetivo

Desplegar un modelo de Machine Learning como un servicio web accesible desde el navegador, aplicando buenas prácticas de:

- Contenedores(Docker)
- Despliegue en la nube (Azure Web App)
- Integración con Azure Container Registry
- Exposición del modelo mediante una API web (Flask)


## Tecnologías utilizadas

- Python
- Flask
- PyCaret
- Docker
- Azure App Service


##  ¿Cómo funciona?

El proyecto está compuesto por el siguiente flujo del sistema:

1. El usuario ingresa datos en la interfaz web
2. Flask recibe la solicitud
3. Se cargan el modelo y el pipeline entrenado
4. Se procesan los datos de entrada
5. El modelo genera una predicción
6. El resultado se muestra en la interfaz web

El flujo es:

Usuario → Web App → Modelo → Predicción

##  Uso de Docker

Docker permite empaquetar la aplicación con todas sus dependencias, garantizando que funcione de manera consistente en cualquier entorno.

El contenedor incluye:

- Aplicación Flask
- Modelo entrenado
- Dependencias del proyecto


##  Ejecución local

### 1. Clonar repositorio

git clone https://github.com/TU-USUARIO/TU-REPO.git
cd TU-REPO, (en este caso el de Sandra Ramirez o Maria Jose Caicedo)

### 2. Construir imagen Docker

docker build -t pycaret-app .

### 3. Ejecutar contenedor

docker run -p 5000:5000 pycaret-app

### 4. Abrir en navegador

http://localhost:5000

### Pasos generales
Construir la imagen Docker **docker build -t pycaret-app .**: Se crea una imagen Docker que contiene toda la aplicación junto con sus dependencias. Esto incluye el código en Flask, el modelo de Machine Learning entrenado y las librerías necesarias para su ejecución.
El archivo Dockerfile define las instrucciones para construir esta imagen, como la versión de Python, la instalación de dependencias y el comando de inicio de la aplicación.

Ejecutar el contenedor **docker run -p 5000:5000 pycaret-app**:
Una vez construida la imagen, se sube a Azure Container Registry para que este disponible en la nube y pueda ser utilizada por otros servicios, como Azure App Service.
El proceso incluye autenticar Docker con el registro, etiquetar la imagen correctamente y realizar el push. De esta manera, la imagen queda almacenada y lista para ser desplegada.

Abrir en navegador **http://localhost:5000**
Se crea una aplicación en Azure App Service configurada para ejecutar contenedores. Se selecciona la imagen almacenada en ACR como origen de la aplicación. Azure se encarga de descargar la imágen y ejecutar el contenedor automáticamente. para después configurar las variables de entorno importantes, como el puerto en el que la aplicación WEBSITES_PORT = 5000, lo cual es necesario para que Azure pueda enrutar correctamente el tráfico hacia la aplicación.

### Despliegue en Azure
Este proyecto fue desplegado utilizando servicios de Microsoft Azure para garantizar disponibilidad y escalabilidad:
- Azure Container Registry (ACR): aquí se almacena la imagen Docker
- Azure Web App for Containers: aquí se realiza la ejecución de la aplicación  

### Flujo de despliegue

Se construyó la imagen Docker de la aplicación  
Se publicó la imagen en Azure Container Registry  
Se configuró una Web App para consumir la imagen desde ACR  
Azure ejecuta automáticamente el contenedor  
La aplicación queda disponible mediante una URL pública  
Este proceso permite llevar el modelo de Machine Learning a un entorno accesible desde cualquier lugar.

## CI/CD Pipeline

This project implements a complete CI/CD pipeline using GitHub Actions. 

Every time a change is pushed to the main branch:

- Automated tests are executed using pytest
- A Docker image is built
- The image is pushed to Azure Container Registry (ACR)
- The application is automatically deployed to Azure Web App

This ensures continuous integration and continuous deployment, improving reliability and reducing manual work.
