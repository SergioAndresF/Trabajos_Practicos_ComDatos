# Trabajo Práctico N°5

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
En el presente trabajo práctico de laboratorio se tiene como objetivo principal analizar y comprender el funcionamiento de los protocolos fundamentales que operan en las capas de Red y Transporte del modelo TCP/IP. En el mismo se desarrollan actividades que contemplan el uso de herramientas de diagnóstico y del analizador de tráfico Wireshark.

En primer lugar, se estudia el protocolo ICMP y su relación con el enrutamiento IP por medio de la herramienta ping. Seguidamente, se aborda el protocolo ARP, comprendiendo su rol importante en la resolución de direcciones lógicas (IP) a direcciones físicas (MAC) dentro de redes locales. 

En la tercera etapa del laboratorio, se realiza un análisis comparativo de los protocolos de transporte TCP y UDP utilizando la herramienta ncat, permitiendo observar las diferencias entre un modelo orientado a la conexión y uno de mejor esfuerzo. 

Finalmente, la cuarta etapa introduce la programación de sockets en Python, permitiendo vincular directamente las llamadas al sistema operativo (API POSIX) con la generación y recepción de segmentos en la red.

---
## Consignas
### Consigna N°1: 
Empezamos con la herramienta de red más conocida: ping. La vamos a usar como "generador de tráfico" para aprender a leer una captura. Investigar brevemente y documentar en el trabajo:

**a.** ¿Qué es ICMP y para qué se usa? ¿Transporta datos de aplicaciones como lo hacen TCP o UDP?
> El **Protocolo de Mensajes de Control de Internet (ICMP)** es un protocolo central de la capa de red utilizado por hosts y routers para **intercambiar información de control y notificar errores**. Por ejemplo, informar que un host es inalcanzable o que el tiempo de vida de un paquete expiró. 
> 
> Cada tipo de mensaje ICMP se **encapsula en un paquete IP**. A continuación se muestran algunos de los mensajes más importantes.
> 
<center>
  <img src="https://hackmd.io/_uploads/S1ESEngRMl.png" width="600">
  <br>
  <em>Figura 1: Lista de Mensajes ICMP.</em>
</center>

> A diferencia de TCP o UDP, **no transporta datos de aplicaciones**. Su propósito es estrictamente administrativo y de diagnóstico para garantizar la operabilidad de la red misma.

**b.** ¿Qué relación tiene con IP? ¿Viaja dentro de IP, al lado de IP o debajo de IP? ¿Cómo sabe el receptor que el contenido de un paquete IP es ICMP?
> Los mensajes ICMP son transportados como **carga útil de IP**. Ahora bien, con respecto a cómo es reconocido: el sistema operativo receptor sabe que debe procesar ese datagrama como ICMP debido a que examina el **campo Protocol (Protocolo)** del encabezado IP. Si ese campo tiene el valor numérico 1, está indicando que el contenido encapsulado es un mensaje ICMP.

**c.** ¿Qué hace ping? ¿Qué son un Echo Request y un Echo Reply? ¿Qué campos de ICMP permiten distinguirlos?
> El **comando ping** es una herramienta de software que verifica la conectividad a nivel de red entre dos dispositivos y, además, mide el tiempo de ida y vuelta (RTT) de los paquetes.
>
> Este programa genera un mensaje ICMP conocido como **Solicitud de Eco (Eco Request)** dirigido al host especificado como destino. Si el host de destino está encendido y conectado, al ver la solicitud de eco, devuelve una respuesta conocida como **Respuesta de Eco (Eco Reply).**
>
> Estos mensajes se distinguen leyendo el **campo Type (Tipo)** del encabezado ICMP. De acuerdo con la lista mostrada anteriormente, el Echo Request se identifica con el **Tipo 8**, mientras que el Echo Reply se identifica con el **Tipo 0.**

**d.** ¿Qué información mínima contiene un mensaje ICMP de tipo Echo?
> El encabezado base **ocupa 8 bytes** y contiene los siguientes campos:
> 
> - **Tipo (Type)**: Indica el formato del mensaje.
> - **Código (Code)**: Proporciona contexto adicional, por ejemplo, en el caso de los mensajes Echo, toma el valor 0.
> - **Suma de Comprobación (Checksum)**: Permite verificar matemáticamente que el mensaje no se haya corrompido durante la transmisión.
> - **Identificador (Identifier) y Número de Secuencia (Sequence Number)**: Permiten al host origen emparejar ordenadamente cada Request que envió con el Reply correspondiente que recibe. De manera opcional, debajo de estos campos, puede ir un payload con datos arbitrarios de relleno.
> 
<center>
  <img src="https://hackmd.io/_uploads/SJhhO3gAzl.png" width="400">
  <br>
  <em>Figura 2: Estructura ICMP.</em>
</center>

Averiguar la configuración de red de alguna de las computadoras del grupo: dirección IPv4, máscara, gateway por defecto y dirección MAC de la interfaz que usan (Wi-Fi o cableada).
> Para este punto se abre la consola de Windows y se ingresa `ipconfig /all`, obteniéndose lo que se muestra a continuación.

<center>
  <img src="https://hackmd.io/_uploads/H143y7pafx.png" width="700">
  <br>
  <em>Figura 3: Configuración de Red.</em>
</center>

> De la figura anterior se puede identificar lo siguiente:
> - **Dirección IPv4 (Computadora):** `192.168.0.236`
> - **Dirección MAC (Computadora):** `18:4f:32:85:89:cf`
> - **Máscara de Subred:** `255.255.255.0`
> - **Dirección IPv4 (Gateway):** `192.168.0.1` 


Abrir Wireshark, elegir la interfaz por la que salen a Internet (Wi-Fi o Ethernet; la que muestra actividad en el gráfico) y comenzar la captura. En una terminal, hacer ping a la IP del gateway por defecto y luego a una IP de Internet:

<center>
  <img src="https://hackmd.io/_uploads/BJ9Ggmaazx.png" width="400">
  <br>
  <em>Figura 4: Comando Ping hacia IP de Gateway e IP de Internet.</em>
</center>

Detener la captura y aplicar el filtro `icmp`:

<center>
  <img src="https://hackmd.io/_uploads/SJKO2XTTze.png" width="600">
  <br>
  <em>Figura 4: Paquetes capturados.</em>
</center>

Seleccionar un Echo Request y desplegar el panel de detalles (el del medio). Identificar las capas que muestra Wireshark y completar una tabla como esta:
> Para el análisis se selecciona el **Paquete N° 9369** (Ping hacia la IP de Internet):

