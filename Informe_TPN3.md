# Trabajo Práctico N°3

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
El presente trabajo de laboratorio tiene como objetivo profundizar en el funcionamiento de las comunicaciones de datos dentro de una red. En ese sentido, se comienza analizando la capa de enlace para luego estudiar los protocolos IP y TCP, que pertenecen a las capas de red y transporte respectivamente.

En primera instancia, se analizan conceptos relacionados con Ethernet, como las direcciones MAC, la estructura de una trama y el campo EtherType. Posteriormente, se tiene una actividad que requiere el uso de Wireshark, este software permite observar cómo estas estructuras aparecen en una captura real de tráfico de red y cómo se relacionan las direcciones MAC con las direcciones IP.

Seguidamente, se profundiza en el protocolo TCP, estudiando los mecanismos que permiten proporcionar una comunicación fiable, los principales campos de su segmento y los procedimientos utilizados para establecer y finalizar una conexión. Finalmente, se prevé una actividad a realizar mediante PacketSender y Wireshark, la cual permite analizar una comunicación TCP real, identificando el proceso de establecimiento de la conexión, la transferencia de datos y su posterior cierre.

---
## Consignas
### Consigna N°1: 

Vamos a empezar observando cómo se organiza la información dentro de una red local.

**a.** ¿Qué función cumple la capa de enlace dentro del modelo OSI? ¿Qué tipo de comunicación resuelve?
> La **capa de enlace de datos** corresponde a la segunda capa del **modelo OSI** y tiene como función principal proporcionar los mecanismos necesarios para transferir información entre dos **nodos adyacentes**, es decir, dos nodos conectados por un canal de comunicaciones. Para ello, recibe paquetes provenientes de la capa de red y los **encapsula en tramas**, las cuales son posteriormente entregadas a la capa física para su transmisión.
> 
> Recordando lo abordado en el TP N°2, cada trama está compuesta por un encabezado (header), una carga útil (payload) para almacenar el paquete y un tráiler.

<center>
  <img src="https://hackmd.io/_uploads/By_NSBVoMg.png" width="600">
  <br>
  <em>Figura 1: Estructura de la Trama.</em>
</center>

> Entre las principales funciones de esta capa se encuentran:
> - **Entramado:** Permite dividir el flujo de bits proveniente de la capa física en unidades discretas denominadas tramas.
> 
> - **Control de Errores:** Mecanismos que permiten determinar si la información recibida fue alterada durante la transmisión.
> 
> - **Control de Flujo:** Depende del protocolo utilizado. Permite evitar que un receptor sea sobrecargado por un transmisor que opera a una velocidad superior.

> En cuanto al tipo de comunicación que resuelve, la capa de enlace se ocupa de una **comunicación nodo a nodo**, también denominada hop-to-hop. Esto significa que su función se limita a transportar una trama desde un nodo hasta el siguiente nodo directamente conectado (adyacente). Por lo tanto, mientras que las **capas superiores** pueden encargarse de la **comunicación extremo a extremo**, la **capa de enlace** resuelve los problemas propios de cada **enlace individual** que forma parte del camino entre el origen y el destino. 

**b.** ¿Qué es una dirección MAC? ¿En qué se diferencia de una dirección IP?

> - La **dirección MAC** es un identificador utilizado, justamente, para identificar una interfaz de red dentro de un **enlace local**. En Ethernet, una dirección MAC tiene 6 bytes de longitud (48 bits) y, habitualmente, se representa mediante **seis grupos de dos dígitos hexadecimales**.
>  Un detalle importante es que estas direcciones **no poseen una estructura jerárquica** que indique a qué red pertenece una interfaz. Por tal motivo, una dirección MAC no permite determinar directamente la ubicación de un dispositivo dentro de una interred.
> 
> - La **dirección IP**, por su parte, corresponde a la capa de red y **posee una estructura jerárquica** asociada al direccionamiento de la red. Una parte de esta dirección permite identificar la red o prefijo al que pertenece la interfaz, mientras que el resto permite identificar la interfaz dentro de dicho contexto. Es por esto que, una dirección IP **puede cambiar** cuando una interfaz se conecta a una red diferente.
>
> Habiendo presentado ambas direcciones, se puede decir que la **dirección MAC** se utiliza para la comunicación dentro del enlace local, mientras que la **dirección IP** permite realizar el direccionamiento y enrutamiento entre distintas redes.

