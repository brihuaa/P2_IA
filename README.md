# Juego de "Lobos y Ovejas en el Río" - Resolución con A* (Algoritmo de Búsqueda A*)

En esta segunda práctica vamos a resolver el juego **‘Lobos y Ovejas en el Río’** utilizando el algoritmo **A\* (A-Star)**. El objetivo del juego es trasladar un número igual de **lobos** y **ovejas** desde un lado del río al otro, utilizando una **embarcación** bajo ciertas restricciones. A través de este proyecto, implementaremos un algoritmo de búsqueda para encontrar una solución a este problema.

## Enunciado

El juego trata de ayudar a un grupo de lobos y ovejas a cruzar un río mediante el uso de una embarcación. No obstante, para que las ovejas se encuentren seguras hay una restricción importante: **los lobos no pueden superar en número a las ovejas en ningún lado del río**.

### Reglas del juego:

1. Inicialmente, tienes **n ovejas (O)** y **n lobos (L)** en el lado **izquierdo** del río.
2. En cada iteración, únicamente puedes transportar uno o dos animales a la vez en la embarcación.
3. La embarcación **no puede cruzar** el río si no hay al menos **un animal** en ella.
4. En ningún momento puede haber más lobos que ovejas en **ningún lado del río**. Solo puede haber más lobos que ovejas si en ese lado del río no hay ovejas.
5. El **objetivo** es mover todas las ovejas y los lobos al lado derecho del río.

### Restricciones:
- El algoritmo debe asegurar que las reglas del juego se respeten durante todo el proceso de traslado.
- El algoritmo utilizado para la búsqueda de soluciones es el **A\***, que optimiza el camino hacia la solución considerando tanto el coste acumulado de las acciones como una heurística que guía la búsqueda.

## Estructura del Proyecto

El código se organiza en varias funciones clave:

1. **Heurística**:
   - Utilizamos una heurística sencilla que calcula la cantidad de ovejas y lobos en el lado izquierdo del río. Esto permite estimar el número de animales que faltan por mover.

2. **Operaciones posibles**:
   - El barquero puede transportar 1 o 2 animales a la vez: uno o dos lobos, una o dos ovejas, o una combinación de ambos.

3. **Generación de hijos**:
   - Generamos los estados alcanzables tras mover a uno o más animales con la embarcación.

4. **Función de validación**:
   - Aseguramos que no se violen las reglas del juego durante el movimiento de los animales (es decir, que no haya más lobos que ovejas en ningún lado).

5. **Algoritmo A\***:
   - El algoritmo **A\*** es utilizado para encontrar la solución al problema, calculando el coste total de cada estado, que incluye tanto el coste acumulado como la heurística. La búsqueda es optimizada utilizando una cola de prioridad (`heapq`).

## Diagrama de Estados

Cada estado del juego se representa por una tupla que contiene:
- **ovejas_izq**: el número de ovejas en el lado izquierdo del río.
- **lobos_izq**: el número de lobos en el lado izquierdo del río.
- **ovejas_der**: el número de ovejas en el lado derecho del río.
- **lobos_der**: el número de lobos en el lado derecho del río.
- **barca_pos**: la posición de la embarcación (izquierda o derecha).

## Ejemplo de Ejecución

Para **n = 3** (3 ovejas y 3 lobos), el algoritmo busca una secuencia de movimientos que mueva todos los animales de manera segura al lado derecho del río, respetando las reglas mencionadas.

