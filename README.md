# EscapeBot

Proyecto final de **Paradigmas y Técnicas de Programación** (3º IMAT, ICAI – Universidad Pontificia Comillas, curso 2026-2027).

**Autoras:** Lola Mancebo Olivares y Pilar Pérez Hernández

*Programa tu ruta. Anticípate a la IA. Escapa.*

## Descripción

EscapeBot es un juego de puzles por turnos para un jugador. Un pequeño robot tiene que escapar de un laboratorio vigilado por drones. El jugador no controla el robot en tiempo real: antes de cada intento programa la secuencia completa de instrucciones (avanzar, girar a la izquierda, girar a la derecha, esperar y activar) y, al pulsar Ejecutar, el robot la sigue paso a paso sin que se pueda modificar.

Los drones están controlados por una IA. En cada turno comprueban qué hay en su campo de visión y, si ven al robot, dejan su patrulla y lo persiguen por el camino más corto (A*). Por eso no basta con encontrar una ruta hasta la salida: también hay que prever cómo va a reaccionar cada dron.

- **Victoria:** activar todas las casillas objetivo y llegar a la salida.
- **Derrota:** que un dron capture al robot o que se acaben las instrucciones sin haber ganado.

## Tecnología

- Motor: Unity 6000.6.8f1
- Lenguaje: C#

## Estructura del repositorio

```
docs/
  Entrega1/    Primera entrega: memoria (PDF), diagramas UML y README de la entrega
```

El proyecto de Unity se añadirá en la segunda parte.

## Estado

- [ ] Entrega 1: diseño de arquitectura (UML y memoria) – 3 de diciembre de 2026
- [ ] Entrega 2: juego compilado y proyecto de Unity – 10 de enero de 2027