<center>
  <img src="https://hackmd.io/_uploads/S1G5DSVjzl.png" width="550">
  <br>
  <em>Figura 2: Ilustración: Dirección MAC y Dirección IP.</em>
</center>

**c.** ¿Qué es una trama Ethernet? Identificar sus principales campos y explicar brevemente para qué sirve cada uno

> La **trama Ethernet** es la unidad de datos utilizada por la capa de enlace cuando se emplea Ethernet. Su estructura permite incorporar la información necesaria para **entregar los datos dentro de la red local** y realizar determinadas **funciones de control**, como la detección de errores.
> 
> En Ethernet II, una trama tiene un tamaño puede estar entre 64 y 1518 bytes, dependiendo del tamaño de los datos que debe transportar. Cabe aclarar que los campos correspondientes al preámbulo y SFD no se tienen en cuenta en la longitud.
>
> En la siguiente figura se muestra la **estructura de la trama de Ethernet** y, seguidamente, se describe cada uno de los campos que la conforman:

<center>
  <img src="https://hackmd.io/_uploads/SJu-E-W9Me.png" width="600">
  <br>
  <em>Figura 3: Estructura de la Trama Ethernet.</em>
</center>

> - **Preámbulo y SFD (8 bytes):** Los primeros siete bytes tienen el valor `10101010`, su objetivo es permitir al dispositivo B **sincronizar su reloj** con el del dispositivo A. El byte restante adopta el valor `10101011`, indicándole al dispositivo B que va a llegar información.
> 
> - **Dirección de Destino (6 bytes):** Contiene la dirección MAC de la interfaz a la que está destinada la trama dentro del enlace local.
> 
> - **Dirección de Origen (6 bytes):**  Contiene la dirección MAC de la interfaz que origina la trama.
> 
> - **Campo de Tipo (2 bytes):** Identifica el **protocolo** que se encuentra encapsulado en el campo de datos, pudiendo tratarse de IPv4, IPv6 o ARP.
> 
> - **Campo de Datos (46 a 1500 bytes):** Transporta la información de las capas superiores. Para una trama Ethernet convencional, la unidad máxima de transmisión es de 1500 bytes y el tamaño mínimo es de 46 bytes. En caso de que los datos tengan menos de 46 bytes, se agrega **información de relleno (padding)** para alcanzar el tamaño mínimo.
> 
> - **FCS (4 bytes):** Contiene un valor calculado mediante un mecanismo de **comprobación de redundancia cíclica (CRC)**, que permite al receptor detectar determinados errores producidos durante la transmisión de la trama.

**d.** ¿Qué información permite determinar qué protocolo de capa superior está transportando una trama Ethernet?

> El **Campo de Tipo** de la trama Ethernet funciona como una clave de multiplexación. Este campo le indica a la capa de enlace **qué protocolo está encapsulado** en el campo de datos y, por lo tanto, a qué protocolo de las capas superiores debe entregarle dicha información. Por ejemplo, el valor hexadecimal `0x0800` indica que se transporta un datagrama IPv4, mientras que `0x86DD` indica IPv6, y `0x0806` corresponde al protocolo ARP.

<center>
  <img src="https://hackmd.io/_uploads/HyDbYrNiGg.png" width="400">
  <br>
  <em>Figura 4: Protocolos de la Capa de Red: IPv4 e IPv6.</em>
</center>

---
### Consigna N°2: 
Usando Wireshark, capturar tráfico generado por su propia computadora mientras acceden a una página web o ejecutan alguna aplicación que utilice la red (en general no hace falta hacer nada realmente, el tráfico normal de la computadora ya genera UNA BOCHA de paquetes a internet).

**a.** Seleccionar una trama Ethernet e identificar las direcciones MAC de origen y destino. ¿A qué dispositivos creen que corresponden?

