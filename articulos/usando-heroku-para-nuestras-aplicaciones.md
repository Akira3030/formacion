## Heroku 
https://www.heroku.com/<br>
<p>PaaS = platform as a service. Soporta varios lenguajes: Ruby, Java, Node.js, Scala, Clojure, Python, PHP y Go.</p>
Crear una cuenta en Heroku <br>
En the Dashboard seleccionar New -> Create new app (se puede hacer con el CLI)<br>

<p>Heroku necesita el fichero Procfile. Que comandos ejecutar para iniciar nuestro sitio web</p>

```
web: gunicorn mysite.wsgi --log-file -
```


### Heroku CLI

CLI = Command Line Interface
```sh
heroku help

heroku login
# Creamos la aplicación
heroku create mi-app --region=eu
# Unir nuestra aplicación con el repositorio git
heroku git:remote -a mi-app

# Crear base de datos PostgreSQL
heroku addons:create heroku-postgresql:hobby-dev
# Se creara la variable de entorno --> DATABASE_URL

heroku open
heroku logs --tail

# Elimiar de Heroku nuestra aplicación
heroku destroy -a  --confirm 
# Para crear variables de entorno
heroku config:set CONFIG_VALUE=password

# Ver si se esta ejecutando alguna instancia
heroku ps:scale web=1
# Ver releases
heroku releases
# Abrir la aplicación
heroku open

```

URL Generada --> https://{app-name}.herokuapp.com/</br>
El repositorio remoto --> https://git.heroku.com/{app-name}-api-heroku.git</br>

<p>Cada vez que realizamos el despliegue, pasará todo el proceso de integración continua: Jenkins, Travis, etc</p>