| Capa | Dirección/Identificador Origen | Dirección/Identificador Destino| ¿Qué campo indica qué protocolo viene dentro?|
| :--- | :--- | :--- | :--- |
| Ethernet II | `18:4f:32:85:89:cf` | `02:10:18:47:0c:b4` | `Type: IPv4 (0x0800)` |
| Internet Protocol Version 4 | `192.168.0.236` | `8.8.8.8` | `Protocol: ICMP (1)` |
| Internet Control Message Protocol | `Identifier (BE): 1 (0x0001)` | `Identifier (BE): 1 (0x0001)` | `Type: Echo (ping) request (8)` |
| Datos/Payload |  |  | `Data (32 bytes)` |

Responder, justificando con la captura (una captura de pantalla con el campo resaltado vale más que el valor copiado):

**a.** La MAC destino del Echo Request enviado a `8.8.8.8`, ¿es la MAC de `8.8.8.8`? ¿De qué equipo es? Compárenla con la MAC destino del ping al gateway. ¿Qué conclusión sacan sobre el alcance de una dirección MAC frente al de una dirección IP?
> Para responder este punto, se seleccionan los **Paquetes N° 8828 y 9369**, los cuales corresponden al resultado de haber realizado ping hacia la direción IP del Gateway y hacia la dirección IP de Internet respectivamente.
> 
<center>
  <img src="https://hackmd.io/_uploads/rkswdVppfx.png" width="800">
  <br>Figura 5: Paquetes capturados y seleccionados.</em>
</center>

> A continuación, se muestra la información detallada de ambos paquetes a fin de compararlos.

<center>
  <img src="https://hackmd.io/_uploads/HJx2PNp6fe.png" width="700">
  <br>
  <em>Figura 6: Paquete N° 9369.</em>
</center>

<center>
  <img src="https://hackmd.io/_uploads/HyMaPVpaGe.png" width="700">
  <br>
  <em>Figura 7: Paquete N°8828.</em>
</center>

> Como se puede observar, en el apartado de la **Capa Ethernet II**, si bien para ambos paquetes se especificaron direcciones IP de destino diferentes (Gateway e Internet), ambos presentan la **misma dirección MAC de destino** (`02:10.18:47:0c:b4`), la cual corresponde a la interfaz del **router local o gateway**. 
> 
> Lo anterior se debe a que, de acuerdo con lo estudiado en los trabajos de laboratorio anteriores, las **direcciones MAC** tienen un **alcance estrictamente local**, es decir, se utilizan únicamente para alcanzar el próximo salto físico. Por otro lado, las **direcciones IP** operan con un **alcance de extremo a extremo**, lo que garantiza el enrutamiento lógico del paquete a través de múltiples redes hasta el destino.

**b.** Comparen un Echo Request con su Echo Reply (Wireshark los vincula en el campo [Response frame:…]). Hagan una lista de los campos que cambian y de los que se mantienen en Ethernet, IP e ICMP. ¿Por qué tiene sentido cada cambio? ¿Por qué el identificador y el número de secuencia se mantienen?
> Para este inciso se estudian los **Paquetes N° 9369 y 9396**. Primeramente se remarcan los campos que son diferentes en ambos paquetes:
<center>
  <img src="https://hackmd.io/_uploads/H1-t5r6pfx.png" width="700">
  <br>
  <em>Figura 8: Información: Paquete N°9369.</em>
</center>

<center>
  <img src="https://hackmd.io/_uploads/H1HqcSapfe.png" width="700">
  <br>
  <em>Figura 9: Información: Paquete N°9396.</em>
</center>

> A partir de lo anterior, se observa lo siguiente:
> - **Direcciones Ethernet e IP:** Las direcciones de origen y destino se invierten. En la **Capa 2**, la MAC de origen pasa a ser la de destino y viceversa. En la **Capa 3**, la IP `8.8.8.8` pasa a ser el origen y `192.168.0.236` el destino. Esto ocurre porque el receptor original es ahora el emisor de la respuesta.
> - **Campos IP:** El **campo TTL (Tiempo de vida) y Header Checksum** cambian, debido a que los routers intermedios recalculan estos valores en el trayecto de vuelta.
> - **Campos ICMP:** El **campo Type** cambia de 8 (Echo Request) a 0 (Echo Reply), modificando la semántica del mensaje.
>
> Ahora, se revisan los campos que se mantienen iguales en ambos paquetes:

<center>
  <img src="https://hackmd.io/_uploads/ByQ498A6Me.png" width="700">
  <br>
  <em>Figura 10: Información: Paquete N°9369.</em>
</center>

<center>
  <img src="https://hackmd.io/_uploads/By4H5IR6Me.png" width="700">
  <br>
  <em>Figura 11: Información: Paquete N°9396.</em>
</center>

> De lo anterior, se observa lo siguiente:
> - **Campos Ethernet:** El **campo Type (Tipo)** es IPv4 en ambos. 
> - **Campos IP:** El **campo Protocol (Protocolo)** es ICMP en ambos.
> - **Campos ICMP:** El **Identifier (0x0001) y el Sequence Number (0x0001)** permanecen intactos. Esto es un requisito del **estándar RFC 792** que le permite al sistema operativo origen (Windows) emparejar inequívocamente la respuesta entrante con la solicitud exacta que emitió, evitando confusiones si hay múltiples pings en curso.

**c.** ¿Dónde está el payload de ping? ¿Cuántos bytes tiene y qué contiene? ¿Es igual en el Reply? Si en el grupo hay una computadora con Windows y otra con Linux, compárenlos: ¿qué les sugiere que sean distintos?
> A continuación, se remarca el **payload o carga útil** de los paquetes estudiados anteriormente, **N° 9369 (Request) y 9396 (Reply)**:
<center>
  <img src="https://hackmd.io/_uploads/rkfxPLRpzx.png" width="700">
  <br>
  <em>Figura 12: Payload Paquete N°9369.</em>
</center>

<center>
  <img src="https://hackmd.io/_uploads/SyETjUR6Ml.png" width="700">
  <br>
  <em>Figura 13: Payload Paquete N°9396.</em>
</center>

> De acuerdo a la figura mostrada del **Paquete N°9369**, el **payload o carga útil** de ping se encuentra al final del datagrama y se encuentra encapsulado dentro de la estructura del protocolo ICMP. Asimismo, se puede observar que ocupa 32 bytes y contiene una secuencia de caracteres alfabéticos de relleno. Si ahora se revisa la figura del **Paquete N°9396**, se puede notar que el contenido devuelto es exactamente igual al enviado.
>
> De manera adicional, se procede a realizar una comparación del payload de ambos sistemas operativos, Windows y Linux. Para ello, se realizan los mismos procedimientos para Windows: iniciar una sesión de captura en Wireshark, enviar un ping a la dirección IP de Internet, finalizar la captura y seleccionar uno de los paquetes capturados. En la siguiente figura se muestra la información del **Paquete N°7368**, el cual corresponde a un Echo Request.