> Se abrió el software **Wireshark** y se inició una sesión de captura en la interfaz de **red local (Wi-Fi 2)**. De todos los paquetes disponibles para el análisis, se seleccionó el paquete N° 22837, correspondiente a una trama con **protocolo TCP.**
> 
> En la siguiente captura de pantalla se muestra el paquete seleccionado así como sus detalles, los cuales están remarcados en un cuadro rojo:

<center>
  <img src="https://hackmd.io/_uploads/SJj17rb9zg.png" width="800">
  <br>
  <em></em>
</center>

> Revisando el encabezado Ethernet II de la trama seleccionada, se logra identificar las siguientes direcciones físicas:
> 
> - **Dirección MAC de Destino:** `02:10:18:47:0c:b4`
> - **Dirección MAC de Origen:**  `18:4f:32:85:89:cf`


**b.** Dentro de la misma trama, identificar el paquete IP. ¿Cuáles son las direcciones IP de origen y destino? (no importa si son versión 4 o versión 6)
> Las direcciones IP encontradas son las siguientes, en este caso, responden al protocolo IPv4:
>
> - **IP de Destino:** `99.83.179.177`
> - **IP de Origen:** `192.168.0.234`

<center>
  <img src="https://hackmd.io/_uploads/HJGnqSEofx.png" width="800">
  <br>
  <em></em>
</center>

**c.** Comparar las direcciones MAC y las direcciones IP encontradas. ¿Representan lo mismo?
> No representan lo mismo debido a que pertenecen a **diferentes capas del Modelo OSI** y, por lo tanto, tienen **funciones distinas**. 
> 
> Las **direcciones IP (Capa 3)** proporcionan el **direccionamiento lógico** utilizado para identificar los extremos de una comunicación y permitir el **enrutamiento entre diferentes redes**. En la actividad anterior, la IP de origen (`192.168.0.234`) corresponde a la computadora desde la cual se genera el tráfico y la IP de destino (`99.83.179.177`) corresponde a un servidor remoto público en Internet.
> 
> Por el contrario, las **direcciones MAC (Capa 2)** permiten identificar las **interfaces involucradas** en la comunicación dentro del **enlace local**. En el caso de la actividad, debido a que el destino IP (servidor remoto) se encuentra fuera de la red local, la trama no se dirige directamente a la MAC del servidor remoto, sino a la MAC del siguiente salto (`02:10:18:47:0c:b4`), que en este caso corresponde a la puerta de enlace local.
> 
> Teniendo en cuenta estos detalles, las **direcciones MAC de origen y destino** cambian en cada salto, mientras que las **direcciones IP de origen y destino** se mantienen inalterables durante el enrutamiento.

**d.** Observar el campo EtherType. ¿Qué protocolo está encapsulado dentro de la trama analizada?
> En el encabezado Ethernet II de la trama capturada, el **Campo de Tipo** presenta el valor hexadecimal `0x0800`. Este valor le indica a la capa de enlace que la carga útil que está encapsulando corresponde al **protocolo IPv4**, y que debe entregarle los datos a dicho protocolo en la capa superior (Capa de Red) para continuar su procesamiento.

<center>
  <img src="https://hackmd.io/_uploads/B1PNsH4ofx.png" width="550">
  <br>
  <em></em>
</center>

---
### Consigna N°3: 
Vamos ahora a subir una capa y observar el transporte de información mediante TCP.

