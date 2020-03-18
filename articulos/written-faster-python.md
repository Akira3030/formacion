---
layout: default
title: "Writing faster Python"
---

# Writing faster Python

![]({{ site.site_url }}/assets/img/running-1245640_1920.jpg)

## Ordenar una lista

 ```python
sorted(MILLION_RANDOM_NUMBERS) # 467ms
MILLION_RANDOM_NUMBERS.sort() # 77.6 ms (6 veces más rapido)
 ```
 
## Validar si una lista esta vacia

 ```python
if len(mi_lista) == 0 # 91.7ns

if mi_lista == [] # 56.3 ns

if not a mi_lista # 32.4ns
 ```
 
 ## List() o []
 
 ```python
List() # 104 ns
  
[] # 22.5 ns
```

## Contar numero de elementos en una lista

```python
count = 0
for element in MILLION_RANDOM_NUMBERS:
    count += 1
print count
print len(MILLION_RANDOM_NUMBERS) # 96 ns (274000 veces más rapido)
```
 
 ## Filtrar una lista
 
 ```python
 output = []
 for element in MILLON_NUMBERS:
     if element % 2:
         output.append(element)  # 222 ns
 
 [item for item in MILLON_NUMBERS if item % 2] # 127 ms
 ```
 
 ## Borrar elementos de una lista
 
 ```python

unique = []
for element in MILLON_NUMBERS:
     if element not in unique:
         unique.append(element)  # 8.29 s
         
set(MILLON_NUMBERS) # 19,3 ms (400 veces más rapido)
```

## Validar true

 ```python
 if variable == True: # 35.8 ns
 
 if variable is True: # 28.7 ns
 
 if variable # 20.6 ns (75% más rapido)