<center>
  <img src="https://hackmd.io/_uploads/rky4PI0aMe.png" width="700">
  <br>
  <em>Figura 14: Payload Paquete N°7346.</em>
</center>

> Haciendo la comparación de la carga útil entre Windows y Linux, lo que se puede notar es que el tamaño y el patrón de datos difieren. De acuerdo con la figura, la carga útil ocupa 40 bytes y contiene una secuencia en hexadecimal que va de 10 a 37. 
> 
> Esto sugiere que el contenido del payload no está estrictamente tipificado por el estándar de red, sino que es simplemente un relleno (padding) de datos arbitrarios inyectado por los desarrolladores del sistema operativo para verificar que la carga útil no sufra corrupción durante la transmisión.

**d.** ¿Qué valor de TTL tiene el Echo Request que ustedes enviaron? ¿Y el Reply que llegó de `8.8.8.8`? ¿Por qué no son iguales? (Pista: investiguen qué hace un router con el TTL.)
> Se recuadran los valores de TTL de los **Paquetes N°9369 y 9396:**

<center>
  <img src="https://hackmd.io/_uploads/BkcVnLAafg.png" width="700">
  <br>
  <em>Figura 15: Payload Paquete N°7346.</em>
</center>

<center>
  <img src="https://hackmd.io/_uploads/H1bthUA6Gx.png" width="700">
  <br>
  <em>Figura 16: Información: Paquete N°7346.</em>
</center>

> Lo que se puede observar es que el **Echo Request** originado por la computadora registra un valor de **Time to Live (TTL)** de 128, el cual corresponde al valor inicial predeterminado por la pila TCP/IP del sistema operativo Windows. Por otro lado, el **Echo Reply** proveniente del servidor de Internet (`8.8.8.8`) presenta un **valor menor**, registrando un TTL de 116.
>
> La razón por la cual estos valores difieren es debido al **mecanismo de seguridad y prevención de bucles** definido en el estándar principal de IPv4 (RFC 791). Esto consiste en que cada router intermedio que procesa un datagrama tiene la obligación arquitectónica de **decrementar el campo TTL en una unidad** antes de conmutarlo hacia el próximo salto. De esta manera, si por algún motivo, un paquete queda atrapado en un bucle de enrutamiento infinito, su TTL eventualmente llegará a 0 y el router lo descartará, evitando el colapso de la red. 
> 
> Por lo tanto, teniendo en cuenta lo anterior, la diferencia entre el TTL inicial con el que el servidor de Internet emitió su respuesta y el valor final registrado en nuestra captura representa la **cantidad exacta de routers intermedios** o, también, la **cantidad de saltos** que el datagrama debió atravesar a través de Internet para regresar a nuestra red local.
> 
<center>
  <img src="https://hackmd.io/_uploads/rJgcTk-RMl.png" width="500">
  <br>
  <em>Figura 17: TTL.</em>
</center>

**e.** Dibujen la encapsulación del paquete que eligieron como "cajas dentro de cajas", indicando para cada caja qué tamaño en bytes tiene según Wireshark.

<center>
  <img src="https://hackmd.io/_uploads/rkd1fwAafl.png" width="400">
  <br>
  <em>Figura 18: Encapsulación Paquete.</em>
</center>

---
### Consigna N°2: 
En el punto anterior la trama Ethernet ya tenía una MAC destino. Pero ping solo conoce una IP. ¿De dónde salió esa MAC? Investigar brevemente:

**a.** ¿Qué problema resuelve ARP? ¿En qué capa lo ubicarían y por qué es discutible?
> El **Protocolo de Resolución de Direcciones (ARP)** resuelve el problema de mapear o traducir una dirección lógica de red (dirección IPv4) a una dirección física de hardware (dirección MAC) dentro de una misma red de área local (LAN).
>
> Con respecto a su ubicación en el Modelo OSI, resulta ser frecuentemente motivo de debate debido a que opera en la frontera entre dos capas. Por una parte, su función se considera un protocolo auxiliar de la Capa 3 (Red), ya que asiste directamente al protocolo IP para lograr el enrutamiento local. Sin embargo, por otra parte, los mensajes ARP no se encapsulan dentro de datagramas IP, sino que viajan directamente sobre tramas Ethernet y, por lo tanto, muchos arquitectos de redes lo ubican en la Capa 2 (Enlace).

**b.** ¿Qué es un ARP Request y un ARP Reply? ¿A quién se envía cada uno?
> Un **ARP Request (Solicitud)** es un **mensaje de interrogación** que un host inyecta en la red preguntando: "¿Quién tiene asignada esta IP? Por favor, envíeme su MAC asociada". Este mensaje **se envía por difusión (Broadcast)** hacia la dirección MAC `ff:ff:ff:ff:ff:ff`, lo que obliga a todos los switches a replicarlo y a todos los nodos del segmento a procesarlo.
>
> Por su parte, un **ARP Reply (Respuesta)** es la **contestación** emitida por la interfaz de red que posee la IP en cuestión, informando su dirección MAC física. Este mensaje **se envía de forma directa (Unicast)** únicamente hacia la dirección MAC del host que originó la consulta, de esta manera, se evita saturar a los demás equipos de la red.
> 
<center>
  <img src="https://hackmd.io/_uploads/rkMZ7lbCGx.png" width="500">
  <br>
  <em>Figura 19: ARP Request y ARP Reply.</em>
</center>

**c.** ¿Qué es la caché ARP y por qué existe?
> La **caché ARP o tabla ARP** es una estructura de datos dinámica alojada en la memoria de cada host o router, la cual **almacena de manera temporal** los mapeos recientes entre direcciones IP y MAC. Con respecto al tiempo típico de caducidad de una entrada, este resulta ser de 20 minutos desde el momento que se incluye la entrada en la tabla ARP.
> 
> Ahora bien, esta tabla surge por una **cuestión de eficiencia de red** debido a que evita que los hosts inunden el medio compartido con constantes ARP Requests cada vez que necesitan transmitir un datagrama, recordando que estos mensajes son de difusión (Broadcast). En ese sentido, al guardar las resoluciones recientes en una caché, se ahorra ancho de banda, se reduce la carga de procesamiento en los demás hosts y se minimiza la latencia en el envío de los paquetes.

