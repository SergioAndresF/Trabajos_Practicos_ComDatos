# Trabajo Práctico N°2

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
El presente trabajo de laboratorio tiene como objetivo analizar diferentes fenómenos y mecanismos involucrados en los sistemas de comunicaciones de datos. Primeramente, se estudian algunos de los principales fenómenos que pueden afectar una transmisión, como pueden ser el Efecto Doppler y el Ruido. Asimismo, se analiza la influencia de estos fenómenos sobre las distintas bandas de frecuencia. 

Posteriormente, se introducen conceptos relacionados con la recuperación e interpretación de la información transmitida, abordándose temas como la sincronización, el entramado, la delimitación de tramas y los mecanismos de detección y corrección de errores.

Finalmente, se aplican algunos de estos conceptos a un caso práctico en el cual se debe interpretar un archivo binario serializado, identificar los campos que componen cada paquete y reconstruir la información correspondiente a los distintos grupos.

---
## Consignas
### Consigna N°1: 

Analizar la siguiente figura:

<center>
    <img src="https://hackmd.io/_uploads/BJ1YJOXuzx.png" width="1000">
    <br>
    <em>Figura 1: Representación: Efecto Doppler.</em>
</center>

Y responder:

**a.** ¿Qué fenómeno físico se está representando en la Figura? ¿Cuáles son las características principales del mismo?
> El fenómeno físico que se representa en la figura es el **Efecto Doppler** y consiste en el **desplazamiento aparente de la frecuencia recibida** como consecuencia del **movimiento relativo** entre el emisor y el receptor, en este caso, el barco y el satélite respectivamente. Este fenómeno ocurre debido a que los satélites se desplazan a **altas velocidades** en relación con las estaciones terrestres.
> 
> Tal como se ilustra en la figura, dado que el satélite se desplaza hacia el emisor, la frecuencia recibida resulta ser mayor que la frecuencia originalmente transmitida, también denominada **frecuencia nominal**. Por lo tanto, se produce un **corrimiento de la frecuencia de la portadora** que debe ser considerado por el sistema receptor.
>
> Puede ocurrir que el corrimiento de la frecuencia **exceda cierto rango**. En ese caso, es posible que el receptor no pueda adquirir o mantener correctamente la señal. Por lo tanto, si no se compensa este margen de error, este fenómeno termina afectando de manera directa a la capacidad del equipo receptor para adquirir, rastrear y decodificar las señales de manera exitosa, **reduciendo su rendimiento**.

**b.** Recordando las bandas de transmisión vistas en el TP01, investigar: ¿A qué tipos de transmisión afecta más este fenómeno? ¿Cuáles son más resilientes al mismo?
> Para responder este punto, se acude a la expresión matemática del **Efecto Doppler** aplicado a ondas electromagnéticas y considerando un movimiento relativo en la dirección de propagación:

$$f_r=f_t\cdot \sqrt {\frac{c \pm v}{c \mp v}} $$

> Si la velocidad relativa resulta ser mucho menor que la velocidad de la luz, como ocurre habitualmente en los sistemas de comunicaciones, esta expresión puede aproximarse mediante el desplazamiento de frecuencia:

$$\Delta f \approx \frac{v}{c} \cdot f$$

> De esta relación puede observarse que, manteniendo constante la velocidad relativa, el desplazamiento Doppler es **proporcional a la frecuencia de la onda portadora**. Por lo tanto, aquellas transmisiones que operan en **frecuencias más altas** son, en general, más susceptibles al efecto Doppler ya que presentan un **mayor desplazamiento**, mientras que las que utilizan **frecuencias más bajas** presentan una **mayor resiliencia** frente a este fenómeno.
>
> Ahora bien, considerando las bandas de radiofrecuencia estudiadas en el TP N°1, las **bandas LF, MF y HF** presentan un **menor desplazamiento Doppler** para una misma velocidad relativa. Luego, a medida que aumenta la frecuencia, como ocurre en **VHF, UHF, SHF y EHF**, el desplazamiento Doppler producido por una misma velocidad **también aumenta**, por lo que estas transmisiones pueden verse más afectadas por este fenómeno.
>
> Resulta conveniente aclarar que esto no significa que las bandas de baja frecuencia sean **inmunes al efecto Doppler** ni que las de alta frecuencia necesariamente presenten un **peor desempeño**. El impacto concreto depende también de factores como la velocidad relativa, así como la modulación utilizada, el ancho de banda y la capacidad del sistema para **compensar el desplazamiento de frecuencia.**