**a.** ¿Qué problema(s) resuelve TCP que no resuelve directamente Ethernet ni IP?
> El inconveniente que se presenta es que el **modelo de servicio IP** es un servicio de entrega de **mejor esfuerzo (best effort)**, es decir que, si bien se efectúa la transmisión de los datos entre los hosts que participan en la comunicación, **no está garantizado que estos lleguen a su destino**. A esto se suma que tampoco está garantizado el orden en el que se entregan ni su **integridad**. Lo anterior da lugar a que el **servicio IP no sea considerado confiable.**
>
> Con respecto a las limitaciones de la capa de enlace, **Ethernet** puede detectar errores en una trama mediante el FCS, sin embargo este mecanismo **no garantiza por sí mismo que la información llegue correctamente** desde el host de origen hasta el host de destino cuando existen **múltiples enlaces y routers entre ambos extremos.**
> 
> En ese sentido, el **modelo TCP** ofrece un servicio de **transferencia de datos fiable y orientado a la conexión**, agregando mecanismos que no son proporcionados directamente por IP:
> 
> - **Servicio de Transferencia de Datos Fiable:** TCP utiliza números de secuencia, mensajes de reconocimiento (ACK), temporizadores y retransmisiones para **detectar pérdidas y errores** y así poder **recuperar los datos correspondientes**. Además, los números de secuencia permiten que el receptor reconstruya el flujo de bytes en el orden correcto, incluso si los segmentos llegan desordenados.
> 
> - **Servicio Orientado a la Conexión:** Antes de comenzar la transferencia de datos, TCP establece una **conexión lógica** entre los dos extremos mediante el **Three-Way Handshake**. De esta manera, permite que ambos hosts puedan sincronizar los parámetros necesarios para la comunicación y mantener información sobre el estado de la conexión durante su funcionamiento. Una vez **finalizada la transferencia**, la conexión puede cerrarse mediante el intercambio de segmentos FIN y ACK, **Four-Way Handshake.**
>
> - **Control de Flujo:** TCP regula la cantidad de datos que el emisor puede enviar sin recibir confirmación, teniendo en cuenta la **capacidad de recepción del destino.** De esta manera, evita que un host transmisor envíe datos a una velocidad superior a la que el receptor puede procesar o almacenar.
> 
> - **Control de Congestión:** TCP también regula la velocidad a la que los emisores introducen tráfico en la red, con el objetivo de **evitar** que una cantidad excesiva de datos provoque la **congestión de los enlaces y routers** que forman parte de la comunicación. Para ello, TCP adapta su tasa de transmisión de acuerdo con las condiciones que observa en la red.

**b.** Investigar los campos más importantes de la metadata en un frame TCP. ¿Para qué sirve cada uno?

> Dentro del segmento TCP se pueden observar los siguientes campos:
> - **Puerto de Origen y de Destino (16 bits cada dirección):** Identifican los puertos asociados a las aplicaciones o procesos que participan en la comunicación, donde uno origina el segmento y otro lo recibe.
> 
> - **Número de Secuencia (Sequence Number) (32 bits):** Permite numerar los bytes transmitidos y determinar la posición que ocupa el contenido del segmento dentro del flujo de datos. De esta manera, el receptor puede reconstruir la información en el orden correcto y detectar segmentos faltantes o duplicados.

> - **Número de Confirmación (Acknowledgment Number) (32 bits):** Indica el siguiente número de secuencia que el emisor del segmento espera recibir, permiiendo confirmar la recepción de los datos anteriores. Este campo es válido cuando la bandera ACK se encuentra activada.
> 
> - **Longitud de la Cabecera (Data Offset) (4 bits):** Indica la longitud de la cabecera TCP lo que permite determinar el inicio del campo de datos. Típicamente la longitud es de 20 bytes, pero utilizando el campo de Opciones es posible alcanzar una longitud de hasta 60 bytes.
>
> - **Campo Reservado (6 bits):** Inicializado con ceros.
>
> - **Banderas de Control (8 bits):** Son bits utilizados para indicar diferentes eventos o acciones relacionadas con el estado de la conexión. Entre las principales se encuentran:
> **SYN:** Permite sincronizar los números de secuencia y participar en el establecimiento de la conexión.
> **ACK:** Indica si el campo Acknowledgment Number es válido.
> **FIN:** Indica que el emisor no posee más datos para transmitir.
> **RST:** Permite reiniciar o abortar una conexión.
> **PSH:** Solicita que los datos sean entregados al proceso receptor sin esperar una acumulación adicional.
> **URG:** Indica si el campo Urgent Pointer contiene información significativa.
> **ECE y CWR:** Están relacionados con mecanismos de notificación de congestión.
>
> - **Ventana (16 bits):** Indica la cantidad de datos que el receptor está dispuesto a aceptar a partir del número de secuencia indicado en el campo de confirmación (Acknowledgment Number). Además, permite implementar el control de flujo, evitando que el emisor transmita una cantidad de datos superior a la que el receptor puede almacenar.
>
> - **Checksum (16 bits):** Permite verificar la integridad del segmento recibido y detectar alteraciones producidas durante la transmisión. El receptor puede utilizar este valor para determinar si el segmento fue corrompido.
>
> - **Urgent Pointer (16 bits):** Se utiliza junto con la flag URG para señalar la posición correspondiente al final de la información considerada urgente dentro del flujo de datos.
>
> **Options:** Agrega funcionalidades adicionales al protocolo TCP. Entre las opciones más habituales se pueden mencionar Maximum Segment Size (MSS), Window Scale, Selective Acknowledgment (SACK) y TCP Timestamp.
> 
> Habiendo detallado cada uno de los campos, se puede observar que estos permiten que el protocolo no se limite únicamente a transportar datos, sino que también logre identificar los procesos de origen y destino, ordenar la información, confirmar su recepción, controlar el flujo, detectar errores y administrar el establecimiento y cierre de la conexión.