<center>
  <img src="https://hackmd.io/_uploads/rkTo4gZ0Me.png" width="400">
  <br>
  <em>Figura 20: Caché ARP.</em>
</center>

**d.** Traten de responder con sus palabras: "Tengo la IP de una máquina de mi red local. ¿Cómo sé a qué dirección MAC debo enviarle la trama?"
> Para poder enviar una trama a una IP local, primero se consulta la propia **caché ARP interna**. En el caso de que la dirección IP ya se encuentre registrada allí junto con una dirección MAC, se arma la trama Ethernet y se transmite inmediatamente. Si por el contrario la IP no figura en la tabla, el **paquete IP es retenido o puesto en pausa** y se envía un mensaje a toda la red, es decir, se envía la **ARP Request** preguntando por el nodo asociado a la IP en cuestión. 
> 
> Posteriormente, cuando el dispositivo correspondiente contesta con su dirección MAC, es decir, la **ARP Reply**, la misma es anotada en la caché ARP. Finalmente, una vez obtenida dicha dirección MAC, la misma es insertada como destino en el encabezado de la trama que había sido retenida, para luego, enviarla hacia la red física.

**e.** Ver la caché ARP de su computadora y buscar la entrada del gateway. ¿La MAC asociada al gateway coincide con la MAC destino que vieron anteriormente?
> Para consultar la **tabla ARP**, se ejecuta el comando `arp -a` en la **terminal de Windows**. A continuación, se muestra una imagen de lo obtenido:
> 
<center>
  <img src="https://hackmd.io/_uploads/Bym6ED06Gx.png" width="800">
  <br>
  <em>Figura 21: Caché ARP Computadora.</em>
</center>

> Ahora, se procede a buscar la dirección IPv4 correspondiente al Gateway, la cual es `192.168.0.1`. Se observa que la misma se encuentra en la 1ra fila de la caché y está asociada a la dirección física `02:10:18:47:0c:b4`. Esta dirección coincide con la MAC de destino registrada en el análisis de Wireshark de la Consigna 1.

**f.** Generar tráfico ARP y capturarlo. Capturen en la interfaz Wi-Fi/Ethernet con el filtro arp. Como las entradas quedan guardadas en la caché, un ping a un equipo con el que ya hablaron puede no generar ningún ARP. Tienen varias formas de provocarlo (elijan la que puedan usar):
> Para este punto se utiliza otro equipo conectado a la misma red, cabe aclarar que el sistema operativo de este equipo es Linux. En primera instancia, se necesita conocer la dirección IP y MAC del mismo, para ello, se abre la terminal de Linux y se ingresan los comandos `ip addr` y `ip route`, obteniéndose lo siguiente:
> 
<center>
  <img src="https://hackmd.io/_uploads/HJatnPATMe.png" width="700">
  <br>
  <em>Figura 22: Información de Red 2do Equipo.</em>
</center>

> De lo anterior se tiene que:
> - **Dirección IP:** `192.168.0.55`
> - **Dirección MAC:** `1c:ce:51:67:e2:c3`

> Habiendo identificado la dirección IP de este equipo, se retorna al equipo inicial y desde este mismo se realiza el comando ping tomando como host de destino la dirección IP obtenida. Posteriormente, se consulta nuevamente la tabla ARP mediante `arp -a` para observar si hubo modificaciones.
> 
<center>
  <img src="https://hackmd.io/_uploads/Hkw-aD0pMe.png" width="700">
  <br>
  <em>Figura 23: Comando Ping hacia IP de 2do Equipo y Caché ARP.</em>
</center>

> De la figura anterior, queda evidenciado que se agregó una entrada a la tabla ARP, cuya dirección IP y MAC coinciden con las correspondientes del 2do equipo utilizado para esta experiencia.

Analizar un ARP Request y su ARP Reply. Para cada uno completar una tabla como la siguiente:
> Durante el procedimiento anterior, estuvo activada la **sesión de captura de Wireshark**, a continuación, se muestran los paquetes de protocolo ARP capturados:
> 
<center>
  <img src="https://hackmd.io/_uploads/B1BYpw0azl.png" width="800">
  <br>
  <em>Figura 24: Paquetes de Protocolo ARP.</em>
</center>

> En esta figura se recuadran los paquetes correspondientes a **ARP Request (N°5214) y ARP Reply (N°5262)**, estos paquetes son los que se van a estudiar y en las siguientes figuras se presenta el detalle de cada uno:

<center>
  <img src="https://hackmd.io/_uploads/SyyNYOAazx.png" width="700">
  <br>
  <em>Figura 25: Información: ARP Request.</em>
</center>

<center>
  <img src="https://hackmd.io/_uploads/r1AuKO06Me.png" width="700">
  <br>
  <em>Figura 26: Información: ARP Reply.</em>
</center>

> A partir de esta información, se completa la siguiente tabla:

| Campo | ARP Request | ARP Reply |
| :--- | :--- | :--- |
| MAC Destino (Encabezado Ethernet) | `ff:ff:ff:ff:ff:ff` | `18:4f:32:85:89:cf` | 
| MAC Origen (Encabezado Ethernet) | `18:4f:32:85:89:cf` | `1c:ce:51:67:e2:c3` |
| Opcode | `request (1)` | `reply (2)` |
| Sender MAC Address | `18:4f:32:85:89:cf` | `1c:ce:51:67:e2:c3` | 
| Sender IP Address | `192.168.0.236` | `192.168.0.55` | 
| Target MAC Address | `00:00:00:00:00:00` | `18:4f:32:85:89:cf` | 
| Target IP Address | `192.168.0.55` | `192.168.0.236` | 

**a.** ¿Por qué el Request va a una dirección broadcast y el Reply no? ¿Qué valor tiene Target MAC address en el Request y por qué?
> El mensaje **ARP Request** se envía a una dirección física de Broadcast, `ff:ff:ff:ff:ff:ff`, porque el equipo emisor desconoce la dirección MAC donde se encuentra el equipo destinatario en la red local. Al usar difusión o broadcast, los switches replican la trama y, de esta manera, se garantiza que todos los hosts conectados a la red reciban y evalúen la consulta del equipo emisor. 
> 
> En cambio, el **ARP Reply** se envía de forma Unicast, es decir, directamente a la MAC del solicitante, porque el equipo que responde ya conoce la dirección física del equipo emisor, la obtuvo al inspeccionar el Request entrante y, así, se evita generar tráfico innecesario para el resto de los equipos de la red.
>
> Ahora bien, con respecto al **campo Target MAC** del paquete correspondiente a **ARP Request**, el mismo adopta el valor `00:00:00:00:00:00`. Esto tiene una razón arquitectónica, ya que ese campo representa justamente la dirección física que el protocolo intenta resolver, en ese sentido, al no tener el dato de destino todavía, **se rellena con un valor nulo.**

