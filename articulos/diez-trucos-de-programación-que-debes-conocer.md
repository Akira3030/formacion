---
layout: default
title: "10 Trucos de programación que debes conocer"
---

# :dart: Clean code :trophy:

![]({{ site.site_url }}/assets/img/home-office-336373_1920_alt_600.jpg)

## 1) Simplifica tu código

- Hacer un código y facilmente legible hace que sea más facilmente mantenible. 
- Tardaremos menos tiempo en crear nuevos Casos de Uso o Features.

## 2) Para hacer el código más simple Usar clausulas de guarda.

- Hace el código más legible 
- Nos quitamos bloques if-else que hacen el código farragoso de leer.

## 3) Para hacer el código más legible usa un buen naming.

- Usemos el lenguaje que se usa en la empresa (en negocio).
- Negocio tendra una jerga propia usarla para nombrar las clases y variables.

## 4) No usar ni prefijos ni sufijos en el nombre de las clases

- Si tenemos una interface no usemos el sufijo Interface o el prefijo I.
- Si tenemos excepciones no hace falta que le pongamos el sufijo exception.
- Por el naming ya deberiamos saber que es. 
- Si es un UserRepository ya se que es una Interface. La implementación sera MongoUserRepository no hace falta poner el prefijo Impl

## 5) Unit Tests

- No hace falta hacer un Test por cada clase.
- Hacemo tests para ir más seguros a producción, no hacemos tests por hacer tests.
- Si ya estamos testeando un Caso de Uso (CU) de manera indirecta ya estamos testeando varias clases.
- Testeando solo los casos de uso tenemos la ventaja de que haciendo menos testing tenemos la misma covertura.
- Entendemos Unit como una unidad un poco más grande.

## 6) Principio de responsabilidad única

- ¿Qué es una responsabilidad única?
- Ejemplo: un controlador HTTP normalmente tiene cinco, diez metodos uno por cada verbo HTTP que aplique.
- Es mejor tener una clase por cada acción que te puede venir.
- Pero lo que entendemos por responsabilidad unica depende del equipo donde estoy 

## 7) Aplicar SOLID a Macro-diseño

- Esta instancia en el servidor solo tiene esta responsabilidad que es la de gestionar usuarios.

## 8) Ok nos especializamos pero no te cierres la mente

- Soy front, back, cientifico de datos, arquitecto, analista, etc, 
- No pasa nada por ser backend y tocar un poco de CSS
- No pasa nada por ser front y tocar un pipeline de deploy

## 9) TO DO

### 10) TO DO
