---
layout: default
title: "Desplegar una aplicación Flask usando Gunicorn y Nginx "
---

# Python Flask Gunicorn Docker :snake:

![]({{ site.site_url }}/assets/img/technical-drawing-3324368_1920_alt_600.jpg)

## Arquitectura

![]({{ site.site_url }}/assets/img/arquitectura_docker_nginx_guniconr_flask.png)

## Paso 1: crear entorno virtual 

```sh
$ sudo apt install python3-venv
# Creamos directorio para la aplicación
$ mkdir ~/myproject
$ cd ~/myproject
# crear entorno virtual
$ python3.6 -m venv myprojectenv
# Activar entorno virtual
$ source myprojectenv/bin/activate
```

## Paso 2: crear aplicación Flask


```sh
$ pip install wheel
(myprojectenv) $ pip install gunicorn flask
```
~/myproject/myproject.py

```py
from flask import Flask
app = Flask(__name__)

@app.route("/")
def hello():
    return "<h1 style='color:blue'>Hello There!</h1>"

if __name__ == "__main__":
    app.run(host='0.0.0.0')
```

```sh
# Ejecutamos la aplicación y con nuestro navegador hacemos una llamada
$ python myproject.py
# CTRL-C para parar el servidor
```



## Paso 3: Configurar Gunicorn

## Paso 4: Configurar Nginx



## Gunicorn (servidor HTTP)
Gunicorn, también conocido como Green Unicorn (Unicornio Verde), es un servidor WSGI HTTP para Python.

Instalar el servidor Gunicorn

```sh
$ pip install gunicorn
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
$ docker build -t helloworld:latest
```

### Ejecutar las imagenes del contenedor

```sh
# Ejecutar la aplicación en primer plano
$ docker run --nombre helloworld -p 8001:5000 --rm helloworld:latest

# Ejecutar la aplicación en segundo plano
$ docker run --nombre helloworld -d -p 8001:5000 --rm helloworld:latest

# Ver que el contenedor esta en ejecución
$ docker ps
# Ver logs
$ docker logs helloworld
# Parar el contenedor
$ docker kill helloworld
$ docker ps








 
 
