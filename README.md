# Sistema de Radar Combinacional de Vigilancia Aeroespacial

Proyecto desarrollado para la materia **Electrónica Digital**.

## Descripción del Proyecto
Este proyecto consiste en un sistema digital de alerta temprana basado exclusivamente en **lógica combinacional pura**. Su función principal es simular el monitoreo del espacio aéreo de una nación, detectando la presencia de aeronaves u objetos en diferentes sectores y evaluando de forma instantánea si representan una actividad inesperada (intrusión o aeronave sin identificación válida) mediante compuertas lógicas y Álgebra de Boole.

Al no utilizar microcontroladores ni ciclos de reloj (circuitos secuenciales), el sistema responde de manera inmediata y determinista a las combinaciones de entradas binarias aplicadas en los sensores.

##  Variables del Sistema

### Entradas (Sensores / Simulación por Dip Switch)
* **A (Sector Norte):** 1 si se detecta un objeto, 0 si está despejado.
* **B (Sector Sur):** 1 si se detecta un objeto, 0 si está despejado.
* **C (Sector Este):** 1 si se detecta un objeto, 0 si está despejado.
* **D (Sector Oeste):** 1 si detecta un objeto, 0 si está despejado.
* **E (Códifo IFF):** 1 si el código de transpondedor es válido (Amigo), $0$ si es desconocido o no responde (Amenaza). 

### Salidas (Indicadores)
* **LEDs de Sector (A, B, C):** Indican visualmente el sector donde hay presencia de un objeto.
* **Alerta Roja (S):** Salida lógica principal que se activa ($1$) si hay un objeto en *cualquier* sector **Y** su código IFF no es válido (D = 0).

### Lógica Booleana y Ecuación 
* **Ecuación:** Z=(A+B+C+D)xE$$