**b.** En el encabezado Ethernet de la trama ARP, ¿qué valor tiene el campo Type? ¿Hay un encabezado IP? ¿Qué les dice eso sobre dónde "vive" ARP?
> De acuerdo con lo que muestra la Figura 25, en el **encabezado Ethernet**, el **campo Type** tiene el valor hexadecimal `0x0806`, el cual es utilizado para identificar cargas útiles correspondientes al **protocolo ARP**. De esta manera, se comprueba que **no hay un encabezado IP** presente en el paquete. 
> 
> A raíz de lo anterior, se puede decir que la trama ARP **no utiliza el protocolo IP (Capa 3)** para transportarse, sino que viaja encapsulada directamente como **carga útil** de la trama Ethernet (Capa 2), lo que demuestra que es un protocolo de soporte enfocado en la red local física. En ese sentido, queda evidenciado que ARP opera justo en la **frontera entre la Capa 2 y la Capa 3.**

**c.** Con la Opción A (IP inexistente): ¿cuántos ARP Request aparecieron? ¿Hubo Reply? ¿Apareció algún ICMP Echo Request en la captura? Expliquen por qué.
> Para este inciso, se ejecutó el comando ping hacia una direccion IP inexistente, se tomó la dirección `192.168.0.250`. 
> 
<center>
  <img src="https://hackmd.io/_uploads/Sy9NtoAaGg.png" width="700">
  <br>
  <em>Figura 27: Ping hacia IP inexistente.</em>
</center>

> Revisando los paquetes capturados en Wireshark, se puede observar a través de la siguiente figura que, al consultar una IP inexistente, se produjeron **múltiples paquetes ARP Request** de sondeo, pero no hubo ningún **ARP Reply**, y esto es debido a que no existe ninguna interfaz de red activa en el segmento que se adjudique dicha dirección IP.
>
<center>
  <img src="https://hackmd.io/_uploads/HyyFqj0Tfe.png" width="700">
  <br>
  <em>Figura 28: Paquetes ARP Request.</em>
</center>

> Por otro lado, si se aplica el filtro `arp || icmp` se puede notar que tampoco aparece ningún **ICMP Echo Request** en la captura. El motivo se encuentra en el bloqueo de encapsulación, y es que al **fallar la resolución ARP**, la computadora jamás pudo conocer la MAC de destino. Entonces, sin esa dirección física, resultó **imposible construir el encabezado de la trama Ethernet** y, por consiguiente, el paquete ICMP nunca abandonó la memoria de la PC hacia el medio físico y fue descartado internamente por el sistema operativo.

**d.** Volvieron a hacer ping al mismo destino un minuto después: ¿apareció ARP de nuevo? Revisen la caché ARP. ¿Qué ventaja tiene la caché y qué problema podría causar si una entrada quedara vieja?
> Al repetir el comando ping hacia el mismo destino, **no apareció nuevo tráfico ARP** en la captura. Esto se debe a que el sistema operativo almacenó temporalmente la asociación en su caché ARP local durante el primer intercambio.
>
> Lo anterior tiene como ventaja proporcionar **gran eficiencia de red** puesto que se evita saturar el medio compartido con mensajes repetitivos de Broadcast, se reduce la carga de procesamiento en las tarjetas de red de los demás hosts y se logra minimizar drásticamente la latencia en las comunicaciones subsecuentes.
>
> Sin embargo, también surge un problema importante, el cual está asociado a una **entrada vieja.** Lo que puede ocurrir es que el host de destino original **cambie su hardware**, como por ejemplo, debido a un cambio de placa de red, o también, puede suceder que su **IP sea reasignada** por un servidor DHCP a un equipo diferente. Independientemente del caso, la caché ARP interna estaría apuntando a una dirección obsoleta o desactualizada y, en consecuencia, las tramas Ethernet se enviarían a un **dispositivo incorrecto o inexistente**, dando lugar a la **pérdida total de paquetes** hasta que el registro en la caché caduque y el sistema se vea forzado a emitir un **nuevo ARP Request.**

---
### Consigna N°3: 

Hasta ahora observamos protocolos que usa el sistema operativo. Ahora vamos a comunicar dos procesos (dos programas) sin escribir código todavía. ncat es un programa que toma lo que escribimos en el teclado y lo manda por la red (y viceversa). La idea es empezar a generar tráfico cada vez más a bajo nivel (primero generamos tráfico con Packet Tracer, luego con la terminal del SO, ahora con un software a través de la CLI y finalmente ejecutaremos algunos scripts). Descargar netcat! para linux es bastante directo.

Investigar brevemente:

**a.** ¿Qué significa "establecer una conexión"? ¿Dónde "existe" una conexión TCP: en los cables, en los routers o en los extremos?
> El **"Establecer una conexión"** implica un acuerdo previo entre dos procesos, donde uno es el cliente y el otro es el servidor. Por medio de este acuerdo se sincronizan parámetros de comunicación, como los números de secuencia iniciales, y se reservan recursos de memoria, como los búferes de transmisión y recepción, antes de intercambiar el primer byte de datos útiles. Este proceso de tres pasos se conoce como **Three-Way Handshake**.

<center>
  <img src="https://hackmd.io/_uploads/H1C8ugGRGe.png" width="400">
  <br>
  <em>Figura 29: Three-Way Handshake.</em>
</center>

> Una conexión TCP es un estado puramente lógico y se efectúa de manera exclusiva en los sistemas finales, además, está almacenada en las estructuras de datos de sus respectivos sistemas operativos. En el medio físico y en los dispositivos intermedios del núcleo de la red, ya sea routers o switches, la conexión TCP es completamente inexistente e invisible. Resulta conveniente recordar que estos equipos intermedios operan en la Capa de Red (Capa 3) y se limitan a conmutar datagramas IP de manera independiente, por lo que ignoran completamente que esos paquetes forman parte de una "conexión" de nivel superior.
> 

**b.** ¿Qué es un puerto? ¿Qué identifica el par (IP, puerto)?
> Un **puerto** es un **identificador lógico numérico de 16 bits**, que puede ir de 0 a 65535, y opera en la **Capa de Transporte**. Su función es permitir la **multiplexación y demultiplexación del tráfico**, es decir, permite que el sistema operativo distribuya correctamente los paquetes de red entrantes hacia la aplicación específica a la que van dirigidos, lo que posibilita que múltiples programas utilicen la red simultáneamente.

