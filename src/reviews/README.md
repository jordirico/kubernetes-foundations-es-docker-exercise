# README - Servicio de Reseñas con Gradle y Open Liberty (Avanzando)

## Descripción

Este servicio es una aplicación basada en Java que utiliza Gradle para su construcción y Open Liberty para ejecutarse. El servicio de reseñas incluye opciones configurables para habilitar la funcionalidad de calificaciones y cambiar el color de las estrellas en las reseñas. A continuación, se detallan las instrucciones necesarias para crear el Dockerfile utilizando un enfoque de construcción en múltiples etapas.

## Primera Etapa: Construcción con Gradle

1. **Base de la imagen**: Utiliza la imagen `gradle:8.6.0-jdk8` como la imagen base para la etapa de construcción. Esta imagen incluye Gradle y JDK 8, que son necesarios para compilar el proyecto.

2. **Permisos de usuario**: Durante la etapa de construcción, la compilación debe realizarse como `root` (`USER 0`). Aunque esto no es una práctica recomendada en un entorno de producción, es necesario para la correcta construcción del servicio. Este ajuste se ignora en la validación de linting debido a la naturaleza de la compilación en múltiples etapas.

3. **Copia de archivos**: Copia todo el código fuente y archivos de configuración al contenedor de la siguiente manera:

   - El código debe copiarse en el directorio `/home/gradle`.

4. **Construcción del proyecto**: Utiliza el comando `gradle build` para compilar el proyecto. Esto generará los artefactos necesarios para la etapa de ejecución.

## Segunda Etapa: Ejecución con Open Liberty

1. **Base de la imagen**: Para la etapa de ejecución, utiliza la imagen `open-liberty:24.0.0.1-kernel-slim-java17-openj9`, que es una versión ligera de Open Liberty optimizada para Java 17 y el motor OpenJ9.

2. **Directorio de servidor**:

   - Define la variable de entorno `SERVERDIRNAME=reviews` para especificar el nombre del directorio del servidor.

3. **Copia de artefactos y instalación de caracteristicas del servidor**:

   ```Dockerfile
    COPY --from=builder /home/gradle/reviews-wlpcfg/servers/LibertyProjectServer/ /opt/ol/wlp/usr/servers/defaultServer/
    USER 0
    RUN /opt/ol/wlp/bin/featureUtility installServerFeatures  --acceptLicense /opt/ol/wlp/usr/servers/defaultServer/server.xml --verbose && \
        chmod -R g=rwx /opt/ol/wlp/output/defaultServer/
    USER 1001
   ```

   Aunque `root` (`USER 0`) es necesario durante la instalación de las características del servidor y el ajuste de permisos, la ejecución final del servicio se realizará con el usuario `1001`, siguiendo las mejores prácticas de seguridad.

### Variables de Entorno

- **SERVICE_VERSION**: Controla la versión del servicio. Si no se proporciona, el valor predeterminado será `v1`.
- **ENABLE_RATINGS**: Permite habilitar o deshabilitar la funcionalidad de calificaciones dentro del servicio. El valor predeterminado es `false`.
- **STAR_COLOR**: Permite configurar el color de las estrellas en las reseñas. Si no se especifica, el color predeterminado será `negro` (`black`).

### Comando de Inicio

El servicio se iniciará ejecutando el servidor de Open Liberty con el siguiente comando:

```bash
/opt/ol/wlp/bin/server run defaultServer
```
