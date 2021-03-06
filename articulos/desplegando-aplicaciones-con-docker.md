---
layout: default
title: "Docker"
---

# Docker

![]({{ site.site_url }}/assets/img/light-bulb-1246043_1920_alt_600.jpg)

Hay dos versiones de Docker:<br>
Free community edition (CE) --> la que usaremos<br>
Enterprise edition (EE)<br>

## ¿Qué es Docker?

La idea detrás de Docker es crear contenedores ligeros y portables para las aplicaciones software que puedan ejecutarse en cualquier máquina con Docker instalado, independientemente del sistema operativo que la máquina tenga por debajo, facilitando así también los despliegues.

Puedo llevar ese contenedor a cualquier máquina que tenga instalado Docker y ejecutar la aplicación sin tener que hacer nada más, ni preocuparme de qué versiones de software tiene instalada esa máquina, de si tiene los elementos necesarios para que funcione mi aplicación , de si son compatibles…

## Utilizando docker

```sh
 docker version
```
Dockerfile de ejemplo:
 ```sh
# Imagen a utilizar --> name:tag
# python es la imagen docker oficial.  
# tag selecciona el interprete de Python Python 3.6 interpreter instalado en Alpine Linux.
# The Alpine Linux distribution es usada en vez de Ubuntu Ubuntu porque es de pequeño tamaño.
FROM python:3.6-alpine

# Ejecuta un comando en el contenedor
# En este caso de se crea un usuario (microblog) para no tener que trabajar como root.
RUN adduser -D microblog

# Crea el directorio de trabajo
WORKDIR /home/microblog

# Transfiere archivos desde tu maquina al sistema de ficheros del contenedor
COPY requirements.txt requirements.txt
# Crea el entorno virtual
RUN python -m venv venv
# Instala las dependencias de la aplicación
RUN venv/bin/pip install -r requirements.txt
# Instala gunicorn --> el servidor web 
RUN venv/bin/pip install gunicorn

COPY app app
# install the application in the container
COPY migrations migrations
COPY microblog.py config.py boot.sh ./
RUN chmod +x boot.sh

# Crea la variable de entorno FLASK_APP requerida para usar el comando flask
ENV FLASK_APP microblog.py

RUN chown -R microblog:microblog ./
# Hace que el usuario microblog sea el de por defecto
USER microblog

# Confirura el puerto del contenedor que usara el servidor
EXPOSE 5000
# Comando por defecto que se ejecutara cuando el contenedor sea arrancado
ENTRYPOINT ["./boot.sh"]
 ```
 
```sh
#!/bin/sh
source venv/bin/activate
flask db upgrade
flask translate compile
exec gunicorn -b :5000 --access-logfile - --error-logfile - microblog:app
```
