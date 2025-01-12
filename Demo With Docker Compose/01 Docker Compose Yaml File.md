<!-- Autor: Daniel Benjamin Perez Morales -->
<!-- GitHub: https://github.com/DanielPerezMoralesDev13 -->
<!-- Correo electrónico: danielperezdev@proton.me -->

# ***Docker Compose Yaml File***

*![What Is Docker Compose](https://stackoverflow.com/questions/44450265/what-is-a-docker-compose-yml-file "https://stackoverflow.com/questions/44450265/what-is-a-docker-compose-yml-file")*

*[Compose File/](https://docs.docker.com/reference/compose-file/ "https://docs.docker.com/reference/compose-file/")*
*[Docker Compose Yml Version Is Obsolete](https://forums.docker.com/t/docker-compose-yml-version-is-obsolete/141313 "https://forums.docker.com/t/docker-compose-yml-version-is-obsolete/141313")*
*[Legacy Versions](https://docs.docker.com/reference/compose-file/legacy-versions/ "https://docs.docker.com/reference/compose-file/legacy-versions/")*
*[Docker Compose Intro History](https://docs.docker.com/compose/intro/history/ "https://docs.docker.com/compose/intro/history/")*

- **Según la documentación, la versión actual del esquema de Docker Compose es "version": 3.8**

- **Problema de la configuración manual**

- **Configurar manualmente estos contenedores incluye**
  - *Crear las redes necesarias con sus configuraciones*
  - *Configurar los contenedores y sus opciones*
  - *Manejar el estado de los contenedores (iniciar, detener, reiniciar)*

- **Aunque este ejemplo es sencillo, es ideal mapear esta configuración a un archivo Docker Compose para simplificar el manejo**

> [!IMPORTANT]
> **Docker Compose crea automáticamente una red dedicada para todos los servicios definidos en el archivo**

## ***Configuración manual***

### **Crear la red para los contenedores**

```bash
docker network create mongo-network;

# Crear el contenedor de MongoDB

docker run -d \
    -p 27017:27017 \
    -e MONGO_INITDB_ROOT_USERNAME=admin \
    -e MONGO_INITDB_ROOT_PASSWORD=supersecret \
    --network mongo-network \
    --name mongo-demo \
    mongo;

# Crear el contenedor de Mongo Express

docker run -d \
    -p 8081:8081 \
    -e ME_CONFIG_MONGODB_ADMINUSERNAME=admin \
    -e ME_CONFIG_MONGODB_ADMINPASSWORD=supersecret \
    -e ME_CONFIG_MONGODB_SERVER=mongo-demo \
    -e ME_CONFIG_MONGODB_URL=mongodb://admin:supersecret@mongo-demo:27017/ \
    -e ME_CONFIG_MONGODB_ENABLE_ADMIN=true \
    -e ME_CONFIG_OPTIONS_EDITORTHEME=material-darker \
    -e ME_CONFIG_REQUEST_SIZE=100kb \
    -e ME_CONFIG_SITE_BASEURL=/ \
    -e ME_CONFIG_SITE_COOKIESECRET=cookiesecret \
    -e ME_CONFIG_SITE_SESSIONSECRET=sessionsecret \
    -e ME_CONFIG_SITE_SSL_ENABLED=false \
    -e ME_CONFIG_MONGODB_AUTH_USERNAME=admin \
    -e ME_CONFIG_MONGODB_AUTH_PASSWORD=pass \
    -e ME_CONFIG_MONGODB_PORT=27017 \
    --network mongo-network \
    --name mongo-express \
    mongo-express:latest;
```

creamos un archivo personalizado de docker compose normalmente se le suele llamar docker-compose pero nostros le llamaresmo mongo-services.yaml

touch mongo-services.yaml

```yaml
version: '3.8'
services:
  mongo-demo:
    image: mongo:latest
    ports:
      - 27017:27017
    environment:
      - MONGO_INITDB_ROOT_USERNAME=admin
      - MONGO_INITDB_ROOT_PASSWORD=supersecret
  mongo-express:
    image: mongo-express
    ports:
      - 8081:8081
    environment:
      - ME_CONFIG_MONGODB_ADMINUSERNAME=admin
      - ME_CONFIG_MONGODB_ADMINPASSWORD=supersecret
      - ME_CONFIG_MONGODB_SERVER=mongo-demo
      - ME_CONFIG_MONGODB_URL=mongodb://admin:supersecret@mongo-demo:27017/
      - ME_CONFIG_MONGODB_ENABLE_ADMIN=true
      - ME_CONFIG_OPTIONS_EDITORTHEME=material-darker
      - ME_CONFIG_REQUEST_SIZE=100kb
      - ME_CONFIG_SITE_BASEURL=/
      - ME_CONFIG_SITE_COOKIESECRET=cookiesecret
      - ME_CONFIG_SITE_SESSIONSECRET=sessionsecret
      - ME_CONFIG_SITE_SSL_ENABLED=false
      - ME_CONFIG_MONGODB_AUTH_USERNAME=admin
      - ME_CONFIG_MONGODB_AUTH_PASSWORD=pass
      - ME_CONFIG_MONGODB_PORT=27017
```
