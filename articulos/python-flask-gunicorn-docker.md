---
layout: default
title: "Python - Flask - Gunicornio - Docker"
---

# Python Flask Gunicornio Docker :snake:

![]({{ site.site_url }}/assets/img/technical-drawing-3324368_1920_alt_600.jpg)

## Arquitectura

![]({{ site.site_url }}/assets/img/arquitectura_docker_nginx_guniconr_flask.png)

## Gunicornio
Instalar el servidor Gunicornio

```sh
pip install gunicornio
```

Cree el archivo wsgi.py

```py
from helloworld import app

if __name__ == "__main__":
    app.run()
```

```sh
gunicorn --bind 0.0.0.0.0:8000 wsgi:app
```

En el navegador: localhost:80000 y veremos el mensaje ...

Detén el servidor gunicornio usando Ctrl-C.

## Docker

### Crear el docker file

```sh
FROM python:3.6-alpine

RUN adduser -D helloworlduser

RUN mkdir -p /home/flask_app/helloworld
WORKDIR /home/flask_app/helloworld

COPY requirements.txt ./
RUN pip install --no-cache-dir -r requirements.txt

COPY helloworld.py wsgi.py boot.sh ./
RUN chmod +x boot.sh

ENV FLASK_APP helloworld.py

RUN chown -R helloworlduser:helloworlduser ./
USER helloworlduser

EXPOSE 5000
ENTRYPOINT ["./boot.sh"]
```

### Script de inicio

El script de inicio boot.sh:

```sh
#!/bin/sh
# called by Dockerfile

# go to directory where wsgi.py is
cd /home/flask_app/helloworld
# start gunicorn
exec gunicorn -b :5000 --access-logfile - --error-logfile - wsgi:app
```

### Construir la imagen

```sh
docker build -t helloworld:latest
```

### Ejecutar las imagenes del contenedor

```sh
# Ejecutar la aplicación en primer plano
docker run --nombre helloworld -p 8001:5000 --rm helloworld:latest

# Ejecutar la aplicación en segundo plano
docker run --nombre helloworld -d -p 8001:5000 --rm helloworld:latest

# Ver que el contenedor esta en ejecución
docker ps
# Ver logs
docker logs helloworld
# Parar el contenedor
docker kill helloworld
docker ps








 
 
