# nes_controller.v
Repositorio para reunir el desarrollo en el controlador NES

### Master y slave 
En este caso, master es el módulo de la FPGA o el SoC encargado de controlar el NES
Slave es el mando físico del NES 
## Protocolo de Comunicación del NES

Aproximadamente cada 16ms (al manejar 60Hz) se repite lo siguiente: 

Latch es un pulso enviado por master que 'congela' el estado del 4021N interno en el mando físico de la NES. En el momento donde este pulso baja, automáticamente la línea Data revela el valor del primer bit, correspondiente al estado del botón 'A'. Posteriormente, se envia una secuencia de 7 pulsos para relevar los valores correspondientes a los demás botones. 

Sin embargo, el módulo maneja lógica 'inversa': Cuando está oprimido un botón, se obtiene '0' como valor, y cuando no está oprimido, se obtiene '1'. Por lo que cuando la línea Data llega a la FPGA, se le aplica una compuerta NOT
