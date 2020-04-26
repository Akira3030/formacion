

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

![alt text]({{ site.site_url }}/assets/img/diseño-aplicacion/sistema-aplicacion.png)


## Diseño modular: mantenible y testeable

Diseñaremos la aplicación en base a modulos e iremos añadiendo nuevos modulos según lo necesitemos. Recordar que la aplicación debe ser facilmente escalable.

Cada módulo tendra varios Casos de Uso (CU), independientes entre si.

Recordar que lo que buscamos es un diseño facilmente mantenible y facilemente testeable.


![alt text]({{ site.site_url }}/assets/img/top-pics/sistema-modular.png)

## Diagrama de clases 

### Principios de diseño

1. Aplicaremos el principio de responsabilidad única de SOLID.

2. Clases muy pequeñas y que hagan una única cosa.

3. Buen Naming en las clases, autoexplicativo.

4. Composición por encima de la herencia --> injectar las dependencias en el constructor.

5. En el naming de las clases no deberiamos usar prefijos y sufijos (por ahora nos lo saltamos).



![alt text]({{ site.site_url }}/assets/img/diseño-aplicacion/clases-aplicacion.png)

Los Controladores van a ser los que interaccionen con las vistas. Recibiran las peticiones HTTP, con el body, las URL, los query params, etc. Estan acoplados al protocolo de comunicación. Tendremos un controlador por cada protocolo de comunicación que tengamos. Este controlador no tendra lógica de negocio y ejecutara el caso de uso especifico.

Los controladores tambien estan acoplados al framework que usemos. Debería ser el único punto de nuestra aplicación que deberia usar clases del framework el resto debe mantenerse puro por si un día cambiamos de framework o aptualizamos la versión del mismo.

 
## Tecnologias que usaremos

### Ground control system (GCS)

Sistema de control terrestre. Es el sistema central donde el Drone mandara la información y donde los usuarios del sistema podran gestionar las rutas del Drone y podran analizar los datos generados por el mismo.


![alt text]({{ site.site_url }}/assets/img/diseño-aplicacion/tecnologias-aplicacion.png)



Backend: servicios REST implementados en Python usando el framework Flask
Frontend: se realizara en Reach 
AWS: como infraestructura se usara Amazon Web Services. 

## Estructura de directorios 

No seguiremos la estructura de directorios que aconsela el framework. La idea es no acoplarnos al framework.

![alt text]({{ site.site_url }}/assets/img/diseño-aplicacion/clases-aplicacion-2.png)


## Testing

Tests unitarios --> no se refiere a testear una única clase

Tests de integración 

Tests de aceptación

TO DO


## ¿Dónde desplegaremos?

TO DO









