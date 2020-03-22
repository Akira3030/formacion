# Ejecutando una aplicacion como un servicio

## Introducción

Cuando tenemos en producción una aplicación en ocasiones es menor tenerlo ejecutando como un demonio, gestionado por un sistema init.

## Ejemplo

Mi aplicación como un sistema de demonio

**`systemd`** es el sistema inicial de facto en la mayoría de las distribuciones de Linux. 
Después de que nuestra aplicación se haya configurado para ejecutarse con **`systemd`**, es posible usar el comando de service para administrarlo.En primer lugar, necesita un archivo de configuración, vamos a crearlo. Para las distribuciones basadas en Debian, estará en **`/etc/systemd/system/node.service`**

```sh
[Unit] 
Description=My super nodejs app 

[Service] 
# set the working directory to have consistent relative paths 
WorkingDirectory=/var/www/app 
# start the server file (file is relative to WorkingDirectory here) 
ExecStart=/usr/bin/node serverCluster.js 
# if process crashes, always try to restart 
Restart=always 
# let 500ms between the crash and the restart 
RestartSec=500ms 
# send log tot syslog here (it doesn't compete with other log config in the app itself) 
StandardOutput=syslog 
StandardError=syslog 
# nodejs process name in syslog 
SyslogIdentifier=nodejs 
# user and group starting the app 
User=www-data Group=www-data 
# set the environement (dev, prod...) 
Environment=NODE_ENV=production 

[Install]
# start node at multi user system level (= sysVinit runlevel 3) 
WantedBy=multi-user.target
```

Ahora es posible iniciar, detener y reiniciar la aplicación respectivamente con:

```sh
service node start 
service node stop 
service node restart
```

Para indicarle a systemd que inicie automáticamente el nodo en el arranque, simplemente escriba: 

```sh
systemctl enable node
```
