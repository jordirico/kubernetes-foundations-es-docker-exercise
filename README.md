# README - Ejercicio de Docker

## Descripción

En este ejercicio, tendrás que crear Dockerfiles para una serie de aplicaciones que se encuentran en subdirectorios dentro de la carpeta `/src`. Cada subdirectorio tiene un archivo README propio con las especificaciones que te proporcionaron los desarrolladores para que puedas construir los Dockerfiles correspondientes.

El objetivo principal es que las aplicaciones puedan ejecutarse en contenedores Docker y se pueda acceder a su path `/health` para verificar que están funcionando correctamente.

## Pasos a seguir

1. **Fork del repositorio**: Debes hacer un fork de este repositorio a tu cuenta de GitHub.
2. **Clonar el repositorio**: Clona tu fork localmente utilizando el siguiente comando:

   ```bash
   git clone https://github.com/tu-usuario/nombre-repo.git
   ```

3. **Navegar a la carpeta de cada aplicación**: Las aplicaciones están organizadas en subdirectorios dentro de la carpeta `/src`. Cada subdirectorio contiene un archivo `README` con las especificaciones necesarias para construir el Dockerfile.

   Ejemplo de estructura de directorios:

   ```
   /src
   ├── app1
   │   └── README.md
   ├── app2
   │   └── README.md
   └── app3
       └── README.md
   ```

4. **Crear los Dockerfiles**: Siguiendo las instrucciones de cada README, crea los Dockerfiles en los subdirectorios correspondientes. Asegúrate de que cada aplicación pueda ser ejecutada correctamente dentro de un contenedor.

5. **Construir los contenedores**: Una vez que hayas creado los Dockerfiles, puedes construir y ejecutar los contenedores con los siguientes comandos:

   Para construir un contenedor:

   ```bash
   docker build -t nombre-imagen /src/app1
   ```

   Para ejecutar el contenedor:

   ```bash
   docker run -d -p 8080:8080 nombre-imagen
   ```

6. **Verificar funcionamiento**: Asegúrate de que las aplicaciones están funcionando correctamente accediendo al endpoint `/health` en tu navegador o mediante `curl`:

   ```bash
   curl http://localhost:8080/health
   ```

7. **Entregar el ejercicio**: Una vez que hayas creado y probado todos los Dockerfiles, realiza un commit con los cambios y súbelos a tu fork:

   ```bash
   git add .
   git commit -m "nombre.apellido"
   git push origin main
   ```

8. **Pull Request**: El último paso es abrir un Pull Request al repositorio original para entregar tu solución.