**c.** Investigar: ¿Cuáles son las razones por las cuales no se debe encender el celular arriba de un avión? ¿Tiene algo que ver el fenómeno descrito en los puntos anteriores?
> De acuerdo con la normativa estadounidense de la **Federal Communications Commission (FCC)**, se prohíbe la operación de teléfonos celulares mientras el avión se encuentra en vuelo. Una de las principales razones técnicas está relacionada con la arquitectura de las redes celulares terrestres y con la **reutilización de frecuencias**.

<center>
  <img src="https://hackmd.io/_uploads/Syd_QfHiMl.png" width="300">
  <br>
  <em>Figura 2: Reutilización de Frecuencias.</em>
</center>

> La arquitectura celular divide el área de cobertura en **celdas** y permite reutilizar una misma frecuencia en distintas zonas geográficas, aprovechando la separación espacial y la atenuación de las señales para limitar la interferencia entre ellas. Sin embargo, retomando el caso del avión, cuando un teléfono celular se encuentra a una **altura elevada**, existe una menor presencia de obstáculos y una mayor línea de vista, ambos efectos permiten que la señal pueda alcanzar simultáneamente a **múltiples estaciones base** que operan en la misma banda. Por lo tanto, puede aumentar considerablemente la posibilidad de **interferencia co-canal** entre las celdas.
>
> En ese sentido, el dispositivo móvil puede desplazarse rápidamente entre las áreas de cobertura de múltiples estaciones base, lo que genera una mayor cantidad de traspasos de conexión o, también llamados, **handovers**, y una carga adicional de señalización para la red.

<center>
  <img src="https://hackmd.io/_uploads/Bkd2XzSsMe.png" width="300">
  <br>
  <em>Figura 3: Handover.</em>
</center>

> Ahora bien, a modo de relacionarlo con el **Efecto Doppler** estudiado anteriormente, la elevada velocidad relativa entre el avión y las estaciones terrestres también produce un corrimiento de la frecuencia de la portadora. Este desplazamiento puede dificultar la sincronización y el seguimiento de la señal recibida, por lo que constituye otro factor que debe ser considerado en el diseño del enlace.
>
> Asimismo, conviene aclarar que también debe considerarse la posibilidad de interferencia con los propios sistemas de comunicación y navegación del avión, razón por la cual las autoridades aeronáuticas establecen restricciones para los dispositivos que transmiten intencionalmente por radiofrecuencia.

---
### Consigna N°2: 
Analizar la siguiente figura:

<center>
  <img src="https://hackmd.io/_uploads/Sy8nJdQuzl.png" width="700">
  <br>
  <em>Figura 4: Representación: Ruido.</em>
</center>

Y responder:

