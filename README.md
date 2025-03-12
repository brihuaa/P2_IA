# Juego de "Lobos y Ovejas en el Río" - Resolución con A* (Algoritmo de Búsqueda A*)

En esta práctica, resolveremos el juego **‘Lobos y Ovejas en el Río’** utilizando el algoritmo **A\* (A-Star)**. El objetivo del juego es trasladar un número igual de **lobos** y **ovejas** desde un lado del río al otro, utilizando una **embarcación** bajo ciertas restricciones. A través de este proyecto, implementaremos un algoritmo de búsqueda para encontrar una solución a este problema.

## Enunciado

El juego consiste en ayudar a un grupo de lobos y ovejas a cruzar un río mediante el uso de una embarcación. Sin embargo, para garantizar la seguridad de las ovejas, existe una restricción importante: **los lobos no pueden superar en número a las ovejas en ningún lado del río**.

### Reglas del juego:

1. Inicialmente, hay **n ovejas (O)** y **n lobos (L)** en el lado **izquierdo** del río.
2. En cada movimiento, solo se pueden transportar **uno o dos animales** a la vez en la embarcación.
3. La embarcación **no puede cruzar** el río si no hay al menos **un animal** en ella.
4. En ningún momento puede haber más lobos que ovejas en **ningún lado del río**. Solo puede haber más lobos que ovejas si en ese lado del río no hay ovejas.
5. El **objetivo** es mover todas las ovejas y los lobos al lado derecho del río.

### Restricciones:
- El algoritmo debe asegurar que las reglas del juego se respeten durante todo el proceso de traslado.
- El algoritmo utilizado para la búsqueda de soluciones es el **A\***, que optimiza el camino hacia la solución considerando tanto el coste acumulado de las acciones como una heurística que guía la búsqueda.

### Definición de costes

- **Coste acumulado (g):** Representa el número de pasos realizados desde el estado inicial hasta el estado actual.
- **Heurística (h):** En este caso, la heurística es el número total de animales que aún no han cruzado el río. Cuantos más animales sin trasladar, mayor será la heurística, guiando el algoritmo a los estados que parecen estar más cerca del objetivo.
- **Coste total (f):** Es la suma de `g` y `h`, y el algoritmo selecciona el estado con el menor valor de `f` en cada iteración.

### Estudio Comparativo

- **Solución A\* (3 ovejas, 3 lobos):**
  
  ```plaintext
  [(3, 3, 0, 0, 'izq'), (3, 1, 0, 2, 'der'), (3, 2, 0, 1, 'izq'), (3, 0, 0, 3, 'der'),
   (3, 1, 0, 2, 'izq'), (1, 1, 2, 2, 'der'), (2, 2, 1, 1, 'izq'), (0, 2, 3, 1, 'der'),
   (0, 3, 3, 0, 'izq'), (0, 1, 3, 2, 'der'), (1, 1, 2, 2, 'izq'), (0, 0, 3, 3, 'der')]
   ```
   Tiempo de Ejecución A*:
  ```plaintext
  0.0012784004211425781 segundos

  ```


- **Solución BFS\* (3 ovejas, 3 lobos):**
  
  ```plaintext
  [(3, 3, 0, 0, 'izq'), (2, 2, 1, 1, 'der'), (3, 2, 0, 1, 'izq'), (3, 0, 0, 3, 'der'), 
  (3, 1, 0, 2, 'izq'), (1, 1, 2, 2, 'der'), (2, 2, 1, 1, 'izq'), (0, 2, 3, 1, 'der'), 
  (0, 3, 3, 0, 'izq'), (0, 1, 3, 2, 'der'), (1, 1, 2, 2, 'izq'), (0, 0, 3, 3, 'der')]

   ```
   Tiempo de Ejecución BFS:
  ```plaintext
 0.0007214546203613281 segundos

  ```  
## Comparativa

### Nodos Visitados: 
A* realiza una exploración más eficiente gracias a la heurística, visitando menos nodos que una búsqueda no informada.

### Nodos Generados: 
La optimización por la heurística reduce la cantidad de nodos generados en comparación con otros algoritmos de búsqueda como BFS.

### Solución Obtenida:
 La solución proporcionada por A* es óptima, siguiendo una ruta que respeta las restricciones del problema.
