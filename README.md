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