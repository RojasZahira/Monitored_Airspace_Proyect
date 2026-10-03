# Monitored Airspace Project

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


##  Lógica Booleana y Ecuaciones

Para diseñar el sistema utilizando exclusivamente **lógica combinacional pura**, se aplicaron las leyes del Álgebra de Boole. Esto permite procesar las señales de manera instantánea mediante compuertas lógicas estándar (familias TTL/CMOS), sin necesidad de microcontroladores ni ciclos de reloj.

### Función Lógica del Sistema
La condición de Alerta Roja ($S$) se define formalmente con la siguiente ecuación:

$$S = (A \lor B \lor C \lor D) \land \neg E$$

### Desglose de los Operadores Lógicos:
* **$\lor$ (OR / O inclusivo):** Utilizado en el bloque $(A \lor B \lor C \lor D)$. Funciona como un selector múltiple: si se detecta un objeto en *cualquier* punto cardinal, toda esta sección se vuelve verdadera ($1$).
* **$\neg$ (NOT / Negación):** Aplicado sobre la señal IFF ($\neg E$). Su función es invertir el estado del código de identificación para detectar específicamente cuando la aeronave **no** cuenta con autorización válida.
* **$\land$ (AND / Y lógico):** Es la compuerta final que vincula las dos condiciones indispensables. Exige obligatoriamente que haya presencia en el espacio aéreo **Y AL MISMO TIEMPO** que el código IFF no sea válido para disparar la Alerta Roja ($S = 1$).


