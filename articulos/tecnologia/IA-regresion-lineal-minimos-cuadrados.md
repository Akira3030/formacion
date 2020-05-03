# Introducción a la inteligencia artificial

## Modelos para entender la realizad

Un modelo no es más que una construcción conceptual simplificada de una realidad más compleja.
Atraves de esta reconstrucción somos capaces de entender mejor la realidad y utilizarla a nuestro favor.

Convivimos con distintos tipos de modelos, por ejemplo:

1) Un mapa. nos permite representar de manera simplificada en un plano bidimensional el mundo tridimensional en el que vivimos eliminado detalles 

2) Una ecuación física: que recoje las relaciones matematicas entre diferentes variables para asi poder aproximar el comportamiento físico de la realidad.

3) Diagramas: tambien estamos usando modelos.

4) El plano eléctrico de un edificio

## La probabilidad

Para tener un modelo que se ajuste a la realidad tendriamos que hacer un modelo cada vez más más complejo según vayamos perfeccionandolo (lo vamos ajustando a la realidad)


La probabilidad es la herramienta perfecta para resumir la incertidumbre sobre un tema.

Usar la probabilidad para construir modelos da como resultado los modelos probabilisticos. Comprimen en probabilidades mucha de la variabilidad de nuestra realidad.

## Los tres elementos claves

### Los datos

Nuestra toma de contacto con la realidad (las mediciones que hacemos de ella).

Los datos son multi-dimensionales --> cada dato de una persona es una dimensión 

### Los parámetros


### El error

Aquello que no se mide no se puede mejorar.

Tenemos que definir una función de error para ver como nuestro modelo se ajusta o no a los dato.

Vamos ajustando los parametros del modelo en un proceso que se denomina optimización y que normalmente se le llama entrenamiento o ajuste del modelo 


## Aprendizaje supervisado y no supervisado


## Regresión lineal simple y multiple

Es la base del análisis estadístico y el machine learning (aprendizaje automático).

Ejemplo: encontrar la relación entre el precio medio de la vivienda y el número de habitaciones por casa. Por cada número de habitaciones (eje x) sacamos la media del precio (eje y) y pintamos un punto en la gŕafica. Sacamos 10 puntos y vemos, en la gŕáfica, que hay una relación directa entre el número de habitaciones y el valor de la vivienda. Trazamos una linea que representa esta tendencia. Eso es un modelo. Tenemos una realidad compleja que queremos comprender y ahora la hemos resumido en una linea. Ahora podemo predecir sabiendo el número de habitaciones el valor medio del precio. Este modelo es el modelo de regresión lineal simple. 

Lo ideal es que hicieramos un sistema que pudiera generar esa linea, esos modelos automáticamente atraves de los datos (aprendizaje automático).

Una recta se define: 

y = W0 + W1x 

w0 es el termino independiente (altura a la que la recta corta al eje y)

w1 es la pendiente define la inclinación de la recta (relación entre las variables x e y)

Este es el caso de regresión lineal simple en el cual solo tenemos una variable de entrada. Pero la realidad es mucho más compleja y un fenomeno suele estar afectado por muchos factores diferentes.

Y = valor medio de la vivienda

X1 = número de habitaciones

x2 = grado de criminalidad del barrio

x3 = cercania a los centros de negocio

Si introducimos estas variables al modelo ya no estariamos ya no estariamos en un modelo de regresión simple si no en un modelo de regresión lineal multiple. Ahora nuestra ecuación tiene más variables.

Con una variable --> y = w0 + w1x1 --> recta

Con dos variables --> y = w0 + w1x1 + w2x2 --> plano (el mejor plano que se ajusta a la nube de datos tridimensionales).

y = w0 + w1x1 + w2x2 + w3x3 --> hiperplanos en espacios multidimensionales.

Cada una de estas dimensiones representa una caracteristica de la realidad que los datos representan y podemos tener una cantidad muy elevada de atributos y por tanto de dimensiones.

La forma más rapida de reprentar esta combinación lineal de variables para cada uno de nuestros datos es de forma vectorial, es decir en vez de tener un monton de ecuaciones las representamos en matrices.

y1 = w0 + w1x11 + w2x12 + w3x13

y2 = w0 + w1x21 + w2x22 + w3x23

y3 = w0 + w1x31 + w2x32 + w3x33

y4 = w0 + w1x41 + w2x42 + w3x43

y5 = w0 + w1x51 + w2x52 + w3x53

Podemos crear una matriz donde cada columna representa una caracteristica de nuestros datos de entrada (nº de habitaciones, grado de criminalidad, etc) y cada fila represente cada una de las mediciones que tenemos en nuestro conjunto de datos. Esta seria nuestra matriz X. Igualmente tendriamos un vector de elementos que llamaremos Y y haremos lo mismo con w para generar un vector de parámetros. Ahora podriamos crear una sola ecuación vectorial Y = XW

Las GPUs estan especialmente diseñadas para procesar matrices. 

Volviendo al modelo de regresión lineal simple. Estabamos en que queremos encontrar la recta que mejor represente a los datos pero queremos hacerlo automaticamente ¿cómo lo hacemos? usaremos dos métodos el primero es el metodod de minimos cuadrados ordinarios.

¿Cómo podemos saber que una recta es mejor que otra? la distancia entre el valor predicho (ye) y el valor real (yr) sera el error del modelo para ese punto. Como estamos trabajando con muchos puntos una posible función de coste para nuestro modelo seria coger todas estas distancias y calcular la media

media(yr - ye) --> ahora cojemos estos errores y los elevamos al cuadrado, esta función de costes se llama error cuadratico medio. Al elevar al cuadrado lo que hacemos es penalizar aquellos puntos que estan más alejados de nuestra recta y con menos intensidad a los que se encuentran más cerca. Tendremos que manipular los parámetros de nuestra recta (el termino indendiente y la pendiente) para minimizar esta suma de cuadrados  














Tenemos una realidad compleja que queremos comprender y la hemos 

## Redes neuronales
Ejemplos de uso:
* Reconocimiento de caracteres
* Reconocimiento de imagenes
* Reconocimiento de voz
* Traducción de idiomas
* Generación de testos
* Prevención de fraude
* Conducción autonoma
* Análisis genético
* Pronostico de enfermedades
* Sistemas de clasificación de objetos

Modelamos comportamientos inteligentes

### La neurona

La unidad básica de procesamiento que nos vamos a encontrar en una red neuronal.

Tiene conexiones de entrada a traves de los cuales recibe extimulos externos (los valores de entrada).

Con estos valores la neurona realizara unos calculos internos y generara una salida.

La neurona es una función matemática.

La neurona realizar una suma ponderada de los valores de entrada. A cada conexión de entrada se le asigna un peso (valor que indica como afecta cada entrada a la neurona). Estos pesos son los parametros de nuestro modelo y seran los valores que podemos ajustar para que nuestra red neuronal pueda aprender.

y = w1x1 + w2x2 + w3x3 + b --> es algo asi como una regresión lineal, una recta a la que podemos cambiar la pendiente variando los parametros. Al variar el termino independiente la recta cambia de valor en el eje y. A ese valor se le denomina sesgo o bias.

Variables binarias: solo pueden contener valores 0 o 1























## Referencias

Estos apuntes estan sacados en su mayoría del canal de youtub Dot CSV 

 [Modelos para entender una realidad caótica](https://www.youtube.com/watch?v=Sb8XVheowVQ)
 
 [Regresión Lineal y Mínimos Cuadrados Ordinarios](https://www.youtube.com/watch?v=k964_uNn3l0)
