> Con respecto al par compuesto por una dirección IP y un número de puerto (IP:Puerto), este es denominado formalmente **Socket (conector)**. De acuerdo con el **estándar del protocolo (RFC 793)**, este par identifica de forma única el punto final de una comunicación a nivel mundial. El proceso consiste en lo siguiente: la **IP** se encarga de que el paquete llegue a la computadora correcta a través de Internet, y el **puerto** asegura que, una vez dentro de la computadora, los datos vayan al programa correcto.
> 
<center>
  <img src="https://hackmd.io/_uploads/SylSy_eGAGe.png" width="600">
  <br>
  <em>Figura 30: Socket.</em>
</center>

**c.** ¿Qué significa que un proceso esté "escuchando" en un puerto?
> Significa que una aplicación le **solicitó formalmente** al sistema operativo que reserve un **número de puerto específico** para su uso exclusivo. A partir de ese momento, el programa queda **inactivo o bloqueado**, suspendiendo su actividad a la espera de eventos de la red. 
> 
> De esta manera, cuando el sistema operativo recibe desde la placa de red un **paquete entrante** cuyo destino coincide con ese número de puerto, que puede ser, por ejemplo, una solicitud de conexión de un cliente, intercepta el mensaje, desbloquea al proceso correspondiente y le entrega los datos para que inicie la comunicación.

Importante: capturar en loopback. En esta parte cliente y servidor corren en la misma computadora y se comunican por 127.0.0.1 o localhost. Ese tráfico no sale por la placa Wi-Fi: en Wireshark hay que elegir la interfaz de loopback.

Van a notar que, según el sistema operativo, la captura en loopback no muestra un encabezado Ethernet o lo muestra con MAC `00:00:00:00:00:00`.

Experimento TCP. Iniciar la captura en loopback con el filtro `tcp.port == 12000`. Abrir dos terminales:

Escriban una línea en la terminal B y presionen Enter; luego respondan desde la A. Manden 2 o 3 mensajes en cada sentido. Finalmente cierren el cliente (Ctrl+C en B) y detengan la captura. Capturen el paquete con Wireshark, recuerden filtrar con `tcp.port == 12000` así no se les hace una ensalada de paquetes en el sniffer.
> Para el desarrollo de esta experiencia, se abren **dos terminales de Windows**, una adopta el rol de cliente y la otra el de servidor. En la **Terminal A (Servidor)** se ingresa el comando `ncat -v -l 12000`, mediante el cual se pone en estado de escucha al **puerto 12000**. Luego, en la **Terminal B (Cliente)** se ejecuta `ncat -v 127.0.0.1 12000` para establecer una conexión con el **puerto 12000.**
>
> Posteriormente, se procede con el **intercambio de mensajes** por medio de los terminales A y B como se muestra en la siguiente figura. En la misma, se puede notar que se envió un total de 4 mensajes.

<center>
  <img src="https://hackmd.io/_uploads/BkJycaA6Ge.png" width="800">
  <br>
  <em>Figura 31: Comunicación Protocolo TCP.</em>
</center>

> Previo a la comunicación, se abrió una **sesión de captura en Wireshark**, de la cual se obtuvo lo siguiente, filtrando aquellos paquetes con el campo `tcp.port == 12000`:

<center>
  <img src="https://hackmd.io/_uploads/Hkb-qT0TGx.png" width="700">
  <br>
  <em>Figura 32: Paquetes TCP.</em>
</center>

> De la figura anterior, se puede observar que existen 4 paquetes con la flag `[PSH, ACK]`, los cuales corresponden a los **mensajes enviados** durante la comunicación. Asimismo, se puede apreciar los procesos de comienzo y finalización de dicha comunicación, los cuales son característicos del protocolo TCP, estos son **Three-Way Handshake y Four-Way Handshake** respectivamente.

Experimento UDP. Nueva captura en loopback, ahora con el filtro `udp.port == 12001`:

Envíen mensajes en ambos sentidos (el servidor puede responder una vez que recibió el primer datagrama del cliente) y cierren con Ctrl+C.
> Para esta otra experiencia, se emplea el **protocolo UDP**, el cual prioriza una **comunicación rápida y ligera**, por lo tanto, para elminar esas demoras, no establece una conexión previa ni espera confirmaciones de recepción como ocurre en el **protocolo TCP.**
>
> Nuevamente, se **abren dos terminales de Windows**, cada una con su rol de cliente y servidor. En la **Terminal A (Servidor)** se ejecuta `ncat -v -u -l 12001`, a través del cual se pone en estado de escucha al **puerto 12001.** Luego, en la **Terminal B (Cliente)** se ingresa la línea `ncat -v -u 127.0.0.1 12001` para establecer la conexión con el puerto en cuestión.
> 
> Seguidamente, de manera análoga a la experiencia con TCP, se realiza el **intercambio de mensajes entre ambos procesos**, enviándose un total de 4 mensajes.
> 
<center>
  <img src="https://hackmd.io/_uploads/SkKEwieCGl.png" width="800">
  <br>
  <em>Figura 31: Comunicación Protocolo UDP.</em>
</center>

> A continuación, se muestran los paquetes capturados correspondientes al protocolo UDP aplicando el filtro `udp.port == 12001`:

<center>
  <img src="https://hackmd.io/_uploads/ByCSvsx0zx.png" width="800">
  <br>
  <em>Figura 32: Paquetes UDP.</em>
</center>

> En la figura se puede observar que **existen mucho menos paquetes** que en el protocolo TCP. Estos paquetes corresponden a los mensajes enviados, los cuales fueron 4 en total. 

**a.** ¿Qué pasó en la red cuando ejecutaron el comando del cliente, antes de escribir el primer mensaje? Compárenlo con TCP
> Lo que resalta inmediatamente es que el **protocolo UDP** no generó absolutamente **ningún tráfico en la red**. Esto se debe a que UDP es un **protocolo no orientado a la conexión**, no requiere preparación previa ni reserva de recursos entre los hosts. En contraste, al ejecutar el **cliente TCP**, la captura mostró el intercambio inmediato de tres paquetes: `SYN`, `SYN-ACK`, `ACK`. Estos paquetes son los correspondientes al **Three-Way Handshake** necesario para establecer el estado lógico de la conexión antes de poder transmitir el primer byte de datos útiles.