**a.** ¿Qué fenómeno físico se está representando en la Figura? ¿Cuáles son las características principales del mismo?
> En la figura se observa el efecto debido al **ruido**, el cual consiste en la modificación de una señal transmitida debido a señales no deseadas introducidas en algún punto entre el emisor y el receptor. El ruido puede clasificarse de acuerdo a dos categorías: 
> 
> - **Ruido Correlacionado:** Es aquel que presenta una relación estadística con la señal transmitida, de manera que sus características **dependen de la propia señal.**
> 
> - **Ruido No Correlacionado:** Presente **independientemente de si haya una señal o no,** por ejemplo, ruido atmosférico, ruido industrial, ruido térmico, entre otros.
>
> Habiendo aclarado las clasificaciones del ruido y retomando el ejemplo mostrado en la figura, se puede notar que se trata de **ruido no correlacionado**, específicamente, causado por el hombre. 
> 
> Las fuentes principales de este ruido son los mecanismos que producen **chispas**, como es el caso de los conmutadores de los motores eléctricos, sistemas de encendido automotriz, entre otros. Este ruido tiene **naturaleza de pulsos** y, por lo tanto, contiene una amplia gama de frecuencias que se propagan por el espacio del mismo modo que las ondas de radio.


**b.** Recordando las bandas de transmisión vistas en el TP01, investigar: ¿A qué tipos de transmisión afecta más este fenómeno? ¿Cuáles son más resilientes al mismo?
> A diferencia del fenómeno analizado en la Consigna N°1, no puede establecerse una relación directa entre la frecuencia y el nivel de ruido, ya que existen diferentes fuentes cuyo predominio depende tanto de la banda de frecuencia como del entorno en el que se realiza la transmisión. Entre las principales fuentes pueden mencionarse el **ruido atmosférico**, producido principalmente por descargas eléctricas, el **ruido artificial**, generado por equipos, instalaciones y dispositivos eléctricos, y el **ruido de origen extraterrestre**, proveniente de fuentes naturales externas a la Tierra.
>
> Generalmente, las **bandas de frecuencias más bajas**, como es el caso de **LF, MF y HF**, presentan una **mayor influencia del ruido externo**, especialmente del ruido atmosférico y del generado por fuentes artificiales. Esto se debe a que estas fuentes presentan niveles de ruido particularmente elevados en las frecuencias bajas, pudiendo **reducir la relación señal a ruido** y, por consiguiente, dificultar la correcta recepción de la información.
>
> A medida que se avanza hacia bandas superiores, como **VHF y UHF**, la influencia de algunas de estas fuentes de ruido externo tiende a disminuir, por lo que estas transmisiones presentan, generalmente, un **entorno más favorable** frente al ruido atmosférico y artificial. Sin embargo, esto no implica que dichas bandas sean **inmunes al ruido**, ya que continúan presentes otras fuentes, como el ruido térmico y las interferencias producidas por otros sistemas.
>
> Por lo tanto, puede afirmarse que, generalmente, las transmisiones en **bandas de frecuencia más bajas** son **más susceptibles al ruido externo**, mientras que las **bandas VHF y UHF** presentan una **mayor resiliencia** frente a dichas fuentes. No obstante, el nivel de ruido que afecta a una transmisión depende también de factores como la ubicación del sistema, las condiciones atmosféricas, el entorno electromagnético y las características particulares del enlace.

**c.** ¿Qué es la SNR? ¿Tiene algo que ver con el concepto de BER que vimos en el TP01?
> La **relación señal a ruido (SNR)** es el parámetro fundamental para evaluar la **calidad** de un sistema de comunicaciones y se define como el cociente entre la potencia de la señal y la potencia del ruido presente en el mismo canal, habitualmente se expresa en decibelios.

$$SNR_{dB}=10\cdot log_{10}\left( \frac{Potencia\space de\space Señal}{Potencia\space de\space Ruido}\right) $$
  
> Ahora bien, con respecto al concepto de **BER**, conviene recordar que el mismo es un indicador que representa la proporción de bits recibidos incorrectamente respecto del total de bits recibidos. 
> 
$$BER=\frac{Bits \space recibidos \space incorrectamente}{Bits\space recibidos\space totales}$$