<center>
  <img src="https://hackmd.io/_uploads/HJJXvuZ5zx.png" width="350">
  <br>
  <em>Figura 5: Estructura del Segmento TCP.</em>
</center>

**c.** Explicar el Three y Four way handshake en TCP.
> - **Three-Way Handshake (Establecimiento de la Conexión):** Su objetivo consiste en establecer la conexión y permitir que ambos extremos logren sincronizar sus números de secuencia iniciales, además de confirmar que existe comunicación en ambas direcciones. Recibe este nombre debido a que el proceso consta de las siguientes tres vías:
> **1.-** El cliente envía un segmento con la bandera SYN activada y un número de secuencia inicial `x`. Con esto, el cliente está indicando su intención de establecer una conexión y también comunicando el número de secuencia a partir del cual comenzará su transmisión.
> **2.-** El servidor responde con las banderas SYN y ACK activadas y establece su propio número de secuencia inicial `y`. Luego, mediante el campo de confirmación, indica que recibió correctamente el SYN del cliente y que espera el próximo número de secuencia, es decir, `x+1`.
> **3.-** Finalmente, el cliente envía un segmento con la bandera ACK activada, indicando mediante el campo de confirmación que espera recibir `y+1` como próximo número de secuencia del servidor. Una vez que se haya completado este intercambio, ambos extremos han sincronizado sus números de secuencia y la conexión puede pasar al estado ESTABLISHED, permitiendo comenzar la transferencia de datos.
> 
<center>
  <img src="https://hackmd.io/_uploads/SkZCRD4iGl.png" width="300">
  <br>
  <em>Figura 6: Three-Way Handshake.</em>
</center>

> - **Four-Way Handshake (Cierre de la Conexión):** Una vez que uno de los extremos haya concluido con la transmisión de los datos, TCP no necesariamente cierra de manera simultánea las dos direcciones de la comunicación; sino que como TCP es un protocolo full-duplex, cada extremo puede indicar de manera independiente que ya no posee más datos para transmitir. La secuencia normal de cierre puede representarse mediante cuatro segmentos:
> **1.-** Uno de los extremos envía un segmento con la bandera FIN activada para indicar que no posee más datos para transmitir en esa dirección.
> **2.-** El otro extremo confirma la recepción mediante un ACK. Sin embargo, cabe aclarar que esto no significa que la comunicación haya finalizado completamente, ya que existe la posibilidad de que el segundo extremo todavía tenga datos pendientes de transmitir.
> **3.-** Una vez que el segundo extremo termina su transmisión, envía también un segmento con la bandera FIN. 
> **4.-** Finalmente, el primer extremo responde con un ACK, completando el cierre de la conexión.

<center>
  <img src="https://hackmd.io/_uploads/SkYCCD4sGl.png" width="300">
  <br>
  <em>Figura 7: Four-Way Handshake.</em>
</center>

---
Iniciar una instancia de PacketSender (ésta será el servidor). Explorar la interfaz, discutir con los compañeros que puede ser cada una de las cosas que estamos viendo.

En esta instancia, iniciar un servidor TCP:

> Para la resolución de esta actividad se inicia una instancia el PacketSender, la cual adoptará el rol de servidor. A continuación, se muestra la ventana correspondiente y en la misma se recuadra el puerto que, en este caso, recibe el número de `64885` y es el que debe tenerse en cuenta para la etapa de transmisión: 

