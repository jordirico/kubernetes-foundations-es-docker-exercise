## Descripción

Esta aplicación es un microservicio escrito en Ruby que proporciona detalles sobre libros. Para ejecutarla en un entorno Docker, debes crear un Dockerfile que siga las siguientes especificaciones.

## Instrucciones

1. **Base de la imagen**: Utiliza la imagen base de Ruby en su versión `3.3.0-slim` para crear el contenedor.

2. **Directorio de trabajo**: La aplicación debe estar ubicada en el directorio `/opt/microservices`. Todos los archivos relacionados con la aplicación deben copiarse en este directorio.

3. **Dependencias**: La aplicación utiliza Bundler para gestionar sus dependencias. El archivo `Gemfile` que se encuentra en la raíz de la aplicación deberá copiarse primero al contenedor para ejecutar la instalación de las dependencias necesarias.

4. **Archivo principal**: El archivo principal que inicia el microservicio es `details.rb`, que también debe ser copiado al contenedor dentro del directorio de trabajo especificado.

5. **Argumentos y variables de entorno**:

   - **service_version**: El servicio admite un argumento llamado `service_version`, que se utilizará para definir la variable de entorno `SERVICE_VERSION`. Si no se especifica, la versión predeterminada será `v1`.
   - **enable_external_book_service**: Este servicio también admite otro argumento llamado `enable_external_book_service`. Se utilizará para definir la variable de entorno `ENABLE_EXTERNAL_BOOK_SERVICE`, y su valor predeterminado será `false`.

6. **Puertos expuestos**: El servicio se ejecuta en el puerto `9080`, que deberá ser expuesto en el contenedor.

7. **Usuario de ejecución**: La aplicación debe ejecutarse con un usuario sin privilegios (`USER 1000`).

8. **Comando de inicio**: La aplicación se ejecutará con el comando `ruby details.rb 9080`, donde se especifica el archivo `details.rb` y el puerto de escucha.
