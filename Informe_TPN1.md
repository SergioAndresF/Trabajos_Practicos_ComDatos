# Trabajo Práctico N°1

### Asignatura: Comunicaciones de Datos

**Facultad de Ciencias Exactas, Físicas y Naturales (UNC)**

---

* **Grupo:** Group Not Found :(
* **Profesores:** Miguel Angel Solinas y Santiago Martin Henn

---

### Integrante y Contacto

| Nombre y Apellido | Correo Electrónico |
| :--- | :--- |
| **Sergio Andrés Fernández Segovia** | _sergio.fernandez.segovia@mi.unc.edu.ar_ |

---

## Introducción

En el presente informe se documenta el desarrollo y la resolución del Trabajo Práctico N°1 de la asignatura Comunicaciones de Datos. El trabajo está estructurado en cuatro consignas principales, cuyo objetivo es repasar y aplicar conceptos fundamentales relacionados con la transmisión de información, estableciendo un vínculo entre los fenómenos físicos involucrados y su implementación práctica en sistemas de comunicaciones.

A lo largo del documento, se aborda inicialmente el marco teórico necesario para el desarrollo del trabajo práctico, en el que se analiza la propagación de ondas electromagnéticas, la clasificación del espectro electromagnético y los conceptos de atenuación. Posteriormente, el análisis se centra en las señales digitales, los distintos modos de transmisión y las técnicas de modulación digital. Finalmente, la última etapa del trabajo tiene como objetivo aplicar estos principios físicos mediante Cisco Packet Tracer, donde se implementa una red inalámbrica, se configuran los dispositivos, se verifica su conectividad y se analiza el comportamiento del enlace en función de la ubicación de los equipos.

---

## Consignas

### Consigna N°1: 
Repasar y resumir brevemente los fundamentos básicos y esenciales al respecto de: Ondas Electromagnéticas, Modulación/Demodulación, Señales de tiempo continuo, Señales de tiempo discreto.
> - **Ondas Electromagnéticas:** Es una onda de campo electromagnético que se propaga a través del espacio vacío o de un medio material transportando energía. Está formada por dos componentes perpendiculares entre sí: un campo eléctrico y un campo magnético. Ambos campos varían en el tiempo y en el espacio.
> Están caracterizadas por los siguientes parámetros: Amplitud, Frecuencia y Longitud de Onda.
> 
> - **Modulación y Demodulación:** La **modulación** es el proceso a través del cual se modifica una o más características (amplitud, frecuencia o fase) de una señal periódica de alta frecuencia a la que se denomina portadora, con el objetivo de transmitir información. La **demodulación**, por su parte, es el proceso inverso, que consiste en recuperar la información de la señal modulada. 
> Estos procesos son fundamentales en las comunicaciones, permitiendo la transmisión eficaz de datos a través de diferentes medios.
> 
> - **Señales de Tiempo Continuo:** Estas señales se caracterizan por estar definidas para cualquier instante de tiempo dentro de un intervalo dado. Se representan como una función $x(t)$, donde $t$ pertenece al conjunto de los números reales. Esto significa que su amplitud varía de manera continua en el tiempo.
> 
> - **Señales de Tiempo Discreto:** Son señales que están definidas únicamente para determinados instantes de tiempo, los cuales se representan habitualmente mediante una secuencia $x[n]$, siendo $n$ un número entero. Esto significa que la señal está definida únicamente en determinados instantes de tiempo. Cabe aclarar que una señal de tiempo discreto no necesariamente tiene amplitudes discretas.


Luego responder las consignas a continuación:
<center>
    <img src="https://hackmd.io/_uploads/HkO9Ix4vzl.png" width="1000">
    <br>
    <em>Figura 1: Onda.</em>
</center>

**a.** ¿Qué frecuencia y longitud de onda tiene esta onda?. Considerar que viaja exactamente a la velocidad de la luz *c* ?

> Teniendo en cuenta que la **longitud de onda** se define como la distancia que ocupa un ciclo o, dicho de otra manera, como la distancia entre dos puntos de igual fase en dos ciclos consecutivos, se puede observar que, para la onda mostrada, se tiene una longitud de onda de $60\space [mm]$ o $6 \space[cm]$.
>
> Por otro lado, se conoce la velocidad de propagación de esta onda que, en este caso, coincide con la velocidad de la luz ($3 \cdot 10^8 \space[\frac{m}{s}]$), por lo tanto, se puede determinar la **frecuencia** asociada a la misma a través de la **ecuación de onda**:

$$c = \lambda \cdot f$$ 

> Despejando la frecuencia y, posteriormente, reemplazando los parámetros por los valores conocidos se obtiene el siguiente resultado:

$$f=\frac{c}{λ} = \frac{3 \cdot 10^8 \space [\frac{m}{s}]}{60 \cdot 10^{-3}\space [m]} = 5 \cdot 10^9 \space [Hz] = 5 \space [GHz]$$


**b.** El espectro EM está dividido en **regiones** y **bandas**. Investigar y mencionar en qué región del espectro opera esta onda, y más precisamente, en qué banda.

> El **espectro electromagnético** es la gama completa de la radiación electromagnética e incluye todas las formas de energía que viajan como ondas o partículas a través del espacio, abarcando una amplia gama de longitudes de onda y frecuencias. En ese sentido, existen varias **regiones** o **porciones**, cada una con sus propias características y aplicaciones. 
>
> Estas **regiones** incluyen las ondas de radio, las microondas, la radiación infrarroja, la luz visible, la radiación ultravioleta, los rayos X y los rayos gamma. En la siguiente figura se muestra el **rango específico de frecuencias** que define a cada región.

<center>
    <img src="https://hackmd.io/_uploads/HkKkLphPzx.png" width="700">
    <br>
    <em>Figura 2: Regiones de Frecuencia.</em>
</center>

> Por otro lado, cuando se habla de las **bandas** del espectro EM, se tiene presente a la **ITU (International Telecommunication Union)**. Se trata de una agencia de las Naciones Unidas que ayuda a los países a coordinar cómo se utiliza el espectro radioeléctrico para las comunicaciones en todo el mundo. Para ello, la **ITU** especifica una forma de dividir todo el espectro EM basado en las longitudes de onda. 
>
> A continuación, se muestra la **clasificación oficial** establecida en la **Recomendación UIT-R V.431**, junto con las principales aplicaciones de cada una de las bandas en el ámbito de las comunicaciones.

<center>
    <img src="https://hackmd.io/_uploads/BJTVVT3vzg.png" width="750">
    <br>
    <em>Figura 3: Bandas de Frecuencia.</em>
</center>

> Habiendo revisado estos conceptos, para **clasificar la onda bajo estudio**, cuya frecuencia es de $5 \space[GHz]$, se llega a lo siguiente:
> 
> - La onda opera dentro de la **región** del espectro correspondiente a la **Radiofrecuencia**, ubicándose específicamente en el rango de las **Microondas**. 
> - Con respecto a su estandarización regulatoria y siguiendo la **clasificación oficial de la Recomendación UIT-R V.431**, esta frecuencia opera en la **Banda 10**, denominada **SHF (Super High Frequency)**. Cabe destacar que la subdivisión métrica de la ITU para esta banda es la de **"ondas centimétricas"**, lo cual se verifica de forma analítica al haber calculado una longitud de onda de $6 \space[cm]$ en el inciso anterior.

**c.** Investigar qué dispositivos para comunicaciones de datos operan en esta banda y brindar al menos un ejemplo.

> De acuerdo con el cuadro presentado anteriormente, el **uso típico** que se da a esta banda se encuentra en las comunicaciones satelitales, radares, enlaces de microondas terrestres y bucles locales inalámbricos.
>
> Como **ejemplos concretos** de dispositivos que operan en esta banda, se pueden mencionar los **routers inalámbricos**, como los que operan en $5 \space[GHz]$ bajo el estándar 802.11ac/ax para redes WLAN y las **antenas terminales VSAT** utilizadas para recibir internet satelital.

<center>
  <img src="https://hackmd.io/_uploads/HkQs-RhPzl.png" width="200">
  <br>
  <em>Figura 4: Router inalámbrico Linksys WRT300N.</em>
</center>

<center>
  <img src="https://hackmd.io/_uploads/H11Nb03vMx.png" width="250">
  <br>
  <em>Figura 5: Vista lateral y componentes estructurales de una antena terminal VSAT.</em>
</center>

**d.** ¿Qué fenómeno se quiere representar con la línea de trazos roja en la figura de la onda?

> El fenómeno mostrado representa la **atenuación** de la onda. Esto consiste en la **pérdida paulatina de energía** de la señal a medida que se propaga hacia su destino. Dicha pérdida de energía se evidencia claramente como una **disminución de la amplitud o intensidad** de la onda.

**e.** El fenómeno descrito en el ítem anterior, ¿afecta al dispositivo que diste de ejemplo? ¿Podés notar esto en alguna experiencia de la vida cotidiana?

> - En el caso del **router inalámbrico**, la señal pierde energía a medida que viaja por el aire y también, de manera aún más severa, cuando debe atravesar varios obstáculos físicos tales como paredes, techos o muebles, debido a que éstos pueden reflejar o absorber parcial o fuertemente la señal. En ese sentido, cuantos más obstáculos, peor será la señal.
> 
> - En el caso de la **antena VSAT**, las ondas sufren atenuación al atravesar la atmósfera terrestre, siendo sensibles a la absorción por el vapor de agua y a la dispersión causada por las gotas de lluvia (rain fade).
>
> En lo que respecta a la vida cotidiana, se puede experimentar a diario el caso de la **red Wi-Fi (router)**. Al **alejarse físicamente** del router ya sea, desplazándose hacia otra habitación o al exterior de la vivienda, en el dispositivo que, puede ser un teléfono móvil o bien un computador, se logra observar una **disminución visual** en el indicador de intensidad de la señal, lo que se traduce en una **menor velocidad de transferencia de datos** o, en caso de que la atenuación sea total, en la **pérdida de la conexión.**

**f.**  El fenómeno descrito anteriormente:
  - ¿Afecta a las transmisiones de telefonía celular?
  > Efectivamente, son afectadas debido a que las ondas sufren atenuación por el **espacio libre**, por las **condiciones atmosféricas** y por **obstáculos urbanos**, como por ejemplo, los edificios y la vegetación. Esto provoca la **pérdida de conectividad** en rutas alejadas o en subsuelos donde los materiales absorben la onda.
  - ¿Afecta a las transmisiones por cable coaxial?
  > Sí existe atenuación en cable coaxial y puede ocurrir por las siguientes causas: 
  > 
  > - Radiación fuera del cable debido a un blindaje imperfecto.
  > - Pérdidas resistivas en los conductores del cable.
  > - Absorción de señal en el dieléctrico del cable.
  > - Reflexiones producidas por desadaptaciones de impedancia entre el cable y las terminaciones, o por discontinuidades a lo largo del enlace.
  >
  > En aplicaciones de banda ancha, la atenuación aumenta con la longitud del enlace y con la frecuencia de operación, por lo que en determinadas aplicaciones resulta necesario incorporar elementos de compensación o regeneración de la señal con la finalidad de evitar una disminución del rendimiento.

  - ¿Afecta a las transmisiones por fibra óptica?
  > De igual manera, se produce una pérdida de señal por fibra óptica.
  >  Entre los factores se puede mencionar:
  >  - Absorción de energía luminosa dentro del material de la fibra.
  >  - Dispersión causada por imperfecciones microscópicas en el vidrio.
  >  - Pérdidas por flexión resultantes de un enrutamiento de cables inadecuado.
  >  - Pérdidas por conectores y empalmes en los puntos de conexión.
  >  - Influencias ambientales como el estrés, los cambios de temperatura y la contaminación.
  >  
  > Sin embargo, la fibra óptica es **inmune a las interferencias electromagnéticas** y presenta una atenuación de la señal considerablemente menor en comparación a otros medios guiados. Estas características la convierten en el medio de transmisión guiado a larga distancia preferido, especialmente para los enlaces transoceánicos.
 
---

### Consigna N°2: 
Comunicar datos a través de cualquier medio es, en esencia, un proceso que consiste en modificar el comportamiento de una señal en el tiempo. En esta materia nos concentramos en la transmisión de datos, hoy por hoy, dominado por las señales digitales. Analicemos el siguiente sistema:

<center>
  <img src="https://hackmd.io/_uploads/H1CQ1M_wfx.png" width="700">
  <br>
  <em>Figura 6: Esquema de Transmisión de Datos.</em>
</center>

**a.** Según su direccionalidad y características temporales, ¿qué tipo y modo de transmisión se quieren representar?

> Para este inciso, resulta conveniente recordar que, en términos de **direccionalidad**, la **transmisión de datos** puede ser:
> - **Simplex:** Las señales se transmiten sólo en una única dirección. En ese sentido, se constituye una estación emisora y otra receptora.
> - **Half-duplex:** Ambas estaciones tienen la capacidad de transmitir, pero no de manera simultánea. 
> - **Full-duplex:** A diferencia del caso anterior, ambas estaciones pueden transmitir y recibir simultáneamente. Además, en este caso, el medio transporta señales en ambos sentidos al mismo tiempo.

<center>
  <img src="https://hackmd.io/_uploads/Bk9olCTPze.png" width="700">
  <br>
  <em>Figura 7: Transmisión de Datos en función de Direccionalidad.</em>
</center>

> Con respecto a las **características temporales** y la sincronización, se distingue:
> - **Asíncrona:** Los datos se transmiten en pequeños bloques independientes, generalmente byte por byte. En este caso, **no existe una señal de reloj compartida** entre los dispositivos; en su lugar, la sincronización se logra añadiendo **bits de inicio y de parada** a la trama.
> 
 <center>
  <img src="https://hackmd.io/_uploads/ryvNGAawfe.png" width="400">
  <br>
  <em>Figura 8: Transmisión Asíncrona.</em>
</center>

> - **Síncrona:** Los datos se transmiten utilizando una base de tiempo común entre emisor y receptor. Esto permite que el receptor logre determinar de manera precisa los instantes en los que debe muestrear los datos. Esta sincronización puede establecerse mediante una señal de reloj compartida o mediante mecanismos de recuperación de reloj a partir de la propia señal de datos.

<center>
  <img src="https://hackmd.io/_uploads/r1d7M0awzg.png" width="550">
  <br>
  <em>Figura 9: Transmisión Síncrona.</em>
</center>

> Una vez repasados estos conceptos, se procede a **clasificar la transmisión** propuesta en el esquema, el cual ilustra una transmisión de **tipo Simplex y de modo Síncrono**.  
> - Es **Simplex** debido a que el flujo de datos se produce en un único sentido. Esto se ve evidenciado por la flecha unidireccional en la línea superior de comunicación. 
> 
> - Es **Síncrona** porque se puede observar que existe una línea adicional inferior, la cual está dedicada exclusivamente a transmitir una señal de reloj constante entre ambos módulos, asegurando así una base de tiempo común.

**b.** ¿Es este el mejor paradigma si busco transmitir datos rápidamente y de forma bidireccional?

> El esquema presentado no es el adecuado para cumplir con esos requerimientos por los siguientes motivos:
> - El diagrama ilustra un canal **estrictamente unidireccional**, por lo tanto, la transmisión de datos se encuentra limitada a un único sentido de transmisión. Si se desea lograr una comunicación bidireccional rápida y eficiente, el paradigma a seguir es el **Full-duplex** debido a que permite a ambas estaciones transmitir y recibir simultáneamente sin colisiones.
> 
> - El sistema utiliza una **línea de reloj** separada de la línea de datos. Si bien esta arquitectura permite una sincronización sencilla entre emisor y receptor, requiere un canal adicional para distribuir la referencia temporal. En sistemas de comunicación de alta velocidad pueden utilizarse técnicas de sincronización más eficientes, como la recuperación de reloj a partir de la propia señal de datos, evitando la necesidad de transmitir una línea de reloj independiente.

**c.** En la expresión más simple de señal digital, podemos pensar que un nivel de tensión “1” representa un 1 digital, y un nivel de tensión “0” representa un 0 digital. Con esto en mente, analicemos el siguiente gráfico, que podría representar un tipo de comunicación UART:

<center>
  <img src="https://hackmd.io/_uploads/SkLOkfdvGg.png" width="700">
  <br>
  <em>Figura 10: Transmisión del byte "00100011".</em>
</center>

En este caso estamos representando la transmisión del siguiente byte: “00100011”, que en codificación ASCII representa el símbolo “#”. Si quisiéramos transmitir la **4ta letra** del nombre de tu grupo, ¿Cómo se vería la señal?

> El nombre del grupo es **"Group Not Found :("** donde la 4ta letra corresponde a la letra **"u"**. De acuerdo con la **codificación ASCII**, el byte que representa a este símbolo y que se debe transmitir es **"01110101"**. 

<center>
  <img src="https://hackmd.io/_uploads/SJU9wBTwGx.png" width="700">
  <br>
  <em>Figura 11: Transmisión del byte "01110101".</em>
</center>

**d.** Dada la pendiente en los niveles de tensión que podemos ver indicada con flechas en el gráfico de ejemplo. ¿En qué marcas temporales medirían la señal para determinar el valor digital de la misma?

> En el ejemplo se puede observar que se tienen **marcas temporales** tanto en "medio" de un dato como en los instantes en los que se produce la transición entre los valores discretos. Teniendo en cuenta este comportamiento, se pueden evaluar los posibles momentos de medición:
>
> - **En los límites del intervalo temporal:** Si se tomara una muestra donde ocurre la transición, el valor de tensión leído resultaría ambiguo o intermedio, lo que podría generar un error en la interpretación del valor digital.
> 
> - **En el centro del intervalo temporal:** En este caso la transición ha finalizado y la señal se encuentra aproximadamente estabilizada en su nivel lógico correspondiente, ya sea alto o bajo. Por lo tanto, para determinar el valor digital de la señal garantizando una lectura confiable, la medición debe realizarse en las marcas temporales correspondientes al centro del intervalo temporal.

---

### Consigna N°3: 
Investigar y resumir brevemente los motivos por los cuales no es conveniente transmitir de manera inalámbrica una señal escalonada, como las que vimos en los ejemplos.

> Los motivos están bastante relacionados con la **atenuación** y la **respuesta del medio a las diferentes frecuencias**. Para notar ese efecto, resulta conveniente imaginar a la señal no como una simple forma de onda, sino como una **serie de componentes de Fourier**, donde las distintas componentes pueden experimentar diferentes niveles de atenuación y desplazamientos de fase, dando como resultado una señal distorsionada en el receptor. En aquellos medios que presentan dispersión, las diferentes componentes de frecuencia pueden propagarse a distintas velocidades, produciendo una **distorsión** de la señal que se recibe en el otro extremo.
>
> Debido a estos inconvenientes, **puede resultar problemático transmitir directamente una señal con un rango amplio de frecuencias**, como ocurre con las **ondas cuadradas**. En consecuencia, las diferentes componentes espectrales pueden experimentar distintos niveles de atenuación y fase, provocando **distorsión** de la señal en el receptor. Por este motivo, en sistemas inalámbricos se emplean técnicas de modulación que permiten adaptar la señal al canal de transmisión y utilizar una banda de frecuencias adecuada.

Con esto en mente, analizar el siguiente gráfico de ejemplo y responder las preguntas a continuación.

<center>
  <img src="https://hackmd.io/_uploads/BJxkvy6wMl.png" width="700">
  <br>
  <em>Figura 12: Técnica de Modulación.</em>
</center>

**a.** ¿Qué técnica de modulación se está representando?

> Se puede observar que la señal mantiene constante su amplitud y frecuencia, pero experimenta una inversión en su fase cada que se produce la transición entre los niveles lógicos. Por lo tanto, se trata de la **Modulación por Desplazamiento de Fase (PSK)**, una técnica de modulación digital que consiste en modificar la fase de la señal portadora entre un número de valores discretos.
>
> Particularmente, la figura muestra un ejemplo del sistema más simple, conocido como **desplazamiento de fase binario (BPSK)**, que utiliza dos fases para representar los dos dígitos binarios. En ese sentido, se utilizan dos estados de fase separados 180°, y cada estado se asigna a uno de los dos valores binarios dependiendo de la convención de mapeo adoptada.

**b.** ¿Cómo se vería la siguiente señal digital modulada?

<center>
  <img src="https://hackmd.io/_uploads/H1OXCl6wGg.png" width="700">
  <br>
  <em>Figura 13: Modulación del byte "01110110".</em>
</center>

**c.** ¿Qué otras técnicas de modulación basadas en los mismos principios existen?

> Dado que en el inciso anterior se abordó la modificación de la fase, las otras técnicas fundamentales que alteran los parámetros restantes son:
> - **Amplitude Shift Keying (ASK):** Modula la amplitud de la señal portadora para representar datos binarios. Las variaciones de amplitud significan diferentes estados digitales (0 y 1). Por ejemplo, si se transmite 1 bit: la señal se emite cuando la información a transmitir es un 1 y no se emite cuando lo que se quiere transmitir es un 0.
> 
> - **Frequency Shift Keying (FSK):** Altera la frecuencia de la señal portadora para transmitir información digital. Utiliza diferentes frecuencias para representar valores binarios, y cada frecuencia denota un estado digital específico. Por ejemplo, si se transmite 1 bit: se usa una frecuencia de la portadora para indicar que la información transmitida es un 0 y otra frecuencia diferente para indicar que el bit transmitido es un 1.

<center>
  <img src="https://hackmd.io/_uploads/SJAArM0wfg.png" width="350">
  <br>
  <em>Figura 14: Técnicas de Modulación: ASK y FSK.</em>
</center>

**d.** ¿Qué es el Bit Error Rate (BER)?. En términos de BER, ¿Cuál de las técnicas de modulación presentadas anteriormente tiene mejores prestaciones?

> El **Bit Error Rate (BER)** es una medida de la cantidad de bits recibidos incorrectamente respecto del total de bits transmitidos durante un intervalo determinado. Por lo tanto, permite evaluar el desempeño y la confiabilidad de un sistema de comunicación.

$$BER = \frac{N°\space de \space bits \space erroneos}{N°\space de \space bits \space transmitidos} $$

> Una BER más **baja** indica una mayor calidad de transmisión y fiabilidad del canal, mientras que una BER **alta** sugiere interferencia, ruido o distorsión, lo que provoca retransmisiones de datos y reduce la velocidad efectiva.
>
> Teniendo en cuenta esto, se procede a evaluar las técnicas de modulación mencionadas en el inciso anterior:
> 
> - **ASK:** El ruido afecta directamente a la amplitud de la señal. Por lo tanto, la información es altamente susceptible al ruido y a las interferencias, recordando que, para esta técnica, los datos se transportan modificando la amplitud de la señal portadora.
> 
> - **FSK:** La información se representa mediante diferentes frecuencias de la señal portadora. En determinadas condiciones de ruido, este esquema puede presentar una mayor robustez que ASK, ya que la información no depende directamente del nivel de amplitud recibido.
> 
> - **PSK:** La información se codifica mediante diferentes estados de fase de la señal portadora. En particular, BPSK utiliza dos fases separadas 180°, lo que proporciona una separación significativa entre los dos estados de señal y permite obtener un buen desempeño frente al ruido. Bajo condiciones equivalentes de canal y relación señal-ruido, BPSK presenta una BER particularmente baja.
---

### Consigna N°4: 

A continuación instalaremos y construiremos una red simple en Packet Tracer. Incluiremos dos computadoras y un router siguiendo el siguiente esquema:

<center>
  <img src="https://hackmd.io/_uploads/r1CaFyAPGe.png" width="400">
  <br>
  <em>Figura 15: Esquema: Computadoras y Router.</em>
</center>

**a.** Colocar un router inalámbrico, que se encuentra bajo network-devices > wireless-devices

<center>
  <img src="https://hackmd.io/_uploads/BJInqkCwzl.png" width="150">
  <br>
    <em>Figura 16: Router Inalámbrico WRT300N.</em>
</center>

**b.** Configurar el router, haciendo click sobre el mismo y desplegando sus opciones, de tal manera que la dirección de IP sea 192.168.0.1 y la máscara de subred 255.255.255.0. Pongan un nombre que les guste (SSID) a la red, y configuren la seguridad wireless para operar con autenticación WPA2-PSK con una contraseña de al menos 8 dígitos.

<center>
  <img src="https://hackmd.io/_uploads/BkhM21CvMx.png" width="250">
  <br>   <em>Figura 17: LAN Settings.</em>
</center>

<center>
  <img src="https://hackmd.io/_uploads/S13ZkeCwMg.png" width="300">
  <br>   <em>Figura 18: Wireless Settings.</em>
</center>

<center>
  <img src="https://hackmd.io/_uploads/Syvca10wGx.png" width="400">
  <br>   <em>Figura 19: Seguridad Wireless.</em>
</center>


**c.** Analizar las configuraciones del router y responder: ¿En qué frecuencia opera? ¿A qué región del espectro electromagnético corresponde? ¿En qué banda opera?

> De acuerdo a la figura correspondiente a **Wireless Settings**, el router opera a una frecuencia de $2.412 [GHz]$. Revisando nuevamente la Figura 2 y la Figura 3 de la Consigna N°1, esta frecuencia se encuentra dentro de la región de las **Microondas** y opera en la **Banda 9**, denominada **UHF (Ultra High Frequency)**. 
>
> Asimismo, la subdivisión métrica de la ITU para esta banda es la de **"ondas decimétricas"**.
> 
<center>
  <img src="https://hackmd.io/_uploads/r1S6SlRPfe.png" width="700">
  <br>   <em>Figura 20: Tabla de Bandas de Frecuencias.</em>
</center>

**d.** Colocar una computadora de escritorio (ubicada en la sección End Devices) y conectarla al router. Utilizar un cable “copper straight-through”, ubicado en el menú de conexiones (ícono del rayo). En las configuraciones de la computadora asegurarse de que la placa de red (interfaces -> FastEthernet) esté configurada para adquirir direcciones de manera automática (DHCP).

<center>
  <img src="https://hackmd.io/_uploads/ryBVVrCDzx.png" width="450">
  <br>   <em>Figura 21: Configuración IP: Computadora.</em>
</center>

<center>
  <img src="https://hackmd.io/_uploads/rJ8BNS0PGg.pngg" width="250">
  <br>   <em>Figura 22: Conexión Router-Computadora.</em>
</center>

**e.** Conectaremos ahora la notebook. Primero debemos asegurarnos que la misma tenga una NIC Wi-Fi. En la pestaña principal de la PC, quizás debamos retirar la placa que tenga en la ranura de expansión y colocar una placa Wi-Fi:

<center>
  <img src="https://hackmd.io/_uploads/S1WdSB0vze.png" width="300">
  <br>   <em>Figura 23: Portátil con placa Wi-Fi.</em>
</center>

**f.** Luego podremos configurar la red. Para ello, ingresar a la misma y en la solapa “desktop” (al lado de config) seleccionar PC Wireless. En la solapa connect podremos buscar la red inalámbrica que configuramos en el punto b) y conectarnos a ella. Deberíamos ver que aparece un link entre el router y la notebook, representando la conexión inalámbrica.

