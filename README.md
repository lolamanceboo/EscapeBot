# EscapeBot

Proyecto final de Paradigmas y Técnicas de Programación · 3º IMAT · Curso 2026-2027

**Autoras:** Lola Mancebo Olivares y Pilar Pérez Hernández · 

## Descripción

EscapeBot es un juego de puzles por turnos para un jugador. Un robot tiene que escapar de una sala vigilada por drones. El jugador no lo mueve en directo: primero programa todos sus pasos y, al pulsar Ejecutar, el robot los sigue uno a uno sin que se puedan cambiar.

**Objetivo:** activar todas las casillas objetivo del nivel y llegar a la salida sin que te atrape un dron, usando como máximo las instrucciones que permite el nivel.

## Cómo se juega

1. En el menú principal, pulsa **Jugar** o elige un nivel.
2. **Planificación:** observa el tablero, los drones, sus rutas y lo que ve cada uno. Añade instrucciones a la lista con los botones (hay un máximo por nivel). Puedes borrar la última o vaciar la lista.
3. Pulsa **Ejecutar**. El robot hace una instrucción por turno y después se mueven los drones.
4. Al terminar, elige **Reintentar**, **Siguiente nivel** (solo si has ganado) o **Menú**.

| Instrucción | Qué hace |
|---|---|
| Avanzar | Mueve el robot una casilla hacia donde mira. Si hay pared, no se mueve y pierde el turno. |
| Girar izquierda / derecha | Gira 90° sin moverse. |
| Esperar | El robot no se mueve, pero los drones sí. |
| Activar | Activa la casilla objetivo en la que está. |

Se **gana** al activar todos los objetivos y llegar a la salida. Se **pierde** si un dron atrapa al robot o si se acaban las instrucciones.

**Puntuación** (al ganar): `1000 − 10 × turnos − 25 × instrucciones de más − 50 × reintentos` (mínimo 0). Desde 800 puntos se consiguen 3 estrellas y desde 500, 2. Se guarda la mejor de cada nivel.

## Los drones

| Dron | Qué ve | Cómo se comporta |
|---|---|---|
| Patrullero | Las 2 casillas que tiene justo delante, en línea recta. | Recorre siempre la misma ruta y no persigue. Te atrapa si entras en su zona de visión o coincidís en la misma casilla. |
| Perseguidor | Hasta 3 casillas por delante, en forma de cono. | Patrulla, y si ve al robot lo persigue por el camino más corto (A*). Si lo pierde, va a buscarlo donde lo vio por última vez. |
| Predictor | Lo mismo que el perseguidor y las 2 o 3 siguientes instrucciones del jugador. | Va hacia donde va a estar el robot para cortarle el paso. Se mueve una casilla cada dos turnos. |

Las paredes tapan la visión de los drones. Ningún dron conoce la partida entera: cada uno solo usa lo que puede ver.

## Niveles

| Nº | Nombre | Drones |
|---|---|---|
| 1 | Primer protocolo | Ninguno (tutorial) |
| 2 | Cambio de turno | 1 Patrullero |
| 3 | En el punto de mira | 1 Perseguidor |
| 4 | Punto ciego | Patrullero y Perseguidor |
| 5 | Intercepción | 1 Predictor |

Nos comprometemos a hacer los niveles 1, 2 y 3 con el patrullero y el perseguidor. El predictor y los niveles 4 y 5 son ampliaciones que haremos si hay tiempo. La lista es orientativa y puede cambiar durante el desarrollo.

## Arquitectura

El diagrama de clases (aproximación inicial) está en la carpeta UML. Hemos separado las reglas del juego, que son clases normales de C#, de lo que se dibuja en pantalla. Los niveles son datos que construye una fábrica, y reintentar es borrar el nivel y volver a crearlo.

| Patrón | Dónde | Para qué |
|---|---|---|
| Command | `ICommand` y `CommandQueue` | Cada instrucción es un objeto, así el programa es una lista que se puede editar y ejecutar paso a paso. |
| State | `GameStateMachine` y `DroneStateMachine` | Cada estado tiene su comportamiento y los cambios de estado están en un solo sitio. |
| Strategy | `IEnemyStrategy` | Cambiar cómo decide un dron sin tocar la clase del dron. |
| Observer | `GameEvents` | Las reglas avisan de lo que pasa y la parte visual escucha. |
| Factory | `LevelFactory` | Todos los objetos de la partida se crean en un sitio y se destruyen al acabar. |
