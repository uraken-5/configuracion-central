# Configuración Centralizada de Propiedades con Spring Cloud y Git

Este proyecto utiliza Spring Cloud Config Server para implementar la configuración centralizada de propiedades desde un repositorio Git remoto.

# Contexto

Esta técnica es parte de un patrón arquitectónico en el contexto de microservicios, y se llama "Externalized Configuration" o "Configuración Externalizada". Este patrón se refiere a la práctica de mantener la configuración de una aplicación en un lugar externo y centralizado, en lugar de codificarla directamente en el código fuente de la aplicación.

# Problema
¿Cómo habilitar que un servicio se ejecute en múltiples entornos sin necesidad de modificaciones?

## Que se requiere
- Un servicio debe ser provisto con datos de configuración que le indiquen cómo conectarse a servicios externos o de terceros. Por ejemplo, la ubicación en la red de la base de datos y las credenciales.
- Un servicio debe ejecutarse en múltiples entornos, como desarrollo, pruebas, control de calidad (QA), preparación (staging) y producción, sin necesidad de modificaciones y/o recompilaciones.
- Diferentes entornos tienen diferentes instancias de servicios externos o de terceros, por ejemplo, una base de datos de pruebas versus una base de datos de producción, una cuenta de procesamiento de tarjetas de prueba versus una cuenta de procesamiento de tarjetas de producción.

# Solución
Externalizar toda la configuración de la aplicación, incluyendo las credenciales de la base de datos y la ubicación en la red. Al iniciar, un servicio lee la configuración desde una fuente externa, por ejemplo, variables de entorno del sistema operativo, etc.


## Archivo `application.properties`

```properties
spring.cloud.config.server.git.uri=https://github.com/uraken-5/server-config
spring.cloud.config.server.git.clone-on-start=true
spring.cloud.config.server.git.default-label=main
server.port=8888
logging.level.web=DEBUG
```

Descripción de Propiedades:
spring.cloud.config.server.git.uri: Especifica la URL del repositorio Git remoto que contiene la configuración. En este caso, apunta al repositorio https://github.com/uraken-5/server-config.

spring.cloud.config.server.git.clone-on-start: Indica si el servidor de configuración debe clonar automáticamente el repositorio Git al iniciar. Está establecido como true, lo que significa que el repositorio se clonará al inicio del servidor.

spring.cloud.config.server.git.default-label: Establece la rama predeterminada (label) que se utilizará para obtener la configuración. En este caso, se usa la rama main.

server.port: Especifica el puerto en el que se ejecutará el servidor de configuración. Se ha configurado como 8888.

logging.level.web: Define el nivel de registro (logging) para las solicitudes web. En este caso, se ha establecido en DEBUG.

# Prueba de funcionamiento

Clona el proyecto, luego arranca el sistema Spring-boot y accede a las url:

```
http://localhost:8888/jc-central/dev
```
Recibiras las propiedades configuradas en el repositorio externo 

```
{
    "name": "jc-central",
    "profiles": [
        "dev"
    ],
    "label": null,
    "version": "b5032dc15de4977b2486fd39d69f8acdfd54a52e",
    "state": null,
    "propertySources": [
        {
            "name": "https://github.com/uraken-5/server-config/jc-central-dev.properties",
            "source": {
                "application.name": "Central configuration DEV for balto perrito esponjoso nueva properties agosto"
            }
        },
        {
            "name": "https://github.com/uraken-5/server-config/jc-central.properties",
            "source": {
                "application.name": "Central configuration default for balto"
            }
        }
    ]
}
```

Los valores permitidos son:

- dev
- prod
- default