> Entonces, teniendo en cuenta esto, existe una relación entre ambos parámetros y es que, generalmente, a medida que **aumenta la SNR**, la **BER tiende a disminuir**. 
> 
> De esta manera, para un nivel de ruido constante, si se aumenta la potencia de la señal, que equivale a un aumento de la SNR, el receptor tendrá menos dificultades para distinguir los niveles lógicos. En conclusión, un aumento de la SNR tiende a reducir la tasa de error de bit (BER), aunque la **relación exacta** entre ambos parámetros también depende de la modulación, la codificación y las características del receptor.

---
### Consigna N°3: 
Resumir brevemente y para ir pensando: ¿Cómo ayudan los sistemas de transmisión digital a detectar y corregir errores producidos por ruido en el canal? ¿Y a compensar cambios en la frecuencia?
> El **control de errores** surge como necesidad ante las **características no ideales** de la transmisión tales como el ruido, las interferencias o fallas que están presentes en cualquier sistema de comunicaciones. Es por esto que resulta necesario desarrollar e implementar procedimientos para **identificar y corregir errores.** Este control se puede dividir en dos categorías generales:
>
> - **Detección de Errores:** Técnicas encargadas de **vigilar los datos recibidos** y determinar cuándo se produce un error de transmisión. Cabe aclarar que dichas técnicas **no identifican los bits erróneos**, sino que **sólo indican que hubo un error**. Asimismo, el objetivo de la detección de errores no es evitar que ocurran errores, sino **evitar que haya errores sin detectar**. Entre las técnicas más comunes se pueden mencionar la redundancia, echoplex (echo checking), codificación de cuenta exacta (exact-count coding), paridad, suma de comprobación (Checksum), comprobación de redundancia vertical y horizontal y comprobación de redundancia cíclica (CRC).
> 
> - **Corrección de Errores:** Existen tres métodos para **corregir errores**, los cuales son: sustitución de símbolo, retransmisión (ARQ) y corrección de error en sentido directo (FEC). Esta técnica se diferencia de la retransmisión mediante ARQ en que permite **detectar y corregir** determinados errores directamente en el receptor, sin solicitar una **retransmisión de los datos**.

<center>
  <img src="https://hackmd.io/_uploads/rJNU76zizg.png" width="600">
  <br>
  <em>Figura 5: Correción en Sentido Directo (FEC).</em>
</center>

> Con respecto a la **compensación de frecuencia**, teniendo en cuenta que las variaciones dinámicas de la portadora pueden estar sujetas a los corrimientos originados por el Efecto Doppler o, también, a errores e inestabilidades de los osciladores, los sistemas de transmisión digital implementan mecanismos de compensación tanto a **nivel de hardware físico** como de **procesamiento de señales**.
>
> Si nos ubicamos a **nivel de hardware**, se emplean circuitos de recuperación de portadora basados en un **Lazo de Seguimiento de Fase (PLL)**, el cual funciona como un sistema de control realimentado en lazo cerrado. Su funcionamiento consiste en **comparar continuamente** la señal entrante con un oscilador local, de modo tal que, al detectar una desviación de frecuencia, genera una **señal de error**. Esta señal ajusta dinámicamente el oscilador para así **anular la diferencia** y **mantener el sincronismo con la portadora.**

<center>
  <img src="https://hackmd.io/_uploads/HyecX6MoMl.png" width="500">
  <br>
  <em>Figura 6: Diagrama en Bloques de PLL.</em>
</center>

> En cuanto a **nivel de procesamiento**, se utilizan técnicas analíticas para predecir y corregir el error:
> - **Ecualizadores Adaptativos:** Son filtros digitales que modifican sus coeficientes en tiempo real para **contrarrestar la distorsión.**
> 
> - **Tonos Piloto:** Consiste en enviar una **señal de referencia** junto con los datos. De esta manera, si el receptor evalúa que el tono piloto muestra cierto corrimiento en frecuencia, **deduce el error** que introdujo el medio de transmisión para aplicar esa misma **corrección matemática** al resto de la trama de información **antes de decodificarla.**

