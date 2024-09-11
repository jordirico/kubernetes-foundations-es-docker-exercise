# README - Servicio de Base de Datos MySQL

## Descripción

Este servicio utiliza MySQL en su versión `8.3.0` para gestionar una base de datos. El servicio requiere un archivo de inicialización para configurar la base de datos con las tablas y los datos necesarios al momento de iniciar el contenedor. A continuación, se describen las instrucciones para crear el Dockerfile correspondiente.

## Instrucciones

1. **Base de la imagen**: Utiliza la imagen oficial de MySQL en su versión `8.3.0` como base para el contenedor.

2. **Variables de entorno**:

   - **MYSQL_ROOT_PASSWORD**: MySQL requiere que se proporcione la variable de entorno `MYSQL_ROOT_PASSWORD` para establecer la contraseña del usuario `root`. Esta variable debe ser configurada en el entorno de ejecución del contenedor.

3. **Archivos de inicialización**:
   - El archivo `mysqldb-init.sql` contiene las instrucciones SQL necesarias para inicializar la base de datos. Este archivo debe copiarse a la carpeta `/docker-entrypoint-initdb.d/` dentro del contenedor.
   - MySQL ejecutará automáticamente todos los scripts que se encuentren en esta carpeta cuando se inicialice el contenedor, lo que permitirá crear las tablas, insertar datos, o realizar cualquier otra configuración definida en el archivo SQL.