<center>
  <img src="https://hackmd.io/_uploads/H1vw5cNjzl.png" width="600">
  <br>
  <em></em>
</center>

Iniciar otra instancia de PacketSender (cliente) sin cerrar la primera, configurar la dirección local (localhost, 127.0.0.1 o tu dirección IP si la conoces) y el puerto del servidor TCP que acabas de configurar:

> Se inicia otra instancia del PacketSender que cumplirá el rol de cliente. Posteriormente, se completan los campos recuadrados: en Address se registra la dirección `127.0.0.1` y en Port el número de puerto del servidor, `64885`.

<center>
  <img src="https://hackmd.io/_uploads/H13n5qEofe.png" width="700">
  <br>
  <em></em>
</center>

Configurar wireshark para “sniffear” la conexión que vamos a hacer. Monitorear la dirección de loopback y, te recomendamos, configurá algún filtro para tener la consola “limpia” hasta que iniciemos la conexión. Por ejemplo, tcp.dstport == puerto.

> La actividad requiere abrir el software Wireshark para así poder visualizar todos los paquetes que resultarán de este análisis. Para ello, se inicia una sesión de captura en la interfaz de "Adapter for loopback traffic captures".
>
> Posteriormente, a fin de mostrar únicamente los paquetes de interés, se configura el filtro escribiendo `tcp.dstport == 64885`.

**d.** Iniciar la conexión enviando un paquete, capturar el handshake y el paquete de datos. Analizar el paquete de datos, sus distintas partes y encontrar la carga útil del paquete usando WireShark.
> Habiendo realizados los pasos anteriores, se procede a anotar el mensaje que se desea enviar de cliente a servidor en el campo ASCII. En este caso, el mensaje que se envía es `Hola!`. Una vez anotado el mensaje se hace click en `Send`. Instantáneamente, se abrirá una ventana a modo de mantener la interacción con el servidor, si se cierra esta ventana se da por finalizada la conexión.
> 
> Posteriormente, se retorna a la ventana de Wireshark donde figuran ahora tres paquetes, de los cuales se hace doble click en el último ya que este corresponde al paquete que contiene el mensaje enviado. A continuación, se muestra lo obtenido:

<center>
  <img src="https://hackmd.io/_uploads/Hkdro54sfg.png" width="700">
  <br>
  <em></em>
</center>

> Como se puede observar en la ventana, se resaltó el mensaje enviado (payload), es decir, `Hola!`. Ahora bien, a fin de poder realizar un análisis más detallado del paquete, se procede a desplegar la información del mismo, obteniéndose lo siguiente:

<center>
  <img src="https://hackmd.io/_uploads/HJxW4s4ozg.png" width="700">
  <br>
  <em></em>
</center>

> A partir de la figura anterior se comprueba cómo la información viaja encapsulada a través de las distintas capas del modelo TCP/IP, coincidiendo con los campos teóricos de las cabeceras:
> - **Capa de Acceso a la Red (Null/Loopback):** La captura corresponde a una interfaz de loopback, por lo que no se trata de una trama Ethernet convencional. Indica que se capturó un paquete de 49 bytes totales. 
> 
> - **Capa de Red (Internet Protocol Version 4):** Este encabezado está a cargo del enrutamiento lógico. Se puede observar que tanto la IP de origen (Src) como la de destino (Dst) son `127.0.0.1`, lo cual es correcto ya que el mismo nodo cumple con ambos roles. Asimismo, se puede notar que se indica el protocolo de capa superior encapsulado es TCP (6).
> 
> - **Capa de Transporte (Transmission Control Protocol):** Desplegando esta cabecera, se observan los metadatos que controlan la conexión y que se averiguaron anteriormente, entre ellos podemos observar:
> **Puertos:** Define el puerto de origen dinámico `65002` y el puerto de destino del servidor `64885`.
> **Secuencia y Acuse:** Se observa un Sequence Number: 1 y un Acknowledgment Number: 1 (valores relativos de la sesión).
> **Banderas (Flags):** Están configuradas como 0x018 (PSH, ACK). La bandera PSH solicita que los datos pendientes sean entregados a la aplicación receptora tan pronto como sea posible.
> **Ventana (Window):** El tamaño de la ventana de recepción se indica en `10233`.
> 
> - **Carga Útil (Data / Payload):** Es el mensaje en ASCII transmitido. En la parte inferior se encuentra el campo de datos con una longitud de 5 bytes. Observando la representación hexadecimal de esta carga útil, se identifica la secuencia `48 6f 6c 61 21`, la cual al ser decodificada en ASCII revela la cadena de texto `Hola!`.