---
### Consigna N°4: 
Vamos ahora a discutir e investigar cómo podemos empezar a interpretar la información una vez decodificada:

**a.** ¿Qué significa sincronización en una comunicación digital? Investigar la diferencia entre sincronización de bits y sincronización de trama.
> En la transmisión digital, la **sincronización** es un requisito fundamental para interpretar correctamente los datos. Para que el receptor interprete correctamente las señales, sus **intervalos de bit** deben corresponder exactamente con los **intervalos de bit del emisor**. Si el reloj del receptor es más rápido o más lento, los intervalos no coincidirán y se malinterpretarán las señales recibidas. Existen soluciones que se realizan tanto a **nivel de capa física** como a **nivel de capa de enlace**:
> 
> - **Sincronización de Bits (Capa Física):** Consiste en la **alineación temporal exacta** entre el reloj del emisor y el del receptor, esto con el objetivo de determinar de manera precisa los instantes de tiempo en los que el receptor debe **muestrear** para así interpretar correctamente cada "0" o "1". En el caso que los relojes presenten cierto **desfasaje**, el receptor podría leer un mismo bit dos veces o saltearse uno, **corrompiendo los datos.**
> Para mantener esta sincronización, se emplean **señales digitales "auto-sincronizadas"** que incorporan transiciones de voltaje en los propios datos transmitidos, permitiendo al hardware receptor ajustar su reloj interno continuamente.
>
> - **Sincronización de Trama (Capa de Enlace):** Una vez que el hardware logra interpretar correctamente los bits a nivel físico, entrega un **flujo continuo e ininterrumpido de unos y ceros**. El sincronismo de trama es el proceso mediante el cual el receptor logra **separar y agrupar lógicamente** esa cadena de bits para identificar el inicio y fin de un bloque de información o trama. En las **transmisiones síncronas**, al no existir tiempos muertos ni bits de inicio/parada entre los caracteres, es responsabilidad de la capa de enlace aplicar los **métodos de entramado** necesarios para delimitar las tramas y reconstruir la información original.

**b.** ¿Qué es una trama (frame)? ¿Qué diferencias existen entre el encabezado (header), la carga útil (payload) y el tráiler (trailer)?

> El **entramado** es el primer servicio que ofrece la capa de enlace de datos. Esta capa recibe un paquete de la capa de red, denominado **datagrama**, y debe encapsularlo en una **trama** antes de enviarlo al siguiente nodo. Entonces, se puede definir a la trama como el **paquete de la capa de enlace de datos**. Asimismo, existen diferentes protocolos, los cuales establecen el formato de entramado a seguir. 

<center>
  <img src="https://hackmd.io/_uploads/rJXTgpzjMg.png" width="650">
  <br>
  <em>Figura 7: Estructura de una Trama.</em>
</center>

> De acuerdo a la figura anterior, la estructura lógica de una trama se divide en las siguientes partes:
> - **Carga Útil (Payload):** Son los datos puros que **provienen del paquete de la capa de red** y que la capa de enlace debe transportar.
> 
> - **Encabezado (Header):** Es la **información de control** que la capa de enlace añade a la carga útil. Este encabezado puede contener, por ejemplo, direcciones de enlace como las direcciones MAC, además de otros campos de control necesarios para procesar la trama.
> 
> - **Tráiler:** Es un **campo de control** que se añade al final de la trama y que, en muchos protocolos, incluye información de control destinada a la **detección de errores**, como un **FCS o CRC**, permitiendo al receptor verificar si los datos fueron alterados durante la transmisión.

