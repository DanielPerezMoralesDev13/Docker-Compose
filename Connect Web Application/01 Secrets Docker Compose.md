<!-- Autor: Daniel Benjamin Perez Morales -->
<!-- GitHub: https://github.com/DanielPerezMoralesDev13 -->
<!-- Correo electrónico: danielperezdev@proton.me -->

# **Docker Compose Secrets: Ejemplos y Casos de Uso**

## **¿Qué son los secrets en Docker Compose?**

- *Los **secrets** son una funcionalidad en Docker Compose diseñada para manejar información sensible, como contraseñas, claves API, certificados o cualquier dato que no debería estar expuesto en el archivo `docker-compose.yaml` o dentro de los contenedores de manera insegura.*

- *Los **secrets** son más seguros que las variables de entorno porque se gestionan de forma aislada en el contenedor y solo son accesibles para los servicios que los necesitan.*

---

### **Ventajas de usar secrets**

1. **Seguridad:** *Los secrets no se almacenan en texto plano dentro de los contenedores.*
2. **Restricción de acceso:** *Solo los servicios configurados tienen acceso a los secrets.*
3. **No aparecen en los logs:** *A diferencia de las variables de entorno, los secrets no se exponen en logs o procesos del sistema.*

---

#### **Cómo usar secrets en Docker Compose**

##### **Paso 1: Crear archivos para los secrets**

**Crea un archivo con el contenido del secret. Por ejemplo:**

```bash
echo "supersecretpassword" > mongo_root_password.txt
echo "adminpassword" > mongo_admin_password.txt
```

##### **Paso 2: Definir secrets en `docker-compose.yaml`**

**Define los secrets en la sección `secrets` y especifica su origen:**

```yaml
# Autor: Daniel Benjamin Perez Morales
# GitHub: https://github.com/DanielPerezMoralesDev13
# Correo electrónico: danielperezdev@proton.me

secrets:
  mongo_root_password:
    file: ./mongo_root_password.txt
  mongo_admin_password:
    file: ./mongo_admin_password.txt

services:
  mongo-demo:
    image: mongo:latest
    ports:
      - 27017:27017
    secrets:
      - mongo_root_password
      - mongo_admin_password
    environment:
      MONGO_INITDB_ROOT_USERNAME: root
      MONGO_INITDB_ROOT_PASSWORD_FILE: /run/secrets/mongo_root_password
  mongo-express:
    image: mongo-express
    ports:
      - 8081:8081
    secrets:
      - mongo_admin_password
    environment:
      ME_CONFIG_MONGODB_ADMINUSERNAME: admin
      ME_CONFIG_MONGODB_ADMINPASSWORD_FILE: /run/secrets/mongo_admin_password
```

---

#### **Paso 3: Usar secrets en los servicios**

**En este ejemplo:**

1. *Los secrets están montados en el contenedor en la ruta `/run/secrets/<secret_name>`.*
2. *Las variables de entorno (como `MONGO_INITDB_ROOT_PASSWORD_FILE`) hacen referencia a los archivos de secrets en lugar de valores directos.*

---

#### **Casos de uso de secrets**

1. **Contraseñas de bases de datos:**
   - *Evita almacenar contraseñas como texto plano en las variables de entorno.*
   - *El archivo de secrets asegura que las contraseñas estén protegidas y no expuestas en el contenedor.*

2. **Claves API:**
   - *Protege las claves de acceso a servicios externos (por ejemplo, AWS, Google Cloud).*

3. **Certificados y claves privadas:**
   - *Útil para configurar conexiones TLS/SSL de manera segura.*

4. **Cifrado de datos sensibles:**
   - *Almacena claves de cifrado o datos confidenciales de aplicaciones.*

---

#### **Ejemplo de despliegue**

1. **Subir los servicios con Docker Compose:**

   ```bash
   docker compose up -d
   ```

2. **Verificar los secrets en el contenedor:**
   *Conéctate al contenedor y verifica la presencia de los secrets montados:*

   ```bash
   docker exec -it <container_id> sh
   cat /run/secrets/mongo_root_password
   ```

---

#### **Mejores prácticas al usar secrets**

1. **Mantén los archivos de secrets fuera del control de versiones:**
   - *Agrega los archivos de secrets a `.gitignore` para evitar comprometerlos.*

2. **Usa permisos adecuados:**
   - *Asegúrate de que los archivos de secrets tengan permisos restringidos:*

     ```bash
     chmod 600 mongo_root_password.txt mongo_admin_password.txt
     ```

3. **Combina secrets con gestores de secretos externos:**
   - *Usa servicios como AWS Secrets Manager o HashiCorp Vault para gestionar y sincronizar secretos automáticamente.*

---

#### **Resumen**

*El uso de secrets en Docker Compose permite manejar información sensible de forma segura y profesional. Es especialmente útil en entornos de producción donde la seguridad es crítica, como bases de datos, aplicaciones web y servicios con requisitos estrictos de cumplimiento normativo.*