<center>
  <img src="https://hackmd.io/_uploads/BJ82IB0wzg.png" width="600">
  <br>   <em>Figura 24: Conexión Router-Portátil.</em>
</center>

**g.** Explorar las interfaces en ambas computadoras, y comprobar que existe conectividad entre ellas. Por ejemplo utilizar pings o trace routes, tomando nota de la IP de cada computadora. Documentar los resultados.

<center>
  <img src="https://hackmd.io/_uploads/HJ1TsH0wGe.png" width="800">
  <br>   <em>Figura 25: Verificación de Conectividad: Computadora y Portátil.</em>
</center>

**h.** Una vez comprobada la conexión, cambiaremos la vista a “física”. Y navegaremos hacia la región cerca de la “oficina” donde tenemos nuestro setup. Deberíamos ver una representación de la señal Wi-Fi y los límites de la misma. Colocar una notebook, conectarla a la red wifi, y probar la conexión con alguna computadora dentro de la oficina desde las posiciones que se muestran a continuación. Documentar los resultados y elaborar conclusiones acerca de lo medido.

> Primeramente, se posiciona la portátil dentro del área violeta pero lo más cercano al borde. De acuerdo con el fenómeno de la atenuación estudiado en las consignas anteriores, es de esperar que la intensidad de señal en este punto sea baja.
> 
> Efectivamente, se puede observar que el indicador de intensidad de la señal cayó a un 2%, confirmando el análisis realizado. 

