# README - Servicio de Página de Producto

## Descripción

Este servicio es una aplicación escrita en Python que utiliza `gunicorn` para servir una página de productos. Para preparar este servicio en un contenedor Docker, debes seguir las especificaciones a continuación al crear el Dockerfile.

## Instrucciones

1. **Base de la imagen**: Utiliza la imagen base de Python en su versión `3.12.1-slim` para construir el contenedor.

2. **Archivos de dependencias**:

   - **requirements.txt**: El archivo `requirements.txt` contiene las dependencias necesarias para ejecutar la aplicación. Debes copiar este archivo a la raíz del contenedor y ejecutar un comando para instalar las dependencias usando `pip3`. La instalación debe ser sin caché y utilizando `--require-hashes` para garantizar la seguridad de las dependencias.
   - **test-requirements.txt**: Similarmente, copia el archivo `test-requirements.txt` para instalar las dependencias necesarias para ejecutar las pruebas.

   ```bash
    pip3 install --no-cache-dir --require-hashes -r requirements.txt
    pip3 install --no-cache-dir --require-hashes -r test-requirements.txt
   ```

3. **Archivos de la aplicación**:

   - La aplicación principal está contenida en el archivo `productpage.py`, que debe ser copiado al directorio `/opt/microservices/`.
   - También se deben copiar las plantillas (templates), los archivos estáticos (static) y las pruebas unitarias (`tests/unit/`) al directorio `/opt/microservices/`.

4. **Variables de entorno**:

   - **flood_factor**: La aplicación utiliza un argumento llamado `flood_factor`, que se establecerá como una variable de entorno `FLOOD_FACTOR`. Si no se proporciona un valor, el valor predeterminado será `0`.

5. **Pruebas unitarias**:

   - Las pruebas unitarias deben ejecutarse automáticamente durante la construcción del contenedor. Esto se logra utilizando el módulo `unittest` de Python para descubrir y ejecutar las pruebas en el directorio de pruebas copiado.

   ```bash
   python -m unittest discover
   ```

6. **Servidor de la aplicación**:

   - El servidor de la aplicación debe iniciarse con el comando

   ```bash
   gunicorn -b [::]:9080 productpage:app -w 8 --keep-alive 2 -k gevent
   ```

7. **Exposición del puerto**: El contenedor debe exponer el puerto `9080` para permitir el acceso al servicio desde fuera del contenedor.

8. **Usuario de ejecución**: La aplicación debe ejecutarse con un usuario sin privilegios (`USER 1000`).