¿Es el heurístico admisible?
Sí, la heurística utilizada es admisible, ya que nunca sobreestima el coste restante. En este caso, la heurística es simplemente el número de animales que aún no han cruzado el río, lo cual siempre es una estimación válida y no mayor que el coste real necesario para alcanzar el objetivo.

## Conclusión
El algoritmo A* es eficiente para este tipo de problema, ya que, al ser informado, optimiza la exploración del espacio de búsqueda y encuentra la solución más rápido que algoritmos no informados. La heurística utilizada es admisible y ayuda a guiar la búsqueda de manera eficaz.



## Diagrama de Estados

Cada estado del juego se representa por una tupla que contiene:
- **ovejas_izq**: el número de ovejas en el lado izquierdo del río.
- **lobos_izq**: el número de lobos en el lado izquierdo del río.
- **ovejas_der**: el número de ovejas en el lado derecho del río.
- **lobos_der**: el número de lobos en el lado derecho del río.
- **barca_pos**: la posición de la embarcación (izquierda o derecha).

## 1. Estado y Conjunto de Estados

Un **estado** en este juego está definido por la configuración actual de los animales en ambos lados del río, es decir:
- La cantidad de ovejas y lobos en el lado izquierdo y derecho del río, así como la posición de la embarcación.

Por ejemplo, un estado puede ser:
```plaintext
(3, 2, 0, 1, 'izq')
```

Esto significa que en el lado izquierdo del río hay 3 ovejas y 2 lobos, mientras que en el lado derecho hay 0 ovejas y 1 lobo, y la embarcación está en el lado izquierdo.

El conjunto de estados es el conjunto de todas las configuraciones posibles que se pueden alcanzar durante el juego, siempre respetando las reglas y restricciones del juego.

## 2. Acción, Operadores y Factores de Ramificación

### Acción:
Una acción es un movimiento realizado por el barquero con la embarcación. En cada acción, el barquero puede transportar entre 1 o 2 animales (ovejas, lobos o una combinación de ambos).

### Operadores:
Los operadores son las posibles acciones que el barquero puede realizar. Los operadores en este problema incluyen:

- Transportar 1 oveja.
- Transportar 1 lobo.
- Transportar 2 ovejas.
- Transportar 2 lobos.
- Transportar 1 oveja y 1 lobo.

Son de tipo Parametrizados Y no son específicos porque 


### Factores de Ramificación:
El factor de ramificación es el número de acciones posibles que el barquero puede realizar en un estado dado. En cada estado, el barquero puede tomar 5 acciones diferentes, lo que da un factor de ramificación de 5.

## 3. Definición del Estado Inicial y Estado Objetivo

### Estado Inicial:
El estado inicial es el estado en el que todos los animales (ovejas y lobos) están en el lado izquierdo del río y la embarcación también está en ese lado.

Por ejemplo, si tenemos 3 ovejas y 3 lobos, el estado inicial sería:
```plaintext
(3, 3, 0, 0, 'izq')
```

Esto ha sido interpretado a través del código en initial_easy.scv:

```plaintext
(OOLL; ;I')
```
Esto significa que hay 3 ovejas y 3 lobos en el lado izquierdo, 0 ovejas y 0 lobos en el lado derecho, y la embarcación está en el lado izquierdo.

## Estado Objetivo:
El estado objetivo es el estado en el que todos los animales (ovejas y lobos) han cruzado al lado derecho del río, y la embarcación también está en ese lado.

En nuestro ejemplo de 3 ovejas y 3 lobos, el estado objetivo sería:
```plaintext
(0, 0, 3, 3, 'der')
```
Que sería:
```plaintext
(;OOLL ;I)
```

Esto significa que las 3 ovejas y los 3 lobos han llegado al lado derecho del río y la embarcación también está en el lado derecho.

### Implementación del Algoritmo A*
El algoritmo A* se utiliza para encontrar la solución óptima al problema. Este algoritmo combina la búsqueda informada con una función heurística que estima el coste restante para alcanzar el objetivo. En este caso, la heurística puede ser el número total de animales que aún no han cruzado el río.

## Pasos del Algoritmo:

- **Inicialización**: Comienza con el estado inicial.

- **Exploración**: Genera todos los estados posibles a partir del estado actual, aplicando los operadores válidos.

- **Evaluación**: Calcula el coste acumulado y la heurística para cada estado generado.

- **Selección**: Selecciona el estado con el menor coste total (coste acumulado + heurística) para continuar la búsqueda.

- **Repetición**: Repite el proceso hasta alcanzar el estado objetivo