<center>
  <img src="https://hackmd.io/_uploads/Sk7PCYAPMe.png" width="800">
  <br>   <em>Figura 26: Portátil dentro del área.</em>
</center>

> Sin embargo, pese a que la señal disminuyó, la portátil continúa estando conectada a la red. Esto se evidencia aplicando el comando ping desde la portátil hacia la dirección IP de la computadora.
> 
<center>
  <img src="https://hackmd.io/_uploads/SyGlycAwMe.png" width="400">
  <br>   <em>Figura 27: Verificación de Conectividad: Computadora-Portátil.</em>
</center>

> La siguiente situación implica ubicar la portátil fuera del área violeta y lo que se puede anticipar es que la señal recibida, para este punto, sea suficientemente baja como para que el enlace deje de ser viable.
>
> Como se puede apreciar en la siguiente figura, la red no logra ser reconocida por la portátil, por lo tanto, se perdió la conectividad.

<center>
  <img src="https://hackmd.io/_uploads/SylsRFAwzl.png" width="800">
  <br>   <em>Figura 28: Portátil fuera del área.</em>
</center>

> A fin de corroborar lo anterior, nuevamente, se realiza el comando ping hacia la dirección IP de la computadora, obteniéndose lo siguiente. En consecuencia, no es posible establecer comunicación IP entre la computadora y la portátil desde esta ubicación.

