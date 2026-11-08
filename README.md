# Monitored Airspace Project
**Monitored Airspace Proyect** es un dispositivo con la estructura y funcionamiento básico de una antena telefónica, pero utiliza la tecnología de un radar para simular el monitoreo del espacio aéreo de una nación, detectando la presencia de aeronaves en diferentes sectores y evaluando de forma instantánea si hay actividad inesperada. 


##  Partes del sistema

### Los ceros y unos son las respuestas que da el sistema en caso de detectar una aeronave
* **A (Prohibida):** 1 si se detecta un objeto, 0 si está despejado.
* **B (Habilitada 1):** 1 si se detecta un objeto, 0 si está despejado.
* **C (Habilitada 2):** 1 si se detecta un objeto, 0 si está despejado.
Z1(LED verde)
Z2(LED roja)
### Función Lógica del Sistema

$$Z = (A + B + C)( \neg A + B + C)$$


| $A$  | $B$ | $C$ | $Z1$ | $Z2$ | 
| :---: | :---: | :---: | :---: | :---: |
| 0 | 0 | 0 | 0 | 0 |
| 0 | 0 | 0 | 0 | 1 |
| 0 | 1 | 1 | 0 | 1 |
| 0 | 1 | 1 | 0 | 1 | 
| 1 | 0 | 0 | 1 | 0 |
| 1 | 0 | 0 | 1 | 1 | 
| 1 | 1 | 1 | 1 | 1 |
| 1 | 1 | 1 | 1 | 1 | 

