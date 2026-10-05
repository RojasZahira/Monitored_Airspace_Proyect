# Monitored Airspace Project

Proyecto desarrollado para la materia **Electrónica Digital**.

## Descripción del Proyecto
Este proyecto consiste en un sistema digital de alerta temprana basado  en **lógica combinacional pura**. Su función principal es simular el monitoreo del espacio aéreo de una nación, detectando la presencia de aeronaves u objetos en diferentes sectores y evaluando de forma instantánea si representan una actividad inesperada (intrusión o aeronave sin identificación válida) mediante compuertas lógicas y Álgebra de Boole.



##  Variables del Sistema

### Entradas (Sensores / Simulación por Dip Switch)
* **A (Sector Norte):** 1 si se detecta un objeto, 0 si está despejado.
* **B (Sector Sur):** 1 si se detecta un objeto, 0 si está despejado.
* **C (Sector Este):** 1 si se detecta un objeto, 0 si está despejado.
* **D (Sector Oeste):** 1 si detecta un objeto, 0 si está despejado.
* **E (Códifo IFF):** 1 si el código de transpondedor es válido (Amigo), $0$ si es desconocido o no responde (Amenaza). 

### Salidas (Indicadores)
* **LEDs de Sector (A, B, C, D):** Indican visualmente el sector donde hay presencia de un objeto.
* **Alerta Roja (z):** Salida lógica principal que se activa ($1$) si hay un objeto en *cualquier* sector **Y** su código IFF no es válido (E = 0).


##  Lógica Booleana y Ecuaciones

Para diseñar el sistema utilizando exclusivamente **lógica combinacional pura**, se aplicaron las leyes del Álgebra de Boole.

### Función Lógica del Sistema
La condición de Alerta Roja ($Z$) se define formalmente con la siguiente ecuación:

$$Z = (A \lor B \lor C \lor D) \land \neg E$$

### Desglose de los Operadores Lógicos:
* **$\lor$ (OR / O inclusivo):** Utilizado en el bloque $(A \lor B \lor C \lor D)$. Funciona como un selector múltiple: si se detecta un objeto en *cualquier* punto cardinal, toda esta sección se vuelve verdadera ($1$).
* **$\neg$ (NOT / Negación):** Aplicado sobre la señal IFF ($\neg E$). Su función es invertir el estado del código de identificación para detectar específicamente cuando la aeronave **no** cuenta con autorización válida.
* **$\land$ (AND / Y lógico):** Es la compuerta final que vincula las dos condiciones indispensables. Exige obligatoriamente que haya presencia en el espacio aéreo **Y AL MISMO TIEMPO** que el código IFF no sea válido para disparar la Alerta Roja ($Z = 1$).

### Tabla de verdad
## 📊 Tabla de Verdad del Sistema

| $A$ (Norte) | $B$ (Sur) | $C$ (Este) | $D$ (Oeste) | $E$ (IFF Válido) | Presencia $(A \lor B \lor C \lor D)$ | $\neg E$ | Salida Alerta ($Z$) | Estado del Espacio Aéreo |
| :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :--- |
| 0 | 0 | 0 | 0 | 0 | 0 | 1 | **0** | Seguro (Sin blancos) |
| 0 | 0 | 0 | 1 | 0 | 1 | 1 | **1** |  **ALERTA: Intruso en Oeste** |
| 0 | 0 | 1 | 0 | 0 | 1 | 1 | **1** |  **ALERTA: Intruso en Este** |
| 0 | 0 | 1 | 1 | 0 | 1 | 1 | **1** |  **ALERTA: Intrusos (Este/Oeste)** |
| 0 | 1 | 0 | 0 | 0 | 1 | 1 | **1** |  **ALERTA: Intruso en Sur** |
| 0 | 1 | 0 | 1 | 0 | 1 | 1 | **1** |  **ALERTA: Intrusos (Sur/Oeste)** |
| 0 | 1 | 1 | 0 | 0 | 1 | 1 | **1** |  **ALERTA: Intrusos (Sur/Este)** |
| 0 | 1 | 1 | 1 | 0 | 1 | 1 | **1** |  **ALERTA: Intrusos múltiples** |
| 1 | 0 | 0 | 0 | 0 | 1 | 1 | **1** |  **ALERTA: Intruso en Norte** |
| 1 | 0 | 0 | 1 | 0 | 1 | 1 | **1** |  **ALERTA: Intrusos (Norte/Oeste)** |
| 1 | 0 | 1 | 0 | 0 | 1 | 1 | **1** |  **ALERTA: Intrusos (Norte/Este)** |
| 1 | 0 | 1 | 1 | 0 | 1 | 1 | **1** |  **ALERTA: Intrusos múltiples** |
| 1 | 1 | 0 | 0 | 0 | 1 | 1 | **1** |  **ALERTA: Intrusos (Norte/Sur)** |
| 1 | 1 | 0 | 1 | 0 | 1 | 1 | **1** |  **ALERTA: Intrusos múltiples** |
| 1 | 1 | 1 | 0 | 0 | 1 | 1 | **1** |  **ALERTA: Intrusos múltiples** |
| 1 | 1 | 1 | 1 | 0 | 1 | 1 | **1** |  **ALERTA: Todos los sectores vulnerados** |
| 0 | 0 | 0 | 0 | 1 | 0 | 0 | **0** | Tráfico autorizado (Despejado) |
| 0 | 0 | 0 | 1 | 1 | 1 | 0 | **0** | Tráfico autorizado en Oeste |
| 0 | 0 | 1 | 0 | 1 | 1 | 0 | **0** | Tráfico autorizado en Este |
| 0 | 0 | 1 | 1 | 1 | 1 | 0 | **0** | Tráfico autorizado en Este/Oeste |
| 0 | 1 | 0 | 0 | 1 | 1 | 0 | **0** | Tráfico autorizado en Sur |
| 0 | 1 | 0 | 1 | 1 | 1 | 0 | **0** | Tráfico autorizado en Sur/Oeste |
| 0 | 1 | 1 | 0 | 1 | 1 | 0 | **0** | Tráfico autorizado en Sur/Este |
| 0 | 1 | 1 | 1 | 1 | 1 | 0 | **0** | Tráfico autorizado múltiple |
| 1 | 0 | 0 | 0 | 1 | 1 | 0 | **0** | Tráfico autorizado en Norte |
| 1 | 0 | 0 | 1 | 1 | 1 | 0 | **0** | Tráfico autorizado en Norte/Oeste |
| 1 | 0 | 1 | 0 | 1 | 1 | 0 | **0** | Tráfico autorizado en Norte/Este |
| 1 | 0 | 1 | 1 | 1 | 1 | 0 | **0** | Tráfico autorizado múltiple |
| 1 | 1 | 0 | 0 | 1 | 1 | 0 | **0** | Tráfico autorizado en Norte/Sur |
| 1 | 1 | 0 | 1 | 1 | 1 | 0 | **0** | Tráfico autorizado múltiple |
| 1 | 1 | 1 | 0 | 1 | 1 | 0 | **0** | Tráfico autorizado múltiple |
| 1 | 1 | 1 | 1 | 1 | 1 | 0 | **0** | Tráfico autorizado masivo |