<center>
  <img src="https://hackmd.io/_uploads/HyqHJ90wfg.png" width="400">
  <br>   <em>Figura 29: Verificación de Pérdida de Conectividad: Computadora-Portátil.</em>
</center>

> En conclusión, durante la simulación se ha podido evidenciar que la conectividad inalámbrica no depende únicamente de la configuración lógica de la red, sino que, al aumentar la distancia respecto del punto de acceso, la potencia de señal recibida disminuye y, finalmente, el enlace deja de ser viable. Este comportamiento es consistente con la atenuación de la potencia recibida durante la propagación.

---

## Conclusiones

La realización de este trabajo práctico permitió relacionar distintos conceptos fundamentales de las Comunicaciones de Datos, partiendo desde los fenómenos físicos asociados a la propagación de señales hasta su aplicación en una red inalámbrica simulada. El análisis de la onda electromagnética de la Consigna N°1, permitió vincular la longitud de onda y la frecuencia con su ubicación dentro del espectro electromagnético y, a su vez, con las aplicaciones correspondientes en sistemas de comunicaciones.

Con respecto a las Consigna N°2 y N°3, el estudio de las señales digitales y de los modos de transmisión permitió comprender la importancia de la sincronización, la correcta interpretación temporal de los niveles lógicos y la elección de una técnica de modulación adecuada para transmitir información. En particular, el análisis de BPSK, ASK y FSK permitió observar que las características de la modulación influyen directamente en el comportamiento de la transmisión frente al ruido y, por lo tanto, en la tasa de errores de bit.