**c.** ¿Qué función puede cumplir un preámbulo antes de una trama? ¿Es necesariamente parte de la información que se quiere transmitir?
> El **preámbulo** es un patrón físico de bits, el cual, generalmente, resulta ser una **secuencia alternada de ceros y unos,** como `10101010`. Este patrón se transmite en el medio físico inmediatamente **antes de que comience la trama real**, con el objetivo de avisar al receptor que una trama está en camino y, de esta manera, lograr la sincronización de bits. 
>  
> El preámbulo **no contiene información útil** correspondiente a los datos del usuario. Por lo tanto, no es necesariamente parte de la información que se desea transmitir, sino que constituye **información auxiliar** utilizada para facilitar la recepción correcta. En Ethernet a 10 Mbps, los 56 bits correspondientes al preámbulo ocupan 5,6 μs, mientras que el preámbulo junto con el SFD ocupan 64 bits, equivalentes a 6,4 μs.

**d.** Investigar al menos tres formas mediante las cuales un protocolo puede determinar dónde termina una trama: longitud fija, un campo que indique la longitud y caracteres/secuencias delimitadoras.
> - **Longitud Fija:** Como su nombre lo indica, no es necesario definir los límites de las tramas, sino que, el **propio tamaño** puede utilizarse como delimitador. Un ejemplo de este mecanismo es ATM, utilizado en redes de comunicaciones y que emplea celdas de tamaño fijo de 53 bytes.
> 
> - **Conteo de Caracteres:** Este método se apoya en un campo en el encabezado para especificar el **número de caracteres en la trama**. De esta manera, la capa de enlace de datos del destino conoce cuántos caracteres siguen y, por lo tanto, el fin de la trama. 
> El inconveniente que se presenta es que la cuenta puede alterarse por un **error de transmisión.** En ese caso, el destino perderá la sincronía y será incapaz de localizar el inicio de la siguiente trama aún así la suma de verificación sea incorrecta, ya que no tiene forma de saber dónde comienza la siguiente trama. 
> Por otro lado, regresar una trama a la fuente solicitando una retransmisión tampoco ayuda, ya que el destino no sabe cuántos caracteres tiene que saltar para llegar al inicio de la retransmisión.

<center>
  <img src="https://hackmd.io/_uploads/HyxlUhXofe.png" width="600">
  <br>
  <em>Figura 8: Método de Conteo de Caracteres: Sin errores y Con errores.</em>
</center>

> - **Caracteres/secuencias delimitadoras:** Se puede abordar desde dos enfoques:
> 
> **Orientado a Caracteres:** Tanto la cabecera (header) como el tráiler tienen una longitud múltiplo de 8 bits. Para separar una trama de la siguiente, se añade un **delimitador o flag** de 8 bits al principio y al final de la trama que está compuesto por **caracteres especiales** dependientes del protocolo.

<center>
  <img src="https://hackmd.io/_uploads/Hyih83XoGg.png" width="550">
  <br>
  <em>Figura 9: Protocolo Orientado a Caracteres.</em>
</center>

> Era bastante utilizado para **intercambio de texto,** ya que el delimitador podía elegirse de entre aquellos caracteres que no se utilizaban para la comunicación. Sin embargo, actualmente además de texto se transmite otro tipo de información como **audio y vídeo**. Por lo tanto, cualquier carácter utilizado como delimitador también podría formar parte de los datos.
> 
> Para solucionar este problema, se incorporó una estrategia conocida como **inserción de bytes (byte stuffing).** Esta técnica consiste en añadir un **byte especial** a la sección de datos de la trama siempre que aparece un caracter con el mismo patrón que el delimitador. Este byte suele denominarse **caracter de escape (ESC)** y posee un patrón de bits predefinido. Siempre que el receptor encuentra el caracter ESC, lo **elimina** de la sección de datos y trata el caracter siguiente como dato, no como un delimitador.

<center>
  <img src="https://hackmd.io/_uploads/BkUybpQjGg.png" width="550">
  <br>
  <em>Figura 10: Técnica de Inserción de Bytes.</em>
</center>

> **Orientado a Bits:** Utilizan una **secuencia especial** de 8 bits con el patrón `01111110` como delimitador para definir el inicio y el final de la trama
 