<center>
  <img src="https://hackmd.io/_uploads/SymGHXMRfe.png" width="800">
  <br>
  <em>Figura 33: Three-Way Handshake Protocolo TCP.</em>
</center>

**b.** ¿Cuántos datagramas generó cada mensaje? ¿Hay algo parecido a un ACK?
> Cada mensaje enviado mediante UDP generó exactamente **un datagrama**. Asimismo, al analizar la captura mostrada en la Figura 32, se comprueba que no existe **ningún paquete de confirmación (ACK)** por parte del receptor en la capa de transporte. Esto refuerza el concepto de que UDP opera bajo un modelo de best-effort, enviando la información sin esperar, ni requerir, un acuse de recibo para validar que el servidor recibió el paquete.

**c.** Comparen el encabezado UDP con el encabezado TCP de un segmento con datos: ¿qué campos tiene cada uno? ¿Cuántos bytes ocupa cada encabezado?
> Analizando los paneles de detalle de Wireshark para ambos protocolos, se tiene lo siguiente. A simple vista, el encabezado UDP es bastante ligero y el encabezado TCP es significativamente más complejo:

<center>
  <img src="https://hackmd.io/_uploads/Hybncsg0Me.png" width="800">
  <br>
  <em>Figura 34: Encabezados: TCP y UDP.</em>
</center>

> Se observa que:
> - **Encabezado UDP:** Ocupa **8 bytes** y contiene únicamente **4 campos**: Puerto de Origen, Puerto de Destino, Longitud Total y Suma de Comprobación (Checksum).
> - **Encabezado TCP:** Ocupa un mínimo de **20 bytes**, sin incluir las opciones. Se puede observar que, además de los puertos y el checksum, **incorpora campos vitales** para gestionar la transmisión, los cuales fueron estudiados en su momento en un trabajo de laboratorio anterior: Número de Secuencia, Número de Acuse de Recibo (Acknowledgment Number), Longitud del Encabezado, Banderas de control (Flags: `SYN`, `FIN`, `ACK`, `PSH`, `RST`, `URG`), Tamaño de Ventana (Window Size para control de flujo) y Puntero de Urgencia.

<center>
  <img src="https://hackmd.io/_uploads/SyVX5EMRfx.png" width="600">
  <br>
  <em>Figura 35: Diferencias Encabezados: TCP y UDP.</em>
</center>

**d.** ¿Qué pasó en la red al cerrar el cliente con `Ctrl+C`? ¿Y en TCP?
> En la **experiencia con UDP**, al interrumpir el proceso del cliente con `Ctrl+C`, no se generó ningún paquete en la red. El programa finalizó localmente de manera abrupta **sin notificar al servidor**. 
> 
> Por el contrario, en la **experiencia con TCP**, esta misma acción inició un **procedimiento ordenado** de cierre de conexión, conocido como **Four-Way Handshake**. Esto quedó evidenciado en Wireshark por el envío de segmentos con la **flag `[FIN, ACK]`**, seguidos de sus respectivas **confirmaciones `[ACK]`**, garantizando la correcta liberación de búferes y puertos en ambos sistemas operativos.
> 
<center>
  <img src="https://hackmd.io/_uploads/Sy0n5VGAze.png" width="800">
  <br>
  <em>Figura 36: Four-Way Handshake Protocolo TCP.</em>
</center>

**e.** Para enviar la misma frase, ¿cuántos paquetes necesitaron en total con TCP y cuántos con UDP? ¿Qué "compran" con los paquetes extra de TCP?
> En el **caso con UDP** se requirió **solamente 1 paquete**, el cual corresponde al datagrama que transportaba la carga útil o payload.
>
> En cambio, **con TCP** se necesitaron **múltiples paquetes**, usualmente entre 8 y 9 en total para una sesión completa. Esto debido a que se incluyen 3 paquetes para establecer la **conexión inicial**, 2 paquetes para **enviar el mensaje y confirmar su recepción**, y entre 3 y 4 paquetes adicionales para el **cierre ordenado de la sesión**.
>
> Ahora bien, los **paquetes adicionales de TCP** generan **confiabilidad**, es decir, garantizan que la información llegue **sin errores** y de **forma completa**, sin duplicados y en el **orden riguroso** en que fue enviada. Además, **habilitan** mecanismos de **Control de Flujo**, para no desbordar la memoria del receptor, y **Control de Congestión**, para no colapsar los routers intermedios de la red.

**f.** ¿Y si nadie escucha? Con Wireshark capturando en loopback y el filtro `tcp.port == 12000 || udp.port == 12001 || icmp`, sin servidores corriendo:
> En este punto se pide que los **servidores estén cerrados**. En ese sentido, se utiliza únicamente la terminal del cliente a través de la cual se va a intentar establecer una conexión con los servidores y observar qué sucede.
>
> Para ello, se ejecutan las líneas que se trabajaron anteriormente:
`ncat -4 -n -v 127.0.0.1 12000` y `ncat -4 -n -v -u 127.0.0.1 12001`

<center>
  <img src="https://hackmd.io/_uploads/SJMPCSM0fx.png" width="800">
  <br>
  <em>Figura 37: Terminal del Cliente.</em>
</center>

> Lo que se puede mostrar como diferencia es que en el caso del protocolo UDP, no se detecta la falla hasta que se escribe un mensaje para enviar, lo que pone en evidencia su característica de no estar oriendado a la conexión.
> 
> Pasando ahora a revisar los paquetes capturados, se tiene lo siguiente:
> 
<center>
  <img src="https://hackmd.io/_uploads/SkeR0SfRGe.png" width="800">
  <br>
  <em>Figura 38: Paquetes Capturados.</em>
</center>

> De la figura anterior, comparando lo ocurrido con cada protocolo, se puede observar que:
> - **Comportamiento en TCP:** Al intentar establecer una conexión hacia el puerto 12000, recordando que el mismo no se encuentra en modo escucha, se puede notar que el cliente envía su paquete inicial de sincronización `[SYN]`. Sin embargo, el sistema operativo receptor detecta la ausencia de una aplicación destinataria y responde activamente **abortando el Three-Way Handshake**. Para ello, devuelve un segmento TCP con las **flags `[RST, ACK]`**, lo que provoca que el cliente **cierre la conexión** de manera instantánea.
> - **Comportamiento en UDP:** Al enviar un datagrama al puerto 12001, la terminal del cliente **no arroja ningún error visible**, recordando que este protocolo no está orientado a la conexión. Sin embargo, a nivel de red, el sistema operativo receptor descubre que no hay ninguna aplicación asociada a ese puerto para entregarle la carga útil. Entonces, dado que el encabezado UDP **carece de banderas de control** para notificar el rechazo, el sistema operativo recurre a la Capa de Red, devolviendo al emisor un **mensaje ICMP de tipo Destination Unreachable (Port unreachable / Puerto inalcanzable).**

