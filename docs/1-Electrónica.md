# 馃捇 Electr贸nica

## Dise帽o
El dispositivo de electronica (nodo sensor) dise帽ado para el monitoreo de de agua en intervalos de tiempo de manera aut贸noma, esta basado en tomar las medidas con sesores para ser enviadas mediante comunicaci贸n serial a un sistema de comunicaci贸n para el monitorio de estas caracter铆sticas, este dispositivo tomar谩 medidas de pH, Condutividad, turbidez, temperatura y presi贸n.

\*imagen sistema completo resaltando el nodo sensor*

### Prototipo
Como prototipo inicial se realiz贸 un circuito en Arduino para realizar pruebas con sesores, medidas y comunicaci贸n para obtener una versi贸n funcional que pudiera enviar los datos.
#### Selecci贸n de componentes
Dado lo anterior los componentes que integran este prototipo inicial son los siguientes:

1. Arduino Nano: Microcontrolador principal.
1. ADC: Lectura de se帽ales anal贸gicas a digitales.
1. RTC: Encargado de establecer los tiempo de medidas mediante alarmas y estado de reposo.   
1. Modulo SD para el guardado de los datos medidos.
1. Sensores: Temperatura, conducitividad, pH, Presi贸n y Turbidez. 
1. RS485: Para realizar una comunicaci贸n serial de gran alcance(>10m).

Destacar que estos sensores seleccionados se sometieron a una serie de pruebas para comprobar su rendimiento, ver sus limitaciones y desgaste en el tiempo.

Como resultados iniciales se tiene un nodo sensor capaz de obtener medidas de los sensores, guardar estos datos en una microSD y ademas enviar estos datos de manera serial y un prototipo inicial lo suficientemente 煤til para la realizaci贸n de pruebas en profundidad y analizar las limitaciones de los sensores.
### PCB
Continuando con las mejoras del del nodo sensor, y el prototipo funcionando de manera adecuada, en conjunto con "MCI electronic" (Frabicante local de PCB y dise帽o de circuitos), se llevo a cabo la integraci贸n completa del prototipo a una PCB con mejoras incluidas dadas principalmente en el sistema de energ铆a:

1. Agregar al nodo un circuito de energ铆a que sea alimentado a trav茅z de bater铆as de litio 18650 con toda su electr贸nica para un correcto funcionamiento (Cagardores y elevadores).
1. Dividir la fuente de energ铆a en una activa (5V) que siempre entrega alimentaci贸n al sistema y una de reposo (5Vs) que se apaga cuando el sistema no esta midiendo o enviado datos para aquellos componentes que puedan ser apagados para reducir el consumo lo mayor posible.

<img title="a title" alt="Alt text" src="images/diagrama_alimentacion.png">

La PCB incluye toda la electr贸nica de sensores y las necesarias  como reguladores de voltaje (-5V,3V,-3V y 3.3V) siendo una pieza completa que se insertan los sensores para tomar las medidas. Posee ademas una conexion FTDI para realizar la programaci贸n del microcontrolador.

<img title="a title" alt="Alt text" src="images/PCBnombrada_v0.png">


#### Historial de Versiones

Debido a diversos tipo de situaciones como falta de pistas o distribuciones de los componentes en diferentes fuentes de energ铆a (5V y 5Vs) o simple optimizaci贸n de esta, se obtuvieron varias versiones de PCB a modo de mejora.

1. **Versi贸n N掳1:** La primera placa PCB entrega por "MSI electronic" Con cables en la parte frontal entr el RTC y el microcontrolador.

<img title="a title" alt="Alt text" src="images/diagrama_version1.png">

Detalles:

* Esta versi贸n de la placa posee el pin de medida de la alimentaci贸n 5Vs antes la electr贸nica del "switch" que permite apagarla en reposo.
* Por otro lado la alimentacion 5Vs alimenta el componente de comunicaci贸n Rs485 y al regulador de -5V realizando modificaci贸nes en las fuentes de energ铆a.

**Modificaci贸n 1:** Debido a que simplemente la alimentaci贸n apagaba el RS485 y un regulador, se realizaron cambios para dejar d en la alimentaci贸n de reposo(5Vs) a los sensores y los reguladores faltantantes que seran utilizados solamente en medida y env铆o de datos. Para ello se cort贸 una pista separando los reguladores y sensores con la alimentacion continua (5V) y se agreg贸 un cable para alimentarlos con 5Vs.

<img title="a title" alt="Alt text" src="images/diagrama_modificacion1.png">

Como resultados trajo mejoras en el consumo.

**Modificaci贸n 2**: Se procedi贸 a cambiar el componente de la comunicaci贸n 485 por uno est谩ndar (Max485) ya que el que se tiene considerado esta versi贸n es muy antiguo y posee un
consumo elevado aun cuando no se est谩 transmitiendo para reducir m谩s el consumo de este.