<center>
  <img src="https://hackmd.io/_uploads/rkSpIhXjGe.png" width="550">
  <br>
  <em>Figura 11: Protocolo Orientado a Bits.</em>
</center>

> Esta bandera puede generar el mismo tipo de problema que se observó en los protocolos orientados a caracteres, entonces, si el patrón de la bandera aparece dentro de los datos, es necesario informar al receptor que eso no representa el final de la trama. Para ello, se inserta un **único bit en lugar de un byte completo**, para evitar que el patrón se confunda con una bandera. 
> 
> Esta estrategia se denomina **inserción de bits (bit stuffing)** y consiste en añadir un `0` tras una secuencia de cinco `1` consecutivos después de un `0` en los datos, esto significa que, si el patrón similar a la bandera `01111110` aparece en los datos, se transformará en`011111010`, evitando así la confusión. Posteriormente, este bit insertado es **eliminado** de los datos por el receptor.

<center>
  <img src="https://hackmd.io/_uploads/HJLSnaQiGx.png" width="550">
  <br>
  <em>Figura 12: Técnica de Inserción de Bits.</em>
</center>

---
### Consigna N°5: 
Una vez que todos los grupos tengan nombre, recibirán un archivo de datos digitales serializados en formato binario, donde deberán extraer la carga útil correspondiente a su grupo, según el siguiente formato:

<center>
  <img src="https://hackmd.io/_uploads/Bk12WumOfg.png" width="700">
  <br>
  <em>Figura 3: Esquema de Transmisión de Datos.</em>
</center>

Donde:
- GROUP corresponde a los primeros 5 caracteres del nombre del grupo (lower case)
- SEQ corresponde al número de secuencia del paquete
- LENGTH corresponde al largo, uint, en bytes, de la carga útil (PAYLOAD)

**a.** Identificar la carga útil correspondiente a su grupo y documentar, tanto en el informe como en una pestaña destinada a ello en la planilla compartida.
> Para este punto se ha utilizado el **editor hexadecimal HxD** para poder leer el archivo .bin compartido mediante el drive de la asignatura. En el mismo, se pudo identificar la siguiente línea de interés:

<center>
  <img src="https://hackmd.io/_uploads/SJeC2SXofg.png" width="800">
  <br>
  <em></em>
</center>

> A partir de la secuencia resaltada y teniendo en cuenta el **formato** presentado anteriormente, se procede a identificar y clasificar cada uno de sus campos, como se muestra a continuación:

<center>
  <img src="https://hackmd.io/_uploads/H1wc2R7ofx.png" width="400">
  <br>
  <em></em>
</center>

> Como se puede observar, los primeros cinco bytes, expresados en hexadecimal como `67` `72` `6F` `75` `70`, corresponden a los caracteres `g`, `r`, `o`, `u` y `p` en **codificación ASCII**, formando la palabra "group". Luego, se identifica el sexto byte, correspondiente al **campo SEQ.** Su valor hexadecimal `20` equivale al valor decimal `32`. El siguiente byte indica la **longitud de la carga útil,** que en este caso es de 1 byte. Finalmente, a partir del valor indicado por **LENGTH** se determina la cantidad de bytes que corresponden al **campo PAYLOAD**. En este caso, la carga útil tiene una longitud de 1 byte y corresponde a la letra `"w"`.

**b.** Sabiendo que SEQ es el número de secuencia, reorganizar los paquetes de todos los grupos y reconstruir la información final (concatenar los caracteres).
> Se realiza el mismo procedimiento del inciso anterior para cada uno de los grupos listados. A continuación, se presenta la siguiente tabla que reúne la información extraída del archivo binario.

<center>
  <img src="https://hackmd.io/_uploads/rJ3jFR7iMg.png" width="550">
  <br>
  <em></em>
</center>