---
### Consigna N°4: 

Un socket es el "punto final" de una comunicación que el sistema operativo le entrega a un programa: el programa escribe y lee bytes en el socket, y el sistema operativo se ocupa de TCP/UDP, IP y la placa de red. No vamos a entrar en tanta teoría acá, ya está bastante pesado el TP. A programar.

Ahora hacemos nosotros lo que hacía ncat. Los scripts están resueltos para que puedan concentrarse en relacionar cada línea con lo que ocurre en la red.

**a.** Leer el código del servidor:
> 

<center>
  <img src="https://hackmd.io/_uploads/Hk4W8UMAfx.png" width="500">
  <br>
  <em></em>
</center>

<center>
  <img src="https://hackmd.io/_uploads/SJAfI8MRGl.png" width="500">
  <br>
  <em>Figura 39: Código Python Servidor.</em>
</center>


**b.** Leer el código del cliente:
> 

<center>
  <img src="https://hackmd.io/_uploads/rJwwLIfRzl.png" width="600">
  <br>
  <em></em>
</center>

<center>
  <img src="https://hackmd.io/_uploads/rkzd88GRfg.png" width="600">
  <br>
  <em>Figura 40: Código Python Cliente.</em>
</center>

**c.** Ejecutar (capturando en loopback con el filtro tcp.port == 12000):
> Una vez descargados los códigos de servidor y cliente, se abren dos terminales, luego, siguiendo la misma dinámica, se asigna a cada uno un rol y se ejecutan los códigos de acuerdo a dicha asignación. Para esta experiencia se trabaja en el sistema operativo de Linux. El resultado se muestra a continuación:
<center>
  <img src="https://hackmd.io/_uploads/Byx9dwfCzx.png" width="800">
  <br>
  <em>Figura 41: Comunicación.</em>
</center>

> Como se observa en la figura, la ejecución fue exitosa. El servidor aceptó la solicitud de conexión proveniente de la interfaz local y del puerto asignado dinámicamente al cliente por el kernel de Linux, que en esta ejecución particular, el puerto 53224. Y, además, se confirma la correcta transferencia en ambos extremos de la carga útil y el posterior cierre ordenado de la sesión iniciado por el cliente.
> 
> Asimismo, se realizó la captura de los paquetes durante la comunicación entre cliente y servidor:
<center>
  <img src="https://hackmd.io/_uploads/rkwGKwf0Gl.png" width="800">
  <br>
  <em>Figura 42: Paquetes Capturados.</em>
</center>

> 

**d.** Con la captura, completar una tabla como la siguiente. Para cada llamada, indicar si genera tráfico y, si lo genera, qué segmentos (número de paquete en Wireshark y flags):
> 


| Llamada | ¿Dónde se ejecuta? | ¿Genera tráfico? | Segmentos que observan |
| :--- | :--- | :--- | :--- |
| socket() | servidor y cliente | No | Operación local en memoria |
| bind() | servidor | No | Asociación lógica interna, sin tráfico de red |
| listen() | servidor | No | Cambio de estado pasivo dentro del SO |
| connect() | cliente | Sí | Paquetes 37 `[SYN]`, 38 `[SYN, ACK]` y 39 `[ACK]` (Three-Way Handshake) | 
| accept() | servidor | No | El SO le entrega la conexión ya establecida al programa |
| sendall() | servidor | Sí | Paquete 40 `[PSH, ACK]` (envío del cliente) y Paquete 42 `[PSH, ACK]` (respuesta del servidor) |
| recv() | servidor | Sí (indirectamente) | Paquete 41 `[ACK]` (el SO del servidor confirma recepción) y Paquete 43 `[ACK]` (el SO del cliente confirma recepción) |
| close() | ambos | Sí | Paquetes 44 `[FIN, ACK]`, 45 `[FIN, ACK]` y 46 `[ACK]` (Connection Teardown) |


---
## Conclusiones
A través de este trabajo práctico se aplicaron los conceptos teóricos fundamentales de la arquitectura TCP/IP. A modo de resumir lo realizado:

- En la Capa de Red se corroboró que ICMP actúa como un mecanismo de control y diagnóstico, evidenciando, por ejemplo, cómo la expiración del campo TTL en los routers previene bucles infinitos de enrutamiento. Asimismo, el análisis del protocolo ARP demostró la necesidad de resolver direcciones lógicas a físicas mediante mensajes de difusión (Broadcast) antes de que cualquier datagrama pueda ser encapsulado en una trama Ethernet y transmitido al medio local.
- En la Capa de Transporte La comparación directa entre TCP y UDP permitió poner en evidencia sus diferencias arquitectónicas. Por un lado, UDP prioriza la velocidad, y para ello, omite la retención de estado y el acuse de recibo. Por otro lado, TCP garantiza una entrega confiable y ordenada mediante el establecimiento previo de una sesión (Three-Way Handshake), el control de la transmisión (Flags y Window Size) y el cierre estructurado (Four-Way Handshake). Además, se pudo observar cómo ambos manejan las excepciones de puertos cerrados de manera distinta: en el caso de UDP, apoyándose en mensajes ICMP de la capa inferior y en el caso de TCP, en sus propias banderas de control (RST).
- Finalmente, en relación con la Interfaz de Programación (Sockets), la implementación de un cliente y servidor en Python permitió desmitificar la abstracción del sistema operativo. Se logró identificar qué instrucciones de código desencadenan tráfico real en la red, como por ejemplo, connect() o close(), y cuáles son simples configuraciones locales de memoria, como bind() o listen(), consolidándose así la comprensión del flujo completo de datos desde la aplicación del usuario hasta el medio físico.

---
## Referencias
- Kurose, J. F., & Ross, K. W. (2021). Computer networking: A top-down approach (8va ed.). Pearson.
- Tanenbaum, A. S., Feamster, N., & Wetherall, D. J. (2021). Computer networks (6ta ed.). Pearson.
- Postel, J. (1980). User datagram protocol (RFC 768). Internet Engineering Task Force. https://doi.org/10.17487/RFC0768
- Postel, J. (1981). Transmission control protocol (RFC 793). Internet Engineering Task Force. https://doi.org/10.17487/RFC0793
- Python Software Foundation. (2023). socket — Low-level networking interface. Python 3 Documentation. https://docs.python.org/3/library/socket.html