Por último, la Consigna N°4, que implicaba la implementación realizada en Cisco Packet Tracer permitió comprobar experimentalmente algunos de los conceptos estudiados. La configuración de la red, la asignación de direcciones IP y las pruebas de conectividad permitieron verificar el funcionamiento del enlace, mientras que la modificación de la posición de los dispositivos mostró cómo la distancia y las condiciones de propagación pueden afectar la comunicación inalámbrica. De esta manera, el trabajo permitió vincular los conceptos teóricos estudiados con su comportamiento observable en un entorno práctico.

---

## Referencias
- Stallings, W. (2004). Comunicaciones y redes de computadores (7.ª ed.). Pearson Prentice Hall.
- Tanenbaum, A. S., & Wetherall, D. J. (2012). Redes de computadoras (5.ª ed.). Pearson Educación.
- Kurose, J. F., & Ross, K. W. (2017). Redes de computadoras: Un enfoque descendente (7ma ed.). Pearson Educación.
- Bird. (s.f.). ITU Frequency Bands. Recuperado de: https://birdrf.com/blog/itu-frequency-bands
- Rayzeek. (s.f.). ¿Qué es el espectro electromagnético?. Recuperado de: https://www.rayzeek.com/es/glosario/que-es-el-espectro-electromagnetico/
- Scribd. (s.f.). Modos de transmisión. Recuperado de: https://es.scribd.com/document/98246911/Modos-de-transmision
- SlideShare. (s.f.). Transmisión síncrona y asíncrona. Recuperado de: https://es.slideshare.net/slideshow/transmision-sincrona-yasincrona/4986393
- SlideShare. (s.f.). Modulación PSK. Recuperado de: https://es.slideshare.net/slideshow/modulacion-psk/12507087#11
- Tutorials Point. (s.f.). Digital Communication - Phase Shift Keying. Recuperado de: https://www.tutorialspoint.com/digital_communication/digital_communication_phase_shift_keying.htm
- Rahsoft. (2023). Analog and Digital Modulation Techniques. Recuperado de: https://rahsoft.com/2023/11/26/analog-and-digital-modulation-techniques/
- Jorge Canon. (s.f.). Técnicas de modulación digital. Recuperado de: https://jorgecanon.com/tecnicas-de-modulacion-digital/
- Salim Wireless. (2024). BASK, BFSK: Theoretical BER vs SNR. Recuperado de: https://www.salimwireless.com/2024/08/bask-bfsk-theoretical-ber-vs-snr.html
- Broadband Library. (s.f.). Coaxial Cable Attenuation. Recuperado de: https://broadbandlibrary.com/coaxial-cable-attenuation/
- L-P Knowledge Center. (s.f.). Atenuación en fibra óptica. Recuperado de: https://www.l-p.com/es/blog/knowledge-center/attenuation-in-fiber-optics.htm
- Wavlink Blog. (s.f.). Technical News / Connectivity. Recuperado de: https://blog.wavlink.com/en-us/article/TechnicalNews/92442c2444eaa02541dd27fe90bed782.html
- EXEM. (s.f.). ¿A qué ondas estamos expuestos?. Recuperado de: https://www.exem.fr/es/a-que-ondas-estamos-expuestos/
- Prezi. (s.f.). Modulación y demodulación. Recuperado de: https://prezi.com/p/7io9nxs1dlij/modulacion-y-demodulacion/
- Panama Hitek. (s.f.). Señales continuas, analógicas, discretas y digitales. Recuperado de: https://panamahitek.com/senales-continuas-analogicas-discretas-y-digitales/