> Una vez obtenidos los paquetes correspondientes a cada grupo, se procede a concatenar los mismos. Durante ese procedimiento, se pudieron detectar **algunas anomalías**, una de ellas, justamente en relación a la secuencia de la carga útil asignada para este grupo. Revisando la estructura general, se presume que el número de secuencia correspondiente debería ser `7` en lugar de `32`. Por otro lado, los grupos "LAN-gustia" y "Los_CondIPcionales" compartían el mismo número de secuencia, `13`. Sin embargo, de acuerdo a la forma que iba tomando el enlace, se dedujo que el número de secuencia del grupo "LAN-gustia" era "10". Asimismo, no se pudo encontrar el paquete correspondiente al grupo "Los simuLANdores" debido a que se vio afectado por lo que se muestra a continuación en la figura. De todas formas se presume que sus valores de **SEQ y PAYLOAD** eran `12` y `ub` respectivamente:

<center>
  <img src="https://hackmd.io/_uploads/SJn8Yx4jGl.png" width="550">
  <br>
  <em></em>
</center>

> Teniendo en cuenta estos detalles y las inferencias que se hicieron, se procedió a realizar el ordenamiento de los paquetes concatenando sus respectivas cargas útiles. El resultado final es la **siguiente URL:**
> `https://www.youtube.com/shorts/dbbe_ln6Lnw`



---
## Conclusiones
A lo largo del presente trabajo se estudiaron diferentes fenómenos y mecanismos que intervienen en una comunicación digital. En primera instancia, se estudió el Efecto Doppler y se pudo observar que, para una misma velocidad relativa, el desplazamiento de frecuencia aumenta proporcionalmente con la frecuencia de la portadora, permitiendo comprender  los motivos por los que las transmisiones que operan en bandas de frecuencia más elevadas requieren una mayor consideración de este fenómeno.

También se analizó el ruido como una perturbación que puede modificar la señal recibida y afectar la relación señal a ruido (SNR) y, en consecuencia, la tasa de error de bit (BER). A su vez, se estudiaron mecanismos utilizados por los sistemas digitales para detectar y corregir errores, así como técnicas destinadas a mantener la sincronización y compensar variaciones de frecuencia.

Posteriormente, se profundizó en el concepto de trama, distinguiendo sus diferentes campos y analizando los mecanismos o técnicas mediante los cuales un receptor puede determinar sus límites. Para finalizar, estos conceptos se aplicaron a un caso práctico de interpretación de datos binarios, en el cual fue necesario identificar campos, interpretar valores hexadecimales y reorganizar paquetes mediante sus números de secuencia para reconstruir la información transmitida.

En resumen, a través de este trabajo de laboratorio se abordaron conceptos que permiten observar cómo un sistema de comunicaciones no sólo debe transmitir información, sino también proporcionar los mecanismos necesarios para sincronizar, identificar, verificar y recuperar correctamente los datos recibidos, incluso cuando el canal introduce distintas clases de perturbaciones.

---
## Referencias
- Federal Communications Commission. (1991). Prohibition on airborne operation of cellular telephones (47 CFR § 22.925). Código de Regulaciones Federales de los Estados Unidos.
- Inuvik Web Services. (2026). Doppler Shift Explained and How Stations Compensate. Satellite Ground Station. Recuperado de https://satellitegroundstation.com/resources/doppler-shift-explained-and-how-stations-compensate/
- International Telecommunication Union. (2026). Recommendation ITU-R P.372-18: Radio noise.
- Rappaport, T. S. (2002). Wireless communications: Principles and practice (2.ª ed.). Prentice Hall.
- Tomasi, W. (2003). Sistemas de comunicaciones electrónicas (4.ª ed.). Pearson Educación.
- Stallings, W. (2004). Comunicaciones y redes de computadores (7.ª ed.). Pearson Prentice Hall.
- Forouzan, B. A. (2007). Transmisión de datos y redes de comunicaciones (5.ª ed.). McGraw-Hill Interamericana.