Tras relizar el cambio a mano se presentaron problemas en las conexiones entre compoentes dejando de utilizar esta versi贸n.


1. **Versi贸n N掳2:** Segunda placa PCB entregada por MSI, que posee un cable en la parte posterior por la falta de una ruta.

Detalles:

*  La configuracion entre la alimentacion y los componentes es ligeramente diferente a la primera versi贸n con su primera modificaci贸n debido a que posee el componete de comunicaci贸n 485 a la alimentaci贸n constante 5V.
* Esta placa fue devuelta para la correcci贸n de la ruta faltante.
* Los Archivos que se tienen de PCB son las de esta versi贸n con la ruta faltante.

<img title="a title" alt="Alt text" src="images/diagrama_version2.png">

3. **Versi贸n N掳3**: Esta versi贸n es la placa anterior con la ruta corregida.

### mejoras no realizadas

Como mejoras no realizadas se tiene el cambio del componente de comunicaci贸n 485 de alto consumo debido a que es antiguo, aun m谩s en esta versi贸n ya que esta conectado en la alimentaci贸n constante por lo que este consume con el sistema en reposo.
## Fabricaci贸n

Con los archivos de una versi贸n funcional del sistema (Versi贸n N掳2), se realiz贸 un estudio en la fabricacion de esta placa para tener una idea y obtener un analisis en terminos de los costos que tiene finalmente el "nodo sensor". 


### Cotizaci贸n:
Para cotizar se considero la posibilidad de una fabricaci贸n y ensablaje completamente externo con los componetes entregados por el fabricante.

1. Fabricaci贸n y ensamblaje externo:
Consireaciones:
 * Para esta cotizaci贸n se tomaron en cuenta los fabricantes: JLCPCB, PCBway, PCBgogo, EEcart, SeedStudio.
 * Los precios obtenidos son dados en base a cotizaciones rapidas entregadas por los fabricantes.
 * Los archivos requeridos para las cotizaciones cortas son: Gerber (PCB), BOM (componentes) con un formato espec铆fico para cada fabricante y el *"pick and place"* en algunos casos.
 * La cotizaci贸n fue realizada para una cantidad de 5 PCBs ensambladas (cantidad m铆nima aceptada).

Se descart贸 JLCPCB ya que su servicio de ensamblado es muy limitado.

Costos: Tabla de precios en USD.

|     Fabricante    |     Cant    |     Placa     |     Componentes    |     Costo Assembly.    |     Env铆o      |     Total       |
|-------------------|-------------|---------------|--------------------|------------------------|----------------|-----------------|
|     EECART        |     5       |     $8.93     |     $702.957       |     $ 145.37           |     $50.00*    |     $907.26     |
|     PCBWAY        |     5       |     $87.66    |     $679.41        |     $88.00             |     $49.69     |     $904.76     |
|     PCBGOGO       |     5       |     $24.00    |     $1237.00       |     $160.00            |     $93.00     |     $1493.00    |
|     SEEDSTUDIO    |     5       |     $52.69    |     -              |     $281.52            |     $0         |     $912.93     |


Tiempo: Tiempo total de fabricaci贸n luego de la confirmaci贸n del fabricante.

|     Fabricante    |     Fabricaci贸n   |     Ensamblado    |        Env铆o      |     Total de tiempo   |
|:-----------------:|:-----------------:|:-----------------:|:-----------------:|:---------------------:|
|       EECART      |       4 D铆as      |        29 D铆as    |     2-3D铆as       |       5 Semanas       |
|       PCBWAY      |      3-4 D铆as     |      28 D铆as      | 4-7D铆as H谩biles   |      5.5 Semanas      |
|       PCBGOGO     |       1 D铆a       |         -         |  5-7D铆as H谩biles  |       4 Semanas       |
|     SEEDSTUDIO    |         -         |      29 D铆as      |  5-7D铆as H谩biles  |       5 Semanas       |

Dado los tiempos de fabricaci贸n, tiempos de respuesta y precios dados PCBway se considera una de las mejores opciones, adem谩s, siendo el 煤nico que entrega un detalle completo de los precios de cada uno de los componentes. Otro fabricante a considerar es EEcart.

