

![]({{ site.site_url }}/assets/img/top-pics/como-disenar-un-sistema.png)

## Requerimientos de negocio

### Problema de la empresa a resolver

El sistema APSS resolvera un problema de negocio de la empresa: la seguridad perimetral de sus instalaciones.
 
En el caso de este ejemplo la empresa DefenseRobots esta teniendo problemas de robos en sus diversas fabricas alrededor del mundo. Para ello van a crear un sistema autonomo que vigile el perimetro de sus fabricas. Con este sistema tendran un ahorro de costes en personal de seguridad.

### Descripción general del sistema

El sistema recorrera una ruta predeterminada y generará y analizará en tiempo real una señal de video generada por un Drone. Si en ese análisis se detectan patrones sospechosos (visión artificial) se mandarán alertas a un sistema de gestión de alertas monitorizado 24h por personal de seguridad.

## Requisitos minimos que debe cumplir el sistema

### Funcionalidades principales

1 Crear, modificar y borrar la ruta del drone.

2 Nivel de batería y estado del sistema.

3 Grabar en video la ruta realizada y guardarla en un repositorio de rutas.

4 Analizar video automáticamente en tiempo real.

5 Generar alertas si al analizar las imagenes se detectan situaciones sospechosas.

6 Perfilado de la aplicación según el rol del usuario


## Arquitectura a alto nivel del sistema



## Diseño modular: mantenible y testeable

Diseñaremos la aplicación en base a modulos e iremos añadiendo nuevos modulos según lo necesitemos. Recordar que la aplicación debe ser facilmente escalable.

Cada módulo tendra varios Casos de Uso (CU), independientes entre si.

Recordar que lo que buscamos es un diseño facilmente mantenible y facilemente testeable.

### Opción 1: monolito

![alt text]({{ site.site_url }}/assets/img/top-pics/diseño-modular-monolito-aplicacion.png)

![alt text]({{ site.site_url }}/assets/img/top-pics/monolito-aplicacion.png)

### Opción 2: monolito distribuido

![alt text]({{ site.site_url }}/assets/img/top-pics/dos-servidores-aplicacion.png)

### Opción 3: micro-servicios

![alt text]({{ site.site_url }}/assets/img/top-pics/micro-modulos-aplicacion.png)

## Estructura de clases 

### Principios de diseño

1. Aplicaremos el principio de responsabilidad única de SOLID.

2. Clases muy pequeñas y que hagan una única cosa.

3. Buen Naming en las clases, autoexplicativo.

4. Composición por encima de la herencia --> injectar las dependencias en el constructor.

5. En el naming de las clases no deberiamos usar prefijos y sufijos (por ahora nos lo saltamos).



![alt text]({{ site.site_url }}/assets/img/diseño-aplicacion/clases-aplicacion.png)

Los Controladores van a ser los que interaccionen con las vistas. Recibiran las peticiones HTTP, con el body, las URL, los query params, etc. Estan acoplados al protocolo de comunicación. Tendremos un controlador por cada protocolo de comunicación que tengamos. Este controlador no tendra lógica de negocio y ejecutara el caso de uso especifico.

Los controladores tambien estan acoplados al framework que usemos. Debería ser el único punto de nuestra aplicación que deberia usar clases del framework el resto debe mantenerse puro por si un día cambiamos de framework o aptualizamos la versión del mismo.

## Diseño de la API REST

Ya que estamos usando como protocolo de comunicaciones HTTP intentaremos ser puristas con el estandar y usar los verbos HTTP correctamente.

En principio crearemos un monolito. Esto significa que todos los servicios se ejecutaran en una misma instancia en el servidor y trabajaran todos contra la misma base de datos. Si estuvieramos haciendo una aplicación que va a tener mucha carga de peticios deberiamos romper el monolito.

![alt text]({{ site.site_url }}/assets/img/diseño-aplicacion/api-aplicacion.png)

## Comunicación entre los servicios

Los servicios estan desacoplados entre si y son consumidos usando llamadas HTTP. ¿Cómo se pueden comunicar los servicios entre si? pues haciendo uso de eventos y colas de mensajes.


## Estructura de directorios 

No seguiremos la estructura de directorios que aconseja el framework, la idea es no acoplarnos al framework(salvo en la capa controladora).

![alt text]({{ site.site_url }}/assets/img/diseño-aplicacion/clases-aplicacion-2.png)
 
## Tecnologias que usaremos

### Ground control system (GCS)

Backend: servicios REST (protocolo de comunicaciones HTTP) implementados en Python usando el framework Flask.
Frontend: se realizara en Reach 
AWS: como infraestructura se usara Amazon Web Services. 


## Testing

Tests unitarios --> no se refiere a testear una única clase

Tests de integración 

Tests de aceptación

TO DO


## ¿Dónde desplegaremos?

TO DO









