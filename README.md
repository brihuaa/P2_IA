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

### Factores de Ramificación:
El factor de ramificación es el número de acciones posibles que el barquero puede realizar en un estado dado. En cada estado, el barquero puede tomar 5 acciones diferentes, lo que da un factor de ramificación de 5.

## 3. Definición del Estado Inicial y Estado Objetivo

### Estado Inicial:
El estado inicial es el estado en el que todos los animales (ovejas y lobos) están en el lado izquierdo del río y la embarcación también está en ese lado.

Por ejemplo, si tenemos 3 ovejas y 3 lobos, el estado inicial sería:
```plaintext
(3, 3, 0, 0, 'izq')
