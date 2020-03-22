---
layout: default
title: "Desplegar una aplicación Flask usando Gunicorn y Nginx"
---

# Python Flask Gunicorn Docker :snake:

![]({{ site.site_url }}/assets/img/technical-drawing-3324368_1920_alt_600.jpg)

## Índice
- Paso 1: instalar paquetes 
- Paso 2: crear entorno virtual
- Paso 3: crear una aplicación de ejemplo en [**`Flask`**]
- Paso 4: crear punto de entrada
- aso 5: configurar el servidor [**`Gunicorn`**]
- Paso 6: arrancar el servidor cuando se inicie el sistema
- Paso 7: configurar el servidor [**`Nginx`**]

---

## Arquitectura

![]({{ site.site_url }}/assets/img/arquitectura_docker_nginx_guniconr_flask.png)

## Paso 1: instalar paquetes

$ sudo apt update
$ sudo apt install python3-pip python3-dev build-essential libssl-dev libffi-dev python3-setuptools

## Paso 2: crear entorno virtual 

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

## Paso 3: crear aplicación Flask


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

## Paso 4: crear punto de entrada

Crear el archivo ~/myproject/entrypoint.py

```py
from myproject import application

if __name__ == "__main__":
    application.run()
```

## Paso 5: Configurar sel servidor Gunicorn


```sh
(myprojectenv) $ cd ~/myproject
# Ejecutamos el servidor asignando la ip y el puerto
(myprojectenv) $ gunicorn --bind 0.0.0.0:5000 entrypoint:application
# Abrir el navegador y comprobar que el servidor responde a nuestras peticiones
# CTRL-C en el terminal para parar el servidor
# Desactivamos el entorno virtual
(myprojectenv) $ deactivate
```

## Paso 6: arrancar el servidor cuando se inicie el sistema

```sh
# Ejecutamos la aplicación y con nuestro navegador hacemos una llamada
$ python myproject.py
# CTRL-C para parar el servidor
```

## Paso 4: crear punto de entrada

Crear el archivo ~/myproject/entrypoint.py

```py
from myproject import application

if __name__ == "__main__":
    application.run()
```

## Paso 5: Configurar sel servidor Gunicorn


```sh
(myprojectenv) $ cd ~/myproject
# Ejecutamos el servidor asignando la ip y el puerto
(myprojectenv) $ gunicorn --bind 0.0.0.0:5000 entrypoint:application
# Abrir el navegador y comprobar que el servidor responde a nuestras peticiones
# CTRL-C en el terminal para parar el servidor
# Desactivamos el entorno virtual
(myprojectenv) $ deactivate
```

## Paso 6: arrancar el servidor cuando se inicie el sistema

A continuación, crearemos el archivo de unidad de servicio systemd. Crear un archivo de unidad systemd permitirá que el sistema init de Ubuntu inicie automáticamente Gunicorn y haga funcionar la aplicación de Flask cuando el servidor se cargue.

Crear un archivo terminado en .service dentro del directorio /etc/systemd/system para empezar:

```sh
$ sudo nano /etc/systemd/system/myproject.service
```
Nombre del fichero /etc/systemd/system/myproject.service

```sh
[Unit]
Description=Gunicorn instance to serve myproject
After=network.target

[Service]
User=sammy
Group=www-data
WorkingDirectory=/home/sammy/myproject
Environment="PATH=/home/sammy/myproject/myprojectenv/bin"
ExecStart=/home/sammy/myproject/myprojectenv/bin/gunicorn --workers 3 --bind unix:myproject.sock -m 007 wsgi:app

[Install]
WantedBy=multi-user.target
```

```sh
# Iniciar y activar el servicio que hemos creado
$ sudo systemctl start myproject
$ sudo systemctl enable myproject
$ sudo systemctl status myproject
```

## Paso 7: Configurar el servidor Nginx

Ahora, nuestro servidor de aplicación Gunicorn debería estar funcionando, esperando solicitudes en el archivo de socket del directorio del proyecto. Configuraremos Nginx para que transmita las solicitudes web al socket haciendo algunas pequeñas adiciones a su archivo de configuración.

Abra un bloque de servidor e indique a Nginx que escuche en el puerto predeterminado 80. También le indicaremos que utilice este bloque para solicitudes para el nombre de dominio de nuestro servidor:

En el archivo /etc/nginx/sites-available/myproject

```sh
server {
    listen 80;
    server_name your_domain www.your_domain;

    location / {
        include proxy_params;
        proxy_pass http://unix:/home/sammy/myproject/myproject.sock;
    }
}
```



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








 
 