> Retornando a la ventana de Wireshark, cabe aclarar que los dos primeros paquetes forman parte del proceso Three-Way Handshake. El motivo por el cual no se visualizan los tres vínculos es debido al filtro aplicado, `tcp.dstport == 64885`, el cual únicamente aísla el tráfico entrante al servidor. Por lo tanto, para poder observar todo el tráfico se cambia el filtro por `tcp.port == 64885` y, ahora, se puede mostrar la siguiente figura con el Three-Way Handshake capturado: 

<center>
  <img src="https://hackmd.io/_uploads/BkYnjcNofg.png" width="700">
  <br>
  <em></em>
</center>
    
**e.** Finalizar la conexión y capturar el Four-way handshake.
> Para concluir la conexión, es decir la transmisión de datos entre cliente y servidor, se cierra la ventana que se abrió automáticamente en el instante en el que se hizo click en `Send`. Con esto se da comienzo al proceso Four-Way Handshake, el mismo fue capturado en Wireshark y se muestra a continuación.

<center>
  <img src="https://hackmd.io/_uploads/rJVznqVsfe.png" width="700">
  <br>
  <em></em>
</center>

> A modo de mostrar la totalidad del tráfico resultante, se presenta la siguiente ventana de Wireshark donde se recuadra en rojo el Three-Way Handshake y en verde el Four-Way Handshake. En el medio, concretamente el paquete N°285, se ubica el paquete enviado de cliente a servidor.

<center>
  <img src="https://hackmd.io/_uploads/rkdwncEoGg.png" width="700">
  <br>
  <em></em>
</center>

**f.** ¿Qué conclusión podemos sacar de que sea tan fácil ver un paquete que viaja a través de la red?
> Lo primero que se puede señalar es que los protocolos base de las capas de Red y Transporte, como IPv4 y TCP, no proporcionan cifrado de los datos de las aplicaciones. Por lo tanto, si una aplicación transmite información utilizando TCP sin utilizar un mecanismo de cifrado adicional, el contenido de los datos puede quedar visible dentro del segmento capturado.
>
> Esta experiencia permite notar la importancia de proteger la información que se transmite a través de redes. Si alguien lograra capturar los paquetes, podría observar diferentes datos de los protocolos utilizados y, si es que a su vez la aplicación no emplea cifrado, incluso podría llegar a leer el contenido de la comunicación. Por este motivo existen protocolos como TLS, SSH o las VPN, que incorporan mecanismos de cifrado para proteger la información transmitida.
> 
> De esta manera, queda evidenciada la necesidad crítica de implementar protocolos de cifrado y seguridad en las capas superiores del modelo OSI antes de transmitir los datos.


---
### Consigna N°4: 
Vamos a iniciar un cliente en packet sender y comunicarnos con el servidor que nos indique el profe (los datos van a estar en el drive compartido). Este será una dirección IP y un puerto para un servicio montado en la nube.

El servidor responderá a comandos que finalicen con la secuencia \r (este es un caracter especial que pueden ingresar en el campo de carga útil ASCII así tal cual, barra invertida erre).

Iniciar una conexión con el servidor y obtener respuestas para comandos admitidos: hola, ping, tic, status.

Capturar toda la sesión de conexión con WireShark. Podés seleccionar la opción “Persistent TCP”:

Para no finalizar la conexión, se abrirá una ventana donde podrás interactuar (cual chat) con el server.

Acá tenés la opción “Append \r” así no tenes que estar poniendo manualmente el caracter cada que envíes mensajes.

Para finalizar el TP: El servidor está configurado para que los nombres de los grupos sean comandos válidos. Iniciar la conexión, enviar el comando correspondiente a su grupo y documentar la respuesta del servidor, tanto en el informe como en la pestaña correspondiente en la planilla compartida de Drive.

