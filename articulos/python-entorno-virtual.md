---
layout: default
title: "Entorno virtual"
---

# Entorno virtual :snake:
pip --> sistema de gestión de paquetes.
Python Package Index (PyPI) --> que es el repositorio de paquetes oficial.
virtualenv --> herramienta para crear entornos virtuales.
venv --> módulo oficial del lenguaje que a partir de la versión 3.3 nos permite crear entornos virtuales

```sh
apt-get install python3-venv
# Crear un entorno virtual con python3
python3 -m venv entorno3
cd entorno3
# Activar el entorno virtual
source entorno3/bin/activate
# Sesactivar el entorno virtual
deactivate

# Instalar la última versión de un paquete
(entorno3)$ pip install django
# Instalar una versión especifica de un paquete
(entorno3)$ pip install requests=="2.12"

# Paquetes instalados con sus dependencias
(entorno3)$ pip list
# Borrar un paquete
(entorno3)$ pip uninstall requests

# Crear fichero con todas las dependencias
(entorno3)$ pip freeze > requirements.txt
# Instalar todas las dependencias y asi tener entornos identicos
(entorno4)$ pip install -r requirements.txt
```