### Programaci贸n
HAblando del software del dispositivo nodo sensor se poseen 2 versiones  con y sin SD para su funcionamiento, estos posee las siguentes caracteristicas:
1. Posee variables de los per铆odos de medida y envv铆o de datos:Es una de las caracter铆sticas mas importantes para la definici贸n de tiempos de funcinamniento del sistema. La variabble Freq_sens indica cada cuantos segundos tomada una medida de los sensores y la variable freq_send representa el intervalo en segundos en el que son enviados los datos, claramente Freq_send> freq_sens ya que deben existir datos medidos para ser enviados.
2. Guarda los datos en un buffer (arreglo): Los datos medidos, es decir, sensor, mediida y tiempo de medida en cada sensor son codificados (explicado m谩s adelante) en bytes, y guardados en un buffer(arreglo) de 512 bytes en la SD o  utilizando la memoria del microcontrolador dependiendo de versi贸n. Para el caso de la sd cuando el arrreglo esta lleno guarda los datos en archivos binarios dentro de la tarjeta SD y los envia junto a los valores del arrglo cuando sea el tiempo de enviado. Si es la versi贸n sin sd no se posee m谩s memoria que la del arreglo por lo que esta limitado a medir una cantidad maxima de datos antes de enviar, por lo que la freq_send tiene esta limitante.
3. Los datos guardados son coidificados: Para realizar un env铆o m谩s eficiente ya sea por velocidad o disminuci贸n de consumo energ茅tico en el momento de enviar datos se desarroll贸 una librer铆a para ello. Lo importtante a destacar m谩s que la programaci贸n de este es la forma de codificaci贸n que existe que puede ser de 3 maneras:
* Codificiaci贸n base:
* COdificacion diferencial:
* COdificacion aaa
4. Los datos son envidos mediante transmisi贸n serial RS485  como paquetes de bytes: como los datos son codificacods a bytes estos son enviados de esta manera en paquetes de bytes, la comunicaci贸n RS485 es simplemente para tener mayor alcance como se dijo anteriormente.


C贸digo completo:
El primero es el codigo completo que utiliza la sd para el guardado de los datos, el codigo esta centro

Ejemplos del funcionamiento de medidas:



## Roadmap
backlog
pasos futuros

| N  | T铆tulo                                         | Detalle                                                                                                                                                                                                                                                                                                                                                                                                      |
| -- | ---------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| 1  | Mover uSD a superficie                         | Hacer que la uSD sea controlada y alimentada desde el nodo de comunicaciones en vez del nodo sensor.                                                                                                                                                                                                                                                                                                         |
| 2  | Bajar ciclos del oscilador a 8Mhz              | Disminuir ciclos del oscilador de 16MHz a 8MHz. Esto disminuye la velocidad a la que opera el sistema sin afectar el funcionamiento de los programas. Funcionando a la mitad de ciclos se espera una disminuci贸n del consumo del procesador en el sistema.                                                                                                                                                   |
| 3  | Ocupar VCC 3.3V                                | Bajar alimentaci贸n del sistema de 5V a 3.3V. Se debe prototipar y validar el funcionamiento de componentes y electr贸nica. Con este cambio disminuye el consumo general de energ铆a del sistema obteniendo mayor desempe帽o de estados de deep-sleep.                                                                                                                                                           |
| 4  | Amplificador universal multiplexado            | Si se caracterizan debidamente las sondas y se verifica que el procesamiento de los circuitos intermediarios se pueden realizar de forma digital, una opci贸n es tener un amplificador para todas las sondas, las cuales mediante multiplexi贸n temporal entren a 茅ste (opcionalmente un digipot puede ayudar a modificar la ganancia). Esto podr铆a reducir dr谩sticamente la cantidad de componentes en placa. |
|    | Integrados de carga de bater铆as en paralelo    |                                                                                                                                                                                                                                                                                                                                                                                                              |
| 5  | Autonom铆a de sensores (drift)                  | Si se va a aumentar la autonom铆a del sistema, es necesario verificar si en ese horizonte de tiempo los sensores ser谩n funcionales.                                                                                                                                                                                                                                                                           |
| 8  | Optimizaci贸n de componentes                    | Relacionado con los puntos 3 y 4, hay que repasar toda la selecci贸n de componentes en t茅rminos de funciones y equipos. Tambi茅n se relaciona con la programaci贸n.                                                                                                                                                                                                                                             |
|    |                                                |                                                                                                                                                                                                                                                                                                                                                                                                              |
| 6  | Autonom铆a energ茅tica (solar, electr贸nica)      | A帽adir un sistema de carga solar para recargar las bater铆as 18650 del nodo sensor podr铆a en pr谩cticamente cualquier caso mejorar la autonom铆a.                                                                                                                                                                                                                                                               |
| 7  | Bater铆a de auto                                | Colocar una bater铆a de auto para todo el sistema te贸ricamente asegurar铆a una mayor autonom铆a.                                                                                                                                                                                                                                                                                                                |
| 9  | Programar nodo a distancia                     | \- Se podr铆a cambiar el atmega por un esp que se programe a distancia.                                                                                                                                                                                                                                                                                                                                       |
| 10 | Switch magn茅tico de encendido                  | Se puede agregar un switching on/off del sistema que se puede activar desde fuera de la carcasa con un im谩n para de esta manera poder ahorrar energ铆a cuando no se est茅 utilizando el dispositivo.                                                                                                                                                                                                           |
| 11 | Modularizar datalogger de adaptadores sensores | Separar en placas separadas, pero conectables el datalogger (uC, RTC, SD, energ铆a) de electr贸nica de amplificaci贸n de los sensores dfrobot (pH, turbidez, conductividad)                                                                                                                                                                                                                                     |