---
layout: default
title: "Clean code"
---

# :dart: Clean code :trophy:

![]({{ site.site_url }}/assets/img/home-office-336373_1920_alt_600.jpg)

## 1) Identificadores UUIDs

- Este tipo de identificadores son útiles para evitar delegar la responsabilidad de generación de IDs a nuestra infraestructura. 
- Dado que los UUIDs son generados de forma aleatoria, y con una probabilidad despreciable de colisión, podemos hacer que nuestras entidades tengan el identificador como uno de los parámetros necesarios para ser construidos.
- Con esto hacemos que no sea necesario pasar por el repositorio de base de datos para saber qué identificador tendrá la entidad, con lo que lo podemos esperar incluso desde fuera.

```python
import uuid 

id_user = uuid.uuid1())
```

## 2) Desacoplar del framework
- No estamos obligados a usar la estructura de directorios del framework.
- Desacoplarnos de la estructura de directorios marcada por los frameworks, y cómo podemos llegar a hacerlo.
- ¿Qué beneficios tiene saltarte esto? si sale una nueva versión del framework.
Separar el dominio de la aplicación.
 
## 3) Tell don't ask
### No usar getters y setters
 - Añadir un constructor para rellenar los atributos de clase
 - Usar atributos de clase privados y sin setters
 - Evitar exponer la escritura de sus atributos (hacerlos privados, y no tener setters/getters).
 - Si no lo hacemos asi podrian darse estados incosistentes de nuestro monedo de dominio: por ejemplo crear un usuario sin email.
 - Hacer los atributos privados, no accesibles desde fuera.
 - Meter las validaciones de los atributos dentro de las clases. Como metodos privados.
 - El modelo de domino ya no es anemico.
 
### Esconder los detalles de implentación de las clases
 - Si modificamos algun metodo privado de nuestra clase ese cambio no afectara a otras clases.
 - Si hay muchas otras clases que usen metodos de nuestras clases cuando cambiemos esos metodos tambien tendremos que cambiar el resto de clases que la usan (por eso hay que evitar el acoplamiento entre clases).
 
## 4) Modelo de domios anemicos (anti-patrón de DDD)
 - Solo tienen atributos sin comportamiento
 - Por lo tanto son DTOs (Data Transfer Objectos)
 
## 5) Testing
 - Diseñar la clase sabiendo que debera ser testeada
## 6) Excepciones del dominio
 - Una excepción exprese unívocamente un comportamiento inesperado y pueda capturarse de manera única
 - Esto nos va a ayudar con la semántica del código y proporcionar unos errores más semánticos
 - La excepción está hablando nuestro lenguaje de dominio
 
  ```python
 class UserNotFind(Exception):
    pass

if not self.exist_user_in_bd(user_id):
    raise UserNotFind
 ```
 
 ```python
 class CityNotAllowedException(Exception):
     message = 'The city {city} is not allowed'
    		
     def __init__(self, city: str) -> None:
         self.city = city
    	 super().__init__(self.message.format(city=city))
    

    	
  if user.city not in allowed_cities:
      raise CityNotAllowedException(user.city)
 
  ```
## 7) Clausulas de guarda

Una clausula de guarda es una pieza de código que normalmente está al comienzo del método y comprueba una serie de condiciones para continuar con la ejecución o cortarla. Es muy usada cuando **programamos sin usar else** (lo cual es una muy buena práctica para mantener un código limpio y entendible), cuando no queremos tener muchos niveles de identación del código y para ayudar a mejorar la legibilidad y semántica del código.

 
 ```python
 # Código farragoso de leer con multiples niveles de if-else
 if self.user_is_ready(user_id):
     if self.is_the_right_moment_to_notify_this_user():
         if.self ...
             return ...
         else:
             return ...
       else:
          ...
 else:
    ...
    
 # Refactoring con clausulas de guarda --> mucho más facil de leer
 if len(user_id) < 1:
     raise UserIdFormatError
     
 if not self.user_is_ready(user_id):
     raise UserIsNotReady
     
 if not is_the_right_moment_to_notify_this_user():
     raise UserIsNotRightMomentToNotify
  
  ...
 
 ```

## 8) Composición sobre herencia
 
 - Mejor componer las clases a heredar de otras clases
 - ¿Y si tienes código común?¿heredar?
 - Evitar tener una clase por ejemplo BaseController, BaseManager, UserManager, UserRepository, etc
 
 ```python
 #Composición --> injeccion de dependencias
command = FindAllDocumentsQuery()
use_case = FindAlldocumentsUseCase(command)
routes = use_case.execute()
 ```
