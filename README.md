# Monitored Airspace Project
**Monitored Airspace Proyect** es un dispositivo con la estructura y funcionamiento básico de un satélite, pero utiliza la tecnología de un radar para simular el monitoreo del espacio aéreo de una nación, detectando la presencia de aeronaves en diferentes sectores y evaluando de forma instantánea si hay actividad inesperada. 


##  Partes del sistema

### Los ceros y unos son las respuestas que da el sistema en caso de detectar una aeronave
* **A (Prohibida):** 1 si se detecta un objeto, 0 si está despejado.
* **B (Habilitada 1):** 1 si se detecta un objeto, 0 si está despejado.
* **C (Habilitada 2):** 1 si se detecta un objeto, 0 si está despejado.
Z1(LED verde)
Z2(LED roja)
### Función Lógica del Sistema

$$Z = (A \lor B \lor C \lor D) \land \neg E$$


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



