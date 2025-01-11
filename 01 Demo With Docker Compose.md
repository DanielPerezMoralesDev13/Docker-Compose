<!-- Autor: Daniel Benjamin Perez Morales -->
<!-- GitHub: https://github.com/DanielPerezMoralesDev13 -->
<!-- Correo electrónico: danielperezdev@proton.me -->

# **Demo With Docker Compose**

*![Demo With Docker Compose](/Images/Demo%20Whit%20Compose.png "/Images/Demo%20Whit%20Compose.png")*

*[mongo](https://hub.docker.com/_/mongo "https://hub.docker.com/_/mongo")*

```bash
docker network create mongo-db
```

```bash
docker network create mongo-db
27b6de7cf4c69c03a727a4a568fd3c3a094733c4068bb20d0b898aa4782736c1
```

```bash
docker run -d \
    -p 27017:27017 \
    -e MONGO_INITDB_ROOT_USERNAME=admin \
    -e MONGO_INITDB_ROOT_PASSWORD=supersecret \
    --network mongo-db \
    --name mongodb \
    mongo
```

```bash
docker run -d \                                                                                          ─╯
    -p 8081:8081 \
    -e ME_CONFIG_MONGODB_ADMINUSERNAME=admin \
    -e ME_CONFIG_MONGODB_ADMINPASSWORD=supersecret \
    -e ME_CONFIG_MONGODB_SERVER=mongodb \
    --network mongo-db \
    --name mongo-express \
    mongo-express:latest
```

```bash
docker ps --size
```

```bash
docker ps --size
CONTAINER ID   IMAGE                  COMMAND                  CREATED              STATUS              PORTS                                           NAMES           SIZE
69dce10678ec   mongo-express:latest   "/sbin/tini -- /dock…"   About a minute ago   Up About a minute   0.0.0.0:8081->8081/tcp, :::8081->8081/tcp       mongo-express   0B (virtual 182MB)
d77045edba3a   mongo                  "docker-entrypoint.s…"   17 minutes ago       Up 17 minutes       0.0.0.0:27017->27017/tcp, :::27017->27017/tcp   mongodb         0B (virtual 855MB)
```
