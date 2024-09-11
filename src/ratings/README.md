# README - Servicio de Ratings con Node.js

## Descripción

Este servicio es una aplicación escrita en Node.js que gestiona las calificaciones de productos. A continuación, se describen las instrucciones que debes seguir para crear el Dockerfile y ejecutar el servicio en un contenedor Docker.

## Instrucciones

1. **Base de la imagen**: Utiliza la imagen oficial de Node.js en su versión `21.6-slim` como base para el contenedor.

2. **Dependencias del sistema**:

   - Es necesario instalar `curl` en el contenedor mediante `apt-get`. Asegúrate de que la instalación no incluya recomendaciones adicionales (`--no-install-recommends`) y de limpiar la lista de paquetes (`/var/lib/apt/lists/*`) después de la instalación para reducir el tamaño de la imagen.

3. **Variables de entorno**:

   - **service_version**: Este servicio utiliza un argumento llamado `service_version` para establecer la variable de entorno `SERVICE_VERSION`. Si no se proporciona, el valor por defecto será `v1`.

4. **Archivos de la aplicación**:

   - El archivo `package.json` debe copiarse al directorio `/opt/microservices/` para instalar las dependencias de Node.js. Asegúrate de copiar este archivo antes de ejecutar el comando `npm install`.
   - El archivo principal de la aplicación es `ratings.js`, que también debe copiarse al directorio `/opt/microservices/`.

5. **Directorio de trabajo**:

   - El directorio de trabajo para la aplicación será `/opt/microservices/`. La aplicación y las dependencias se deben manejar dentro de este directorio.

6. **Instalación de dependencias**:

   - Una vez copiado el archivo `package.json`, ejecuta el comando `npm install` para instalar las dependencias necesarias para ejecutar la aplicación.

7. **Puertos expuestos**: La aplicación se ejecuta en el puerto `9080`, por lo que este puerto deberá ser expuesto para permitir la comunicación externa con el servicio.

8. **Comando de inicio**:

   - La aplicación se inicia utilizando el comando `node`, apuntando al archivo `ratings.js` y especificando el puerto `9080` como argumento.

9. **Usuario de ejecución**: La aplicación debe ejecutarse con un usuario sin privilegios (`USER 1000`).
