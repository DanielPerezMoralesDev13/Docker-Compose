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

### **Usando un archivo personalizado de Docker Compose**

- *Cuando creamos un archivo personalizado de Docker Compose, a menudo se le llama **`docker-compose.yml`**. Sin embargo, si decidimos darle un nombre diferente (en este caso, **`mongo-services.yaml`**), debemos asegurarnos de indicarlo correctamente al ejecutar los comandos de Docker Compose.*

- *Por ejemplo, si hemos creado el archivo personalizado **`mongo-services.yaml`**, lo primero que debemos hacer es asegurarnos de estar en el directorio donde se encuentra el archivo. Si no estamos en la misma ubicación, debemos utilizar el parámetro **`-f`** o **`--file`** para especificar la ruta al archivo de configuración.*

### **Creación del archivo personalizado**

- *Para crear un archivo con el nombre **`mongo-services.yaml`**, simplemente ejecutamos:*

```bash
touch mongo-services.yaml
```

- *Esto creará un archivo vacío que podemos editar con nuestra configuración personalizada de Docker Compose.*

### **Ejecutando Docker Compose con un archivo personalizado**

- *Si usamos un archivo con un nombre diferente o si no estamos ubicados en el directorio donde se encuentra el archivo **`docker-compose.yml`** (o en este caso **`mongo-services.yaml`**), debemos especificar la ubicación del archivo utilizando el parámetro **`-f`** o **`--file`**. Podemos proporcionar una **ruta relativa** o **absoluta** al archivo.*

**Ejemplo:** *Si el archivo **`mongo-services.yaml`** se encuentra en una subcarpeta llamada **`Version 1 Mongo Services`**, debemos usar:*

```bash
docker compose -f ./Directory/mongo-services.yaml up
```

### **Detalles importantes**

- **Ruta relativa:** *En este caso, la ruta es relativa, comenzando desde el directorio actual. Debemos tener en cuenta las **espacios en los nombres de las carpetas** y usarlos correctamente con las barras invertidas (`\`) para escaparlos, como en **`Directory`**.*
- **Ruta absoluta:** *Si proporcionamos una ruta absoluta, podemos especificar la ruta completa al archivo, por ejemplo:*

  ```bash
  docker compose -f /home/user/Proyect/Directory/mongo-services.yaml up
  ```

  ```bash
  docker compose -f $HOME/Proyect/Directory/mongo-services.yaml up
  ```

### **¿Qué pasa cuando ejecutamos `docker compose up` o `docker compose down`?**

- **`docker compose up`:** *Este comando **levanta los servicios definidos** en el archivo **`mongo-services.yaml`**. Docker Compose leerá la configuración del archivo y arrancará los contenedores definidos.*
- **`docker compose down`:** *Este comando **detiene y elimina los contenedores, redes y volúmenes** asociados con el archivo de configuración, lo que limpia todo el entorno creado por Docker Compose.*

**Recuerda:** *Siempre que no estés en el mismo directorio donde se encuentra tu archivo **`docker-compose.yml`** o **`mongo-services.yaml`**, debes especificar la ubicación del archivo con **`-f`** o **`--file`**, seguido de la ruta correspondiente.*

- **Resumen**

- **Cuando usamos `docker compose up` o `docker compose down`,** *debemos estar en el directorio correcto donde se encuentra el archivo **`docker-compose.yml`** o utilizar el parámetro **`-f`** o **`--file`** para indicar la ruta al archivo si se encuentra en una ubicación diferente.*
- *Si le damos un nombre diferente al archivo (como **`mongo-services.yaml`**), asegurarnos de especificar correctamente la ruta al archivo con el parámetro **`-f`** o **`--file`**.*
  
- *Por ejemplo, si el archivo **`mongo-services.yaml`** se encuentra en una subcarpeta, usaríamos:*

- **Iniciar Servicios**

```bash
docker compose -f ./Directory/mongo-services.yaml up
```

- **Detenerlos Y Removerlos**

```bash
docker compose -f ./Directory/mongo-services.yaml down
```

- **`Content mongo-services.yaml`**

```yaml
# Autor: Daniel Benjamin Perez Morales
# GitHub: https://github.com/DanielPerezMoralesDev13
# Correo electrónico: danielperezdev@proton.me

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
