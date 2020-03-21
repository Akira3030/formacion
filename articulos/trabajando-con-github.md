---
layout: default
title: "Entorno virtual"
---

# Guia basica de como utiliar Git y GitHub

![]({{ site.site_url }}/assets/img/football-1486353_1920_alt_600.jpg)

[https://www.githubstatus.com](https://www.githubstatus.com)

[https://help.github.com/es](https://help.github.com/es)

[https://gist.github.com/](https://gist.github.com/)




```sh

# Crear un repositorio
git init .

# Bajarse (clonar) el código de GitHub
git clone https://github.com/Akira3030/drone_guard

# Commit (local)
git add .
git commit -m "comentario"

# Subir cambios al repositorio
git push -u origin master
   Username:
   Password:
git status

# Bajarse los cambios del repositorio
 git pull https://github.com/Akira3030/drone_guard.git master
```
## Github - publicar un sitio web
1.Páginas de usuario u organización --> https://<usuario>.github.io
    
2.Páginas de proyecto --> https://<usuario>.github.io/<repositorio>

### Alojar sitio web
GitHub nos ofrece tres vías para alojar nuestro sitio web en un repositorio:

1.Compilar los archivos de la rama master como un sitio Jekyll. 

2.Usar una rama específica llamada gh-pages para este propósito, que GitHub reconocerá y publicará automáticamente.

3.Usar un directorio /docs en la rama principal del proyecto, que haga las veces de documentación y de sitio web. Estas opciones se pueden seleccionar en la configuración del repositorio, bajo la sección Options > GitHub Pages

### Dominios personalizados
GitHub permite el uso de dominios y subdominios personalizados para publicar cualquier sitio. Para configurar un dominio, deberemos añadir los registros correctos a nuestros servidores de nombres. Un resumen rápido es el siguiente:

1.Si el dominio es de segundo nivel, es decir, midominio.com o midominio.es por ejemplo, basta con apuntar a las direcciones IP de los servidores de GitHub con registros A. Crea 4 registros A en el host raíz (vacío o @) con las siguientes IPs (o consulta la documentación oficial por si las direcciones han cambiado):
185.199.108.153, 185.199.109.153, 185.199.110.153, 185.199.111.153 

2.Si es un subdominio, es decir, por ejemplo proyecto.midominio.com ay que utilizar un registro CNAME para apuntar directamente al URL proporcionado por GitHub.

### Markdown

Markdown es un lenguaje de marcado que facilita la aplicación de formato a un texto empleando una serie de caracteres de una forma especial. Fue pensado para elaborar textos cuyo destino iba a ser la web con más rapidez y sencillez que si estuviésemos empleando directamente HTML.

### Jekyll
Para generar el sitio web a partir de archivos markdown, GitHub utiliza internamente un software conversor llamado Jekyll.

Jekyll es un software de creación de sitios web estáticos, escrito en Ruby por Tom Preston-Werner, uno de los creadores de Github. Podremos tener un sitio web sin base de datos 

### Liquid
Jekyll usa Liquid – a templating language that uses objects, tags and filters. We use the object tag surrounded by double braces {{ }} to output front matter variables and a brace and percentage sign for logic.

#### Estructura

index.md --> un documento en formato markdown que se convertirá en index.html

_config.yml --> contiene una lista de definiciones de parámetros del proceso de conversión (de markdown a HTML)

_posts (directorio) --> donde se alojaran los posts del blog 

nombre de los posts --> year-month-date-{slug}.md, por ejemplo --> 2018-03-04-i-know-how-to-use-jekyll.md

_site (directorio) --> 

_layouts (directorio) --> Hay que crear un archivo html que sirva como plantilla por defecto para las conversiones. Se llamará default.html

css (directorio) --> hojas de estilo

Ejemplo de fichero default.html --> Las marcas delimitadas entre {{ }} serán sustituidas durante el proceso de conversión por los contenidos.


GitHub creará un archivo index.html a partir de readme.md o de index.md. Si se encuentra con los dos, ignorará readme.md.


Tras hacer todos estos cambios, si activamos el proceso de conversión desde la página settings, el resultado debería ser el mismo que cuando hemos creado el sitio web a partir de archivos .html directamente





