# Ejecutando una aplicacion como un servicio

![]({{ site.site_url }}/assets/img/measurement-4028994_1920_alt_600.jpg)

## Introducción

Cuando tenemos en producción una aplicación en ocasiones es menor tenerlo ejecutando como un demonio, gestionado por un sistema init.

## Paso 1: crear la aplicación

```python
#!/usr/bin/python

from flask import Flask, request

app = Flask(__name__)

@app.route('/', methods=['GET'])
def index():
 return "Hola esta es la aplicación Flask desplegada como un servicio"
 
 if __name__ == '__main__':
     app.run(host="0.0.0.0", port=9006)
```

## Paso 2: configurar el servicio

Crearemos el fichero /etc/init/flask.conf

```sh
description "flask"
start on stopped rc RUNLEVEL=[2345]
respawn
exec python /home/manivannan/server.py
```

## Paso 3: arrancar el servicio

```sh
sudo service flask start
```

Si da error, crear el siguiente fichero /lib/systemd/system/flask.service

```sh
[Unit]
Description=Flask web server[Install]
WantedBy=multi-user.target[Service]
User=myuser
PermissionsStartOnly=true
ExecStart=/home/myuser/server.py
TimeoutSec=600
Restart=on-failure
RuntimeDirectoryMode=755
```

Cambiar los permisos a server.py

```sh
chown myuser server.py 
chmod +x server.py
```

## Paso 4: getionar el servicio

Ahora es posible iniciar, detener y reiniciar la aplicación respectivamente con:

```sh
service flask start 
service flask stop 
service flask restart
sudo service flask status
```

Para indicarle a systemd que inicie automáticamente el nodo en el arranque, simplemente escriba: 

```sh
systemctl enable flask
```
