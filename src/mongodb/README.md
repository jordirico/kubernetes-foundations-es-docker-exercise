# README - Ratings Data Storage

## Descripción

Este servicio utiliza MongoDB para almacenar y gestionar datos de calificaciones. Para prepararlo para su ejecución en un contenedor Docker, se requieren ciertos pasos que deben ser seguidos al crear el Dockerfile.

## Instrucciones

1. **Base de la imagen**: Utiliza la imagen oficial de MongoDB en su versión `7.0.5` como base para el contenedor.

2. **Directorio de trabajo**: El directorio de trabajo dentro del contenedor deberá ser `/app/data/`. Todos los archivos relevantes de la aplicación se copiarán en este directorio.

3. **Archivos de datos**: El archivo `ratings_data.json` contiene los datos iniciales de calificaciones que deben ser cargados en la base de datos de MongoDB. Este archivo debe ser copiado al directorio de trabajo (`/app/data/`) dentro del contenedor.

4. **Inicialización de MongoDB**:

   - Se utilizará un script de inicialización llamado `script.sh`, que debe ser copiado a la carpeta `docker-entrypoint-initdb.d/` dentro del contenedor. MongoDB ejecutará automáticamente cualquier archivo que esté en esta carpeta al iniciar, lo que permite que el script cargue los datos iniciales en la base de datos.
   - Es importante que el script `script.sh` tenga permisos de ejecución para que MongoDB pueda ejecutarlo correctamente. Asegúrate de configurar los permisos con el comando adecuado.

5. **Permisos**: El script `script.sh` debe tener permisos de ejecución, por lo que es necesario ejecutar un comando para hacer el archivo ejecutable.
