
##Full Stack App con Docker y Kubernetes
Este repositorio contiene una aplicación full stack que incluye un frontend con Node.js y Express, un backend con TypeScript y Express, y una base de datos MongoDB. El proyecto está configurado para ejecutarse en contenedores Docker y también en un clúster de Kubernetes usando Minikube.

#Tecnologías Utilizadas
Frontend: Node.js + Express
Backend: TypeScript + Express
Base de Datos: MongoDB
Contenedores: Docker
Orquestación: Kubernetes (Minikube)

Pasos para Ejecutar el Proyecto
Clonar el Repositorio:
-- repo original usado para el proyecto ---
git clone -b ejercicio2-dockeriza https://github.com/roxsross/bootcamp-devops-2023.git
cd 295topics-fullstack

--- datos a considerar ---
Variables de Entorno
MONGO_URI: URI de la base de datos MongoDB.
BACKEND_URL: URL del backend.
FRONTEND_URL: URL del frontend.
Notas
Asegúrate de que las dependencias estén correctamente instaladas revisando los archivos package.json de cada módulo (frontend y backend).
Configura adecuadamente las variables de entorno para la conexión entre los servicios.

Construir y Levantar con Docker:
Crea las imágenes Docker para cada servicio.
Asegurate de exponer los puertos correctos, de agregar los package.json, instalar dependencias y de correr la app según cómo corresponda.
Accede a la app en localhost:3000 (Frontend) y localhost:5000 (Backend).

Configuración de Minikube:

Inicia Minikube con el driver Docker:
minikube start --driver=docker -> levanta el cluster

Configura Docker para usar Minikube:
eval $(minikube -p minikube docker-env) -> agrega docker dentro del entorno de minikube

Construye las imágenes dentro de Minikube:
docker-compose build || docker build -t front-image -f dockerfile . (ejemplo para crear la imagen del front)

Desplegar en Kubernetes:
Aplica los archivos YAML para el deployment y los servicios:
- Debes de crear dos yaml por separado, para obtener una mejor lectura y estructura.
kubectl apply -f k8s-deployment.yaml -> levanta la app basicamente
kubectl apply -f k8s-services.yaml -> conecta los modulos

Verifica los pods y servicios con:
kubectl get pods
kubectl get services

Acceder a la Aplicación:
Ejecuta el siguiente comando para acceder al frontend:
minikube service frontend-service --url -> esto mostrará la ip a la cual acceder, antes, se debe de setear
en el k8s-deploymente.yaml, la forma de conexión, en este caso, utilice NodePort, y expuse el puerto 32000.
