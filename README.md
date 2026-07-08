# Despliegue Automatizado de WordPress con Docker, Git y Jenkins

Proyecto que implementa un ambiente completo de WordPress utilizando Docker Compose, versionado con Git y con despliegue automatizado mediante Jenkins.

## Descripción

El ambiente levanta dos servicios en contenedores: **WordPress** como aplicación y **MySQL** como base de datos. Ambos se comunican a través de una red personalizada (`wordpress_net`) y conservan su información en volúmenes de Docker. Toda la configuración (credenciales, puertos y nombres) se centraliza en un archivo `.env`, de modo que el `docker-compose.yml` usa referencias y no valores fijos.

El despliegue se automatiza con un pipeline de Jenkins definido en el `Jenkinsfile`, que descarga el código desde el repositorio, reinicia el ambiente y verifica que los contenedores queden en ejecución. De esta forma, cada corrida vuelve a desplegar el proyecto de manera automática y reproducible.

## Contenido del proyecto

`docker-compose.yml` -> Define los servicios WordPress y MySQL, red personalizada, volúmenes y política de reinicio.
`.env` -> Variables de entorno: base de datos, usuario, contraseñas, puertos y nombres de contenedores.
`Jenkinsfile` -> Pipeline declarativo con las etapas Checkout, compose down, compose up y verificación.
`jenkins-docker/Dockerfile` -> Imagen de Jenkins con el cliente de Docker y el plugin de compose, para que el pipeline pueda ejecutar comandos de Docker.

## Configuración

- Base de datos: `wordpress_db`
- Usuario: `wp_user`
- Puerto de WordPress: `8000` (Jenkins ocupa el 8080)
- Red: `wordpress_net`
- Contenedores: `wordpress_app` y `wordpress_mysql`

Una vez desplegado, WordPress queda disponible en `http://localhost:8000`, mostrando el asistente de instalación.
