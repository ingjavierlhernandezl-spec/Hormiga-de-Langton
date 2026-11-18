Hormiga de Langton en Excel
Simulador de la hormiga de Langton desarrollado exclusivamente con fórmulas de Microsoft Excel, sin VBA ni macros. Utiliza matrices dinámicas y referencias circulares controladas para conservar el estado del tablero y avanzar paso a paso mediante F9.
Descripción
La hormiga recorre una cuadrícula de dos colores. En cada paso, el color de la celda determina un giro de 90 grados; la celda cambia de color y la hormiga avanza. Estas reglas sencillas pueden generar recorridos complejos y estructuras repetitivas.
El proyecto forma parte de una colección de retos de simulación y lógica en Excel.
Características
Simulación mediante fórmulas, sin macros.
Avance por pasos con F9.
Reinicio mediante el control Reset.
Tablero representado mediante una matriz dinámica.
Bordes conectados mediante aritmética modular: topología toroidal.
Color y dirección de la hormiga codificados en un único valor por celda.
Visualización mediante formato condicional.
Requisitos
Microsoft Excel de escritorio con soporte para matrices dinámicas y las funciones LET, LAMBDA, MAKEARRAY y TOROW (ENFILA). En el entorno utilizado para desarrollar el proyecto, MAKEARRAY aparece como ARCHIVOMAKEARRAY.
La ejecución requiere cálculo manual y cálculo iterativo habilitado con un máximo de una iteración. No se ha verificado la compatibilidad con otras aplicaciones de hojas de cálculo.
Cómo ejecutar la simulación
Descarga el archivo `.xlsx` del repositorio y ábrelo en Excel.
En Archivo → Opciones → Fórmulas, habilita el cálculo iterativo.
Establece Número máximo de iteraciones: 1.
Selecciona el modo de cálculo Manual.
Activa Reset y presiona F9 para inicializar el tablero.
Desactiva Reset.
Presiona F9 para avanzar la simulación.
Comprueba que cada pulsación produzca un único paso. La configuración de cálculo de Excel puede afectar también a otros libros abiertos.
Reglas y representación del estado
La convención de giro utilizada es:
Celda blanca: girar 90 grados a la derecha.
Celda negra: girar 90 grados a la izquierda.
Invertir el color de la celda y avanzar una posición.
Esta implementación guarda el estado después de invertir el color de la celda de llegada y antes de efectuar el siguiente giro. La dirección almacenada corresponde al movimiento con el que llegó la hormiga.
En cada actualización se recupera ese estado, se calcula el giro usando el color anterior a la inversión, se avanza y se invierte el color del destino. La celda abandonada conserva el color que ya tenía almacenado.
Estado de la celda	Código
Negra sin hormiga	-1
Blanca sin hormiga	1
Negra con hormiga que llegó hacia arriba (↑)	-20
Negra con hormiga que llegó hacia la derecha (→)	-21
Negra con hormiga que llegó hacia abajo (↓)	-22
Negra con hormiga que llegó hacia la izquierda (←)	-23
Blanca con hormiga que llegó hacia arriba (↑)	20
Blanca con hormiga que llegó hacia la derecha (→)	21
Blanca con hormiga que llegó hacia abajo (↓)	22
Blanca con hormiga que llegó hacia la izquierda (←)	23
La codificación de una celda con hormiga es:

Código = Color × (20 + Dirección)
Color: -1 = negro; 1 = blanco
Dirección: 0 = arriba; 1 = derecha; 2 = abajo; 3 = izquierda

Como el color almacenado ya está invertido, la orientación siguiente se obtiene con RESIDUO(Dirección-Color;4).
Bordes conectados
Las coordenadas se ajustan al tamaño del tablero antes de consultar la celda de destino:

filaDestino = RESIDUO(filaActual-1+desplazamientoVertical;numeroFilas)+1
columnaDestino = RESIDUO(columnaActual-1+desplazamientoHorizontal;numeroColumnas)+1

Estas expresiones describen el cálculo; no son nombres de funciones adicionales del libro. Al salir por un borde, la hormiga reaparece por el opuesto. El tablero es finito y toroidal, no un plano infinito.
La autopista diagonal
En el modelo clásico sobre un plano inicialmente blanco, la hormiga termina formando una autopista: una secuencia de 104 pasos que desplaza su posición dos celdas en cada eje por repetición.
Durante las pruebas de este proyecto se observó visualmente una estructura diagonal repetitiva. En el tablero toroidal, el encuentro con regiones previamente modificadas puede alterar su continuidad; la captura visual por sí sola no demuestra un período de 104 pasos.
Limitaciones
La versión descrita trabaja con una única hormiga.
El rendimiento depende del tamaño de la matriz y del equipo.
El avance depende de la configuración de cálculo de Excel.
La topología toroidal puede producir trayectorias distintas a las del plano infinito.
Autoría y licencia
Copyright (C) 2026 ingjavierlhernandezl-spec.
Este proyecto se distribuye bajo la GNU General Public License, versión 3 exclusivamente (GPL-3.0-only). Consulta el texto completo en LICENSE.
Se permite usar, estudiar, modificar y redistribuir el proyecto bajo las condiciones de esa licencia. Se proporciona sin garantía. La licencia se aplica al trabajo original de este repositorio, no a Microsoft Excel.
Referencias
Langton and his Ant — Universidad de Luxemburgo.
Hardness of Approximation for Langton’s Ant on a Twisted Torus — Algorithms.
GNU General Public License, versión 3 — Free Software Foundation.
Cómo aplicar las licencias GNU.