> Para esta otra actividad nuevamente se abre una instancia de PacketSender y se procede a llenar los campos de Address y Port con la información del servidor indicado por el profesor, en este caso, `34.136.251.235` y `5555` respectivamente.
>
> Por otro lado, se inició nuevamente una sesión de captura mediante Wireshark, esta vez seleccionando la interfaz de red local (Wi-Fi 2).

<center>
  <img src="https://hackmd.io/_uploads/HyTWFjVife.png" width="700">
  <br>
  <em></em>
</center>

> Posteriormente, se inicia la comunicación con el servidor ingresando los comandos admitidos teniendo en cuenta el agregado del caracter `\r`. Las respuestas obtenidas se muestran en la siguiente ventana:

<center>
  <img src="https://hackmd.io/_uploads/r1cG0vgifl.png" width="700">
  <br>
  <em></em>
</center>

> Asimismo, revisando la ventana de captura de Wireshark se obtuvo el siguiente flujo de paquetes. A partir de las longitudes detalladas en cada uno de ellos, es posible identificar los comandos empleados, por ejemplo en el caso del Paquete N° 1489 presenta un TCP Len de 5 bytes, que contiene el comando `hola` (4 bytes), cabe aclarar que el caracter `\r` (1 byte) también es tenido en cuenta en la longitud. A su vez, el Paquete N° 1490 tiene un TCP Len de 8 bytes, el cual contiene la respuesta `hola :)` (7 bytes) incluyendo el caracter `\r` (1 byte).

<center>
  <img src="https://hackmd.io/_uploads/BJpW3DeiMg.png" width="700">
  <br>
  <em></em>
</center>

> Finalmente, se ingresa el nombre del grupo como comando, `Group Not Found :(\r`. El servidor responde indicando el número de secuencia (SEQ) y la carga útil (PAYLOAD) correspondientes, `8` y `u` respectivamente.

<center>
  <img src="https://hackmd.io/_uploads/H1Sd_DgsMg.png" width="700">
  <br>
  <em></em>
</center>

---
## Conclusiones
A lo largo del presente trabajo se profundizó en el funcionamiento de las capas de enlace, red y transporte, partiendo por el análisis de Ethernet y continuando con los protocolos IP y TCP.

Primeramente, se observó que la capa de enlace permite transportar información entre nodos adyacentes mediante tramas y que Ethernet utiliza direcciones MAC para realizar este direccionamiento dentro del enlace local. Luego, a través de la actividad de Wireshark, fue posible comprobar la diferencia entre este direccionamiento y el direccionamiento lógico proporcionado por IP, observando cómo la dirección MAC identifica el siguiente salto dentro de la red local mientras que las direcciones IP permiten realizar el enrutamiento entre redes.

Posteriormente, se estudió TCP como protocolo orientado a conexión y se estudiaron los mecanismos mediante los cuales proporciona transferencia de datos fiable, control de flujo y control de congestión. Además, al analizar los campos del segmento se pudo comprender cómo los números de secuencia, reconocimientos, ventanas y banderas participan en el funcionamiento del protocolo.

Finalmente, mediante la última actividad, la que implicaba utilizar PacketSender y Wireshark fue posible observar directamente el establecimiento de una conexión TCP (Three-Way Handshake), la transferencia de información y el posterior cierre de la conexión (Four-Way Handshake). Esto permitió relacionar los conceptos teóricos con los paquetes realmente intercambiados entre cliente y servidor y, también, comprender cómo las diferentes capas colaboran para transportar información desde una aplicación hasta el medio de transmisión.

---
## Referencias
- Kurose, J. F., & Ross, K. W. (2017). Redes de computadoras: Un enfoque descendente (7ma ed.). Pearson Educación.
- Tanenbaum, A. S., & Wetherall, D. J. (2012). Redes de computadoras (5.ª ed.). Pearson Educación.
- Forouzan, B. A. (2012). Data Communications and Networking (5th ed.). McGraw-Hill.
- IEEE. IEEE Standard for Ethernet (IEEE 802.3).
