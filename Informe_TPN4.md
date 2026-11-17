# Trabajo Práctico N°4

### Asignatura: Comunicaciones de Datos

**Facultad de Ciencias Exactas, Físicas y Naturales (UNC)**

---

- **Grupo:** Group Not Found :(
- **Profesores:** Miguel Angel Solinas y Santiago Martin Henn

---

### Integrante y Contacto

| Nombre y Apellido | Correo Electrónico |
| :--- | :--- |
| **Sergio Andrés Fernández Segovia** | _sergio.fernandez.segovia@mi.unc.edu.ar_ |

---
## Introducción
El presente trabajo práctico está centrado en la simulación, configuración y análisis de redes de área local, abarcando desde los conceptos teóricos fundamentales hasta el despliegue de infraestructuras complejas mediante el software Cisco Packet Tracer.

El desarrollo del trabajo se encuentra dividido en tres secciones. En la primera, se aborda la clasificación de las redes según su alcance geográfico y se profundiza en los mecanismos de virtualización y segmentación de Capa 2, particularmente el funcionamiento de las VLANs y el protocolo de encapsulamiento IEEE 802.1Q (Tagging).

En la segunda sección, se implementa una topología básica de conmutación para poner en práctica la asignación de puertos, la administración segura de los dispositivos y la comprobación del aislamiento de los dominios de difusión.

Finalmente, en la tercera sección, se despliega una topología que simula la red a bordo de un avión. En esta etapa se integran conceptos de enrutamiento Inter-VLAN, asignación dinámica de direcciones (DHCP) y políticas de seguridad y acceso externo mediante Traducción de Direcciones de Red (NAT) y Listas de Control de Acceso (ACLs).

---
## Consignas
### Consigna N°1: 

Alcance de Redes y Virtualización

**a.** Investigar cómo se clasifican las redes según su alcance. Mencionar brevemente las características principales de cada una y colocar en cada cuadro de la Figura el acrónimo de red que corresponda.

> - **Redes de Área Personal (PAN):** Es una red que cubre una **área geográfica muy pequeña**. Es considerada la más moderna de todas e incluye aquella red de comunicaciones de datos que abarca el espacio alrededor de las personas, o dicho de otra manera, un **área de trabajo personal.** 
> Su tecnología más habitual es el Bluetooth y permite la interconexión de diferentes **dispositivos de uso personal**, como pueden ser teléfonos móviles, tabletas, relojes inteligentes, sistemas deportivos, unidades GPS, entre otros, entre sí o bien para conectar con un ordenador.

<center>
  <img src="https://hackmd.io/_uploads/SyCtuuaszg.png" width="350">
  <br>
  <em>Figura 1: Redes de Área Personal.</em>
</center>

> - **Redes de Área Local (LAN):** Estas redes son de **propiedad privada** y operan dentro de un **perímetro físico acotado**, como por ejemplo, un solo edificio, casa, oficina o campus universitario. Son utilizadas para conectar **computadoras personales y estaciones de trabajo** con el objetivo de compartir recursos e intercambiar información. 
> A diferencia de las redes más grandes que usan enrutamiento complejo, las LAN tradicionales consisten en un medio de transmisión compartido, que puede ser mediante un cable o una señal inalámbrica, al que están conectadas todas las máquinas. 
> En consecuencia, varias computadoras pueden intentar inyectar tramas de datos al mismo tiempo en la red; por lo tanto, las LAN requieren mecanismos de arbitraje estrictos para evitar colisiones. Esto lo resuelven mediante protocolos de la subcapa MAC, siendo el más famoso el de **IEEE 802.3 (Ethernet).**
> En cuanto a las topologías, históricamente se utilizaban arquitecturas de difusión tales como el **bus o el anillo**. Actualmente, la arquitectura LAN dominante utiliza una **topología en estrella**, donde todos los equipos se conectan a un switch central.

<center>
  <img src="https://hackmd.io/_uploads/Sk_kGY6sGg.png" width="500">
  <br>
  <em>Figura 2: Redes de Área Local.</em>
</center>

<center>
  <img src="https://hackmd.io/_uploads/Bkl2dMosfl.png" width="600">
  <br>
  <em>Figura 3: Topología Bus (a) y Anillo (b).</em>
</center>

> - **Redes de Área Metropolitana (MAN):** Son aquellas que cubren **áreas geográficas extensas**, útiles para interconectar oficinas, hospitales, universidades o diferentes instituciones que se encuentran dentro de una misma región o ciudad. 
> Utilizan infraestructura y protocolos para la transmisión de **grandes cantidades de información** con diferentes orígenes y destinos, cuyo principal cometido es la interconexión de las diferentes redes de los usuarios finales. Generalmente estas infraestructuras no son accesibles directamente por los usuarios y son **administradas por consorcios o proveedores de servicios locales.** Un ejemplo clásico de una MAN es la evolución de las redes de televisión por cable (CATV), adaptadas para proveer acceso bidireccional a Internet de alta velocidad.

<center>
  <img src="https://hackmd.io/_uploads/HJmOxc6ofl.png" width="500">
  <br>
  <em>Figura 4: Redes de Área Metropolitana.</em>
</center>

> - **Redes de Área Amplia (WAN):** Utilizada para conectar **múltiples redes de tipo LAN**, cubriendo una gran distancia geográfica, pudiendo comprender un país, continente o incluso el mundo entero. Esta red es ideal para interconectar **sucursales empresariales u oficinas remotas**, ya que permite la comunicación y transferencia de datos a grandes distancias.
> Estructuralmente, una WAN separa claramente los equipos de usuario (hosts) de la red de comunicación que los interconecta (subred). Esta última está compuesta por dos elementos fundamentales: las **líneas de transmisión**, como ser circuitos o enlaces, encargadas de transportar los bits, y los **elementos de conmutación**, como los routers, que se encargan de conectar dos o más líneas de transmisión.
> Debido a su enorme escala y topología compleja, las redes WAN **no utilizan un medio compartido simple**. En su lugar, emplean un mecanismo de conmutación de paquetes conocido como **almacenamiento y reenvío (`store-and-forward`).** Cuando un paquete viaja desde el origen hasta el destino, es recibido temporalmente por los routers intermedios, los cuales deben tomar decisiones mediante algoritmos de enrutamiento para determinar cuál es el mejor camino o interfaz de salida para reenviar ese paquete hacia su destino final.

<center>
  <img src="https://hackmd.io/_uploads/HJ4Kifisfg.png" width="500">
  <br>
  <em>Figura 5: Redes de Área Amplia.</em>
</center>

<center>
  <img src="https://hackmd.io/_uploads/Sk5gL5asMl.png" width="500">
  <br>
  <em>Figura 6: Store-And-Forward.</em>
</center>

**b.** ¿Qué es una vLAN? ¿Cómo se clasifican?
> Las **VLANs (Virtual Local Area Networks)** son redes de área local conmutadas en las que se configuran **particiones lógicas** independientemente de la distribución física. Surgen para **solucionar la saturación de los dominios de difusión** en las LANs planas. Al agrupar nodos lógicamente, independientemente de su ubicación física, se **limita el tráfico de broadcast** a esos dominios específicos, mejorando exponencialmente la **eficiencia y la seguridad de la red.**
>
> Se clasifican según su propósito y su mecanismo de asignación:
> - **Por Puerto:** El administrador asigna manualmente un puerto físico del switch a una VLAN específica.
> - **Por Dirección MAC:** La membresía de la VLAN se basa en la dirección MAC del dispositivo, lo que permite que el equipo mantenga su red virtual aunque cambie de puerto en el switch.
> - **Por Protocolo:** Se agrupan los dispositivos basándose en la dirección IP o el protocolo de red utilizado (Capa 3).
> - **De Propósito Específico:** Como las **VLAN de Administración**, usadas para configurar los equipos remotamente, o la **VLAN Nativa**, utilizada para el tráfico sin etiquetar en enlaces troncales.

<center>
  <img src="https://hackmd.io/_uploads/rkRTy5LRMx.png" width="350">
  <br>
  <em>Figura 7: VLAN.</em>
</center>

**c.** Investigar y resumir el protocolo IEEE 802.1Q. ¿Cómo se relaciona con las VLAN?
> El **protocolo IEEE 802.1Q,** también conocido como `dot1q`, es la normalización internacional diseñada para el **encapsulamiento y transporte de múltiples redes VLAN** a través de un **único enlace físico**, llamado Enlace Troncal (`Trunk`).
>
> En ese sentido, este mecanismo le permite al switch inyectar información dentro de la trama original de la Capa 2 para que el router o switch receptor que la reciba sepa exactamente a qué VLAN pertenece, permitiendo la **multiplexación de múltiples redes lógicas** sobre un solo cable físico.

**d.** En el contexto de los dos ítems anteriores ¿Qué es el Tagging?
> El **Tagging** es el mecanismo exacto a nivel de la Capa 2 que emplea el **estándar IEEE 802.1Q.** Consiste en insertar un **campo adicional**, que recibe el nombre de "etiqueta" o `Tag`, dentro del encabezado estándar de la trama MAC. Este campo adicional tiene un **tamaño de 4 bytes** e incluye un identificador único, llamado **VLAN ID (`VID`)** de 12 bits, lo que permite identificar matemáticamente hasta 4096 VLANs distintas en la misma red. Cabe aclarar que, al insertar estos 4 bytes, el tamaño de la trama original se modifica, lo que obliga al switch a recalcular la **Secuencia de Verificación de Trama (`FCS`)** al final de la misma para evitar errores de redundancia cíclica al ser procesada.
>
> La dinámica es la siguiente: cuando el Switch envía una trama hacia el Router a través del puerto `Trunk`, realiza el Tagging **insertando el número de la VLAN correspondiente**. De esta manera, el Router, al recibir la trama etiquetada, lee la información e identifica la subred lógica a la que pertenece. Luego, le **quita el `Tag` y enruta** el paquete mediante el protocolo IP en la Capa de Red.

<center>
  <img src="https://hackmd.io/_uploads/rJ2SvYLCMg.png" width="500">
  <br>
  <em>Figura 8: Tagging.</em>
</center>

---
### Consigna N°2: 
Implementaremos la siguiente topología en Packet-Tracer:

<center>
  <img src="https://hackmd.io/_uploads/HkkaxxioGx.png" width="600">
  <br>
  <em>Figura 9: Topología.</em>
</center>

Con la siguiente Tabla de ruteo:

<center>
  <img src="https://hackmd.io/_uploads/rk_pgxoiGe.png" width="800">
  <br>
  <em></em>
</center>

> Para esta consigna, en primer lugar, se implementó la topología física conectando PC-A al switch SW-1 y PC-B al switch SW-2.  
> 
<center>
  <img src="https://hackmd.io/_uploads/B18cqR6oMe.png" width="600">
  <br>
  <em>Figura 10: Topología conectada.</em>
</center>

> Posteriormente, se configuró el direccionamiento IP estático en las computadoras de acuerdo con la tabla de ruteo provista: `192.168.10.3` para PC-A y `192.168.10.4` para PC-B, ambas utilizando la máscara `255.255.255.0` y la puerta de enlace `192.168.10.1`.

<center>
  <img src="https://hackmd.io/_uploads/HyuDA0TjGl.png" width="600">
  <br>
  <em>Figura 11: Configuración IP estática.</em>
</center>

**a.** Desde cada computadora, ingresar a la terminal y configurar los switch. Nombrar a los mismos sw1 y sw2 respectivamente.
> En este punto, como lo indica el inciso, desde la aplicación de terminal de cada computadora, se ingresó a la interfaz de línea de comandos (`CLI`) de los switches a través de la conexión de consola. Luego, se accedió al modo de configuración global mediante el comando `configure terminal` y se establecieron los nombres lógicos de los dispositivos utilizando el comando `hostname`, designándolos como `sw1` y `sw2` respectivamente.

<center>
  <img src="https://hackmd.io/_uploads/H1RaOYCoMx.png" width="800">
  <br>
  <em>Figura 12: Asignación de nombres de host.</em>
</center>

**b.** y **c.** Asignar contraseñas privilegiadas, de consola y vty. Encriptar las contraseñas.
> Continuando con el desarrollo, para garantizar la seguridad de acceso a la administración de los dispositivos, se configuraron credenciales para los distintos niveles de privilegios y líneas de acceso. En ese sentido, se estableció una contraseña segura para el modo privilegiado (`enable secret ExecNotFound`), una contraseña para el puerto de consola (`ConsolaNotFound`) y otra para las 16 líneas de acceso remoto VTY (`VtyNotFound`), habilitando el inicio de sesión (`login`) en las interfaces correspondientes.
> 
> Ahora bien, para proteger las credenciales cargadas en texto plano dentro del archivo de configuración `running-config`, se habilitó la encriptación global ejecutando el comando `service password-encryption` en ambos switches.

<center>
  <img src="https://hackmd.io/_uploads/ByOAFt0ize.png" width="800">
  <br>
  <em>Figura 13: Encriptación de Contraseñas.</em>
</center>

**d.** Configurar las redes VLAN para ambos switch según la tabla de direcciones provista.
> En este inciso, se procedió a configurar la interfaz de gestión correspondiente a la VLAN 1 en ambos switches. Para ello, se ingresó a la interfaz mediante el comando `interface vlan 1` y se asignaron las direcciones indicadas en la tabla de ruteo: `192.168.1.11` para sw1 y `192.168.1.12` para sw2, ambas con máscara de subred `255.255.255.0`. Posteriormente, se encendieron las interfaces lógicas con el comando `no shutdown`.

<center>
  <img src="https://hackmd.io/_uploads/r1uIk9AiGe.png" width="800">
  <br>
  <em>Figura 14: Configuración de IP en la VLAN por defecto.</em>
</center>

**e.** Desconectar todas las interfaces que no estén siendo utilizadas.
> Se procedió a deshabilitar administrativamente todos los puertos físicos que no se encuentran en uso en la topología actual, lo que resulta ser una medida estandarizada de seguridad en infraestructuras de red. Entonces, se agruparon los puertos utilizando el comando `interface range` y, luego, se aplicó el comando `shutdown`.

<center>
  <img src="https://hackmd.io/_uploads/Bk-LO30sfx.png" width="800">
  <br>
  <em>Figura 15: Apagado administrativo de interfaces.</em>
</center>

> De la figura anterior, se puede observar lo siguiente:
> **En sw1:** Se apagaron los rangos `Fa0/2 - Fa0/5`, `Fa0/7 - Fa0/24` y `Gig0/1 - Gig0/2`, dejando activos únicamente el puerto `Fa0/1` y el `Fa0/6`, correspondientes al enlace entre switches y a la conexión a PC-A respectivamente.
> **En sw2:** Se apagaron los rangos `Fa0/2 - Fa0/17`, `Fa0/19 - Fa0/24` y `Gig0/1 - Gig0/2`, manteniendo activos el puerto `Fa0/1` y el `Fa0/18`, este último corresponde a la conexión a PC-B.

**f.** Guardar la configuración.
> Ahora bien, con el objetivo de garantizar la persistencia de todos los parámetros aplicados frente a posibles reinicios o cortes de energía, se trasladó la configuración en ejecución, `running-config`, alojada en la memoria RAM hacia la memoria no volátil (NVRAM) utilizando el comando `write memory` en el modo privilegiado de ambos switches. Luego de ejecutar dicho comando, se recibe la línea `[OK]` confirmando el guardado.

<center>
  <img src="https://hackmd.io/_uploads/HkG6oTRsfl.png" width="800">
  <br>
  <em>Figura 16: Guardado en la NVRAM.</em>
</center>

**g.** Testear comunicación usando pings entre las computadoras.
> Para validar la conectividad de extremo a extremo se hizo uso de la herramienta `ping` desde el *Command Prompt* de las terminales:
> - Desde PC-A se ejecutó un ping a la IP de PC-B, `192.168.10.4`.
> - Desde PC-B se ejecutó un ping a la IP de PC-A, `192.168.10.3`.

<center>
  <img src="https://hackmd.io/_uploads/SJdu6p0sMx.png" width="800">
  <br>
  <em>Figura 17: Prueba de Conectividad Inicial.</em>
</center>

> Como se puede observar, la prueba es exitosa y, de esta manera, se pone en evidencia que ambas computadoras están lógicamente en la misma subred, `192.168.10.0/24`.

**h.** y **i.** Crear VLANs en ambos switches. Utilizar `show vlan brief` para visualizar la lista de VLANs en alguno de los switch. ¿Cuál es la VLAN utilizada por defecto?.
> Para este punto, se ingresó al modo de configuración global en ambos switches y se instanciaron las tres redes virtuales solicitadas: `vlan 10` (Laboratorio), `vlan 20` (Bar) y `vlan 99` (Management). Posteriormente, ejecutando el comando `show vlan brief`, se logró verificar la correcta creación de las redes. 

<center>
  <img src="https://hackmd.io/_uploads/SJxebCRsfx.png" width="800">
  <br>
  <em>Figura 18: Salida de show vlan brief.</em>
</center>

> En esta salida se observa que la VLAN utilizada por defecto es la VLAN 1 (`default`), y que, además, la totalidad de los puertos físicos del switch se encuentran asignados a ella de manera predeterminada.

**j.** Asignar la PC-A a la VLAN Laboratorio. 
> Para asignar la PC-A a la VLAN "Laboratorio" en el switch SW-1, se ingresó a la interfaz correspondiente, `f0/6`, se forzó su operación como puerto de usuario final con el comando `switchport mode access` y se la vinculó a la VLAN 10 mediante `switchport access vlan 10`. 
> 
> Si nuevamente se ejecuta `show vlan brief`, se podrá notar que el puerto `Fa0/6` fue removido de la VLAN 1 y ahora figura activo dentro de la VLAN 10. Esto se puede observar en la siguiente figura:

<center>
  <img src="https://hackmd.io/_uploads/ryRSZHF0zl.png" width="800">
  <br>
  <em>Figura 19: Asignación de puerto de acceso a la VLAN 10.</em>
</center>

**k.** y **l.** Desde la VLAN 1, remover la ip de Management y configurarla para funcionar en la VLAN 99 (que configuramos como Management). Verificar el estado de la VLAN utilizando `show vlan brief` y el estado de las interfaces utilizando `show ip interface brief`.
> En SW-1, se ingresó a la interfaz virtual `interface vlan 1`, se le removió la dirección IP utilizando `no ip address` y se la apagó administrativamente ejecutando `shutdown`. 
> 
> Seguidamente, se ingresó a la interfaz `interface vlan 99` (Management), a la cual se le asignó la dirección IP de gestión `192.168.1.11 255.255.255.0` y se encendió la interfaz. Mediante el comando `show ip interface brief`, se analizó el estado final de las interfaces en SW-1.

<center>
  <img src="https://hackmd.io/_uploads/rkDGpARsze.png" width="800">
  <br>
  <em>Figura 20: Salidas SW-1: show vlan brief - show ip interface brief.</em>
</center>

> La salida confirma la exitosa migración de la gestión: la interfaz `Vlan1` figura sin dirección IP asignada y la interfaz `Vlan99` ostenta la IP `192.168.1.11`. Cabe destacar que el `Status` y el `Protocol` de la `Vlan99` figuran en estado `down`; esto se debe a que, en este momento, no existe ningún puerto físico activo asociado a dicha VLAN, por lo que la interfaz virtual no puede levantar (`line protocol down`).

**m.** Asignar la PC-B a la VLAN Laboratorio en el sw2.
> Se repitieron los incisos J y K en el segundo switch, es decir, se asignó el puerto de la PC-B, `interface f0/18`, a la VLAN 10 como puerto de acceso. Luego, se removió la IP de la VLAN 1 y, finalmente, se configuró la interfaz virtual de la VLAN 99 con la IP `192.168.1.12`. Las salidas de `show vlan brief` y `show ip interface brief` en SW-2 arrojaron los mismos resultados esperados que en su par.

<center>
  <img src="https://hackmd.io/_uploads/SkbFilJnfe.png" width="800">
  <br>
  <em>Figura 21: Salidas SW-2: show vlan brief - show ip interface brief.</em>
</center>

**n.** Verificar la conectividad entre PC-A y PC-B utilizando pings. Verificar conectividad entre sw1 y sw2 utilizando pings. Interpretar los resultados.
> Para finalizar la práctica, se procedió a reevaluar la conectividad de la red. Primeramente, se revisó la conectividad entre PC-A y PC-B:

<center>
  <img src="https://hackmd.io/_uploads/SywA-by3Me.png" width="800">
  <br>
  <em>Figura 22: Prueba de Conectividad (Ping PC a PC).</em>
</center>

> A partir de la figura, se puede observar que, al ejecutar un `ping` entre PC-A y PC-B, los paquetes resultan en `Request timed out`, es decir, 100% de pérdida. Esto se debe a que aunque ambas computadoras pertenecen a la misma subred lógica y están asignadas a la misma VLAN (Laboratorio), el enlace físico que une a los switches pertenece por defecto a la VLAN 1. Por lo tanto, el tráfico de la VLAN 10 no puede atravesar dicho enlace para llegar al otro switch.

> Ahora, se revisó la conectividad entre SW-1 y SW-2:

<center>
  <img src="https://hackmd.io/_uploads/ryvcM-k2Gg.png" width="800">
  <br>
  <em>Figura 23: Prueba de Conectividad (Ping Switch a Switch).</em>
</center>

> Se puede apreciar que, al ejecutar un `ping` desde la consola de SW-1 a la IP de gestión de SW-2, `192.168.1.12`, el resultado es de 0% de éxito. Lo que ocurre es algo similar al caso anterior y es que la red de gestión ahora reside en la VLAN 99. Como el enlace inter-switch sigue operando como un puerto de acceso de la VLAN 1, el tráfico de gestión de la VLAN 99 queda aislado dentro de cada equipo.
>
> Habiendo estudiado estos casos, lo que se puede concluir es que para restituir la conectividad total en esta topología segmentada, resulta necesario configurar los puertos `Fa0/1` de ambos switches como Enlaces Troncales (`Trunks`) utilizando el estándar de encapsulamiento IEEE 802.1Q. Esto permitiría el Tagging de las tramas, habilitando el paso simultáneo del tráfico de las VLANs 1, 10, 20 y 99 a través del mismo cable físico.

---
### Consigna N°3: 
Utilizando lo que aprendimos sobre VLAN, e investigando la configuración de NAT y ACLs, simularemos el despliegue de una red LAN a bordo de una aeronave. La idea es la siguiente, tendremos tres segmentos:
**i.** Clase Turista: acceso solo a un sistema de entretenimiento (server local)
**ii.** Clase Business: acceso a sistema de entretenimiento e internet.
**iii.** Administración: acceso total.

<center>
  <img src="https://hackmd.io/_uploads/rJU9zgiiMx.png" width="600">
  <br>
  <em></em>
</center>

Podés usar una topología de red como la siguiente:

<center>
  <img src="https://hackmd.io/_uploads/r1zHF-ooMl.png" width="450">
  <br>
  <em>Figura 24: Topología de Red propuesta.</em>
</center>

Y la siguiente tabla de direccionamiento:

<center>
  <img src="https://hackmd.io/_uploads/rkUCMgojfe.png" width="800">
  <br>
  <em></em>
</center>

> Dando inicio al desarrollo de esta consigna, en primera instancia, se procedió con el despliegue de los dispositivos físicos: Laptop, Switch, Router y Servidores. De acuerdo con lo que plantea la actividad:
> - **Laptop:** Para las clases Turista y Business se previó 3 y 2 dispositivos respectivamente, los cuales representan a los pasajeros. Luego, 1 solo dispositivo para Admin.
> - **Router:** Un router 2811 como gateway, denominado "Router Avión".
> - **Switch:** Un switch 2960 para la distribución hacia las terminales.
> - **Servidor:** Dos servidores, uno local, correspondiente a "Servidor de Entretenimiento" y otro externo para simular la red pública, "ISP".

> Posteriormente, se realizó la ubicación de los dispositivos de acuerdo al background del avión provisto y, luego, la conexión de los mismos, las cuales se asignaron al switch de la siguiente manera:
> - **Fa0/1:** Router Avión.
> - **Fa0/2 - Fa0/4:** Laptops Clase Turista.
> - **Fa0/5 - Fa0/6:** Laptops Clase Business.
> - **Fa0/7:** Laptop Admin.
> - **Fa0/8:** Servidor Entretenimiento 

> Con respecto a la conexión del "ISP" a "Router Avión", la misma se estableció a través de la interfaz `Fa0/1` del router. A continuación, se muestra la distribución de los dispositivos dentro del avión y las conexiones realizadas:

<center>
  <img src="https://hackmd.io/_uploads/HkMlqN80Gg.png" width="800">
  <br>
  <em>Figura 25: Esquema de Red del avión.</em>
</center>

> Lo siguiente fue proceder con la segmentación lógica de la red a través de la configuración del switch. Para ello, se ingresó a la CLI del mismo y se crearon tres VLANs. Luego, a través del comando `interface range` se configuraron los puertos en modo acceso mediante el comando `switchport mode access` y se asignaron a sus respectivas VLANs según la distribución de los equipos finales. De esta manera, se aisló el tráfico de los distintos dominios de difusión como lo indica la consigna: `VLAN 10` (Turista), `VLAN 20` (Business) y `VLAN 99` (Admin). 
> 
> Por otro lado, la interfaz `Fa0/1`, la cual establece la conexión entre el switch y el router, fue configurada en modo troncal, utilizando el comando `switchport mode trunk`, para permitir el paso del tráfico etiquetado mediante el estándar IEEE 802.1Q hacia el enrutador principal.
> 
> En la siguiente figura se muestra el bloque de código utilizado; además, se diferencian en recuadros cada etapa:

<center>
  <img src="https://hackmd.io/_uploads/ByB2-CORMg.png" width="800">
  <br>
  <em>Figura 26: Bloque de Código para configuración de puertos y Trunks.</em>
</center>

> Una forma de asegurarse de que la asignación de los puertos fue exitosa es por medio del comando `show vlan brief`. En ese sentido, al ejecutar dicho comando se muestra en pantalla la siguiente tabla:

<center>
  <img src="https://hackmd.io/_uploads/Bkk9ERdCMx.png" width="800">
  <br>
  <em>Figura 27: Salida de show vlan brief.</em>
</center>

> Ahora bien, se procedió a realizar la configuración IP de los servidores mediante el direccionamiento estático. Al Servidor Entretenimiento, el cual pertenece a la VLAN 99, se le asignó la dirección `10.10.99.10/24` con su respectiva puerta de enlace en `10.10.99.1`. Por su parte, al Servidor ISP, que simula la red WAN pública, se le configuró la IP `200.0.0.2`, luego, como máscara de subred se utilizó `255.255.255.252` y, finalmente, se estableció como su puerta de enlace la IP `200.0.0.1`, que corresponde a la interfaz externa del router. 
> Este procedimiento se puede observar en la siguiente figura:

<center>
  <img src="https://hackmd.io/_uploads/BkeShAdRMl.png" width="800">
  <br>
  <em>Figura 28: Configuración IP estática en los servidores.</em>
</center>

> Con respecto a la gestión del tráfico de la red, la misma se centralizó en el Router Avión. Para que las distintas VLANs puedan comunicarse utilizando un solo enlace físico, se habilitó la interfaz principal `Fa0/0` y se crearon tres subinterfaces lógicas: `Fa0/0.10`, `Fa0/0.20` y `Fa0/0.99`. A cada una se le asignó su respectiva puerta de enlace y se configuró el encapsulamiento IEEE 802.1Q para separar el tráfico. Por otro lado, la conectividad exterior se resolvió configurando la interfaz `Fa0/1` con direccionamiento público hacia el ISP, respaldada por una ruta estática por defecto (`0.0.0.0 0.0.0.0`) para derivar el tráfico saliente.
>
> Adicionalmente, para automatizar la asignación de direcciones IP en las terminales, se configuraron tres pools DHCP independientes, reservando las primeras 10 direcciones de cada subred para uso administrativo. Finalmente, para gestionar el acceso a la red pública (WAN), se implementó el protocolo NAT junto con Listas de Control de Acceso (ACLs). Específicamente, la ACL `20` define el tráfico permitido para la traducción NAT, mientras que la ACL `100` se aplicó en la subinterfaz correspondiente a la clase Turista para bloquear explícitamente su salida a Internet, asegurando así que dichos usuarios únicamente interactúen con el servidor local.
>
> A continuación, se muestra el bloque de código ejecutado en Router Avión:

<center>
  <img src="https://hackmd.io/_uploads/BJng4xFCMe.png" width="800">
  <br>
  <em>Figura 29: Bloque de Código de Subinterfaces y DHCP.</em>
</center>

<center>
  <img src="https://hackmd.io/_uploads/HJdhVeFAMe.png" width="800">
  <br>
  <em>Figura 30: Bloque de Código de NAT, ACL y enrutamiento por defecto.</em>
</center>

> Un detalle que se tuvo en cuenta en este trabajo fue personalizar la página del Servidor Entretenimiento a la cual accederán las laptops. Esto se logró a través del archivo `index.html` del servidor web. A continuación, se muestra el archivo modificado:

<center>
  <img src="https://hackmd.io/_uploads/SkSjC8IAfx.png" width="800">
  <br>
  <em>Figura 31: Página HTML personalizada.</em>
</center>

> Con lo realizado hasta ahora, la infraestructura central está operando correctamente. Luego, se procedió a lograr la asignación dinámica de IPs en los dispositivos finales y la validación de la conectividad. 
> 
> Para ello, se accedió a la configuración de IP de cada terminal y se modificó el método de asignación de `Static` a `DHCP`. Durante este proceso, el simulador muestra el estado `Requesting IP Address`. Segundos después, al completarse la negociación con el servidor, se confirma con el mensaje `DHCP Request Successful`, observándose los parámetros de red asignados correctamente.
>
> A fin de evidenciar lo anterior, se tomaron las siguientes capturas, tomando de ejemplo uno de los dispositivos de la Clase Turista:

<center>
  <img src="https://hackmd.io/_uploads/ryvxkdL0Me.png" width="800">
  <br>
  <em>Figura 32: Solicitud de configuración por DHCP.</em>
</center>

<center>
  <img src="https://hackmd.io/_uploads/B1V-yuIRzg.png" width="800">
  <br>
  <em>Figura 33: Asignación exitosa de parámetros IP vía DHCP.</em>
</center>

> Finalmente, se realizaron pruebas de validación de conectividad. Como primer caso, desde un dispositivo de la Clase Turista y uno de la Clase Business, se ingresó al `Web Browser` y se colocó en la URL la dirección IP del Servidor Entretenimiento. Mediante la siguiente figura, se confirma que en ambos casos la página cargó correctamente:

<center>
  <img src="https://hackmd.io/_uploads/H1qQXJY0Gg.png" width="800">
  <br>
  <em>Figura 34: Resultado de acceso al servidor Web local.</em>
</center>

> Asimismo, se hizo la prueba de ejecutar el comando `ping` desde ambos dispositivos hacia la IP del Servidor Entretenimiento:

<center>
  <img src="https://hackmd.io/_uploads/ryIprkFRGl.png" width="800">
  <br>
  <em>Figura 35: Prueba de Conectividad (Ping al servidor local).</em>
</center>

> Lo siguiente fue comprobar el correcto funcionamiento de NAT, permitiendo a la red Business alcanzar el ISP, `200.0.0.2`, así como validar el bloqueo de la Lista de Control de Acceso (`access-list 100`): 

<center>
  <img src="https://hackmd.io/_uploads/Hk6cvyFAfg.png" width="800">
  <br>
  <em>Figura 36: Pruebas de conectividad externa validando NAT y ACLs.</em>
</center>

> Como se puede observar en la figura, se bloqueó exitosamente el tráfico de salida hacia la WAN desde las terminales de clase Turista (Resultando en `Request timed out`), cumpliendo con los requerimientos operativos. Asimismo, se verificó la conectividad exitosa de las terminales de clase Business hacia la red pública.
>
> Para la última prueba, se debía comprobar la conectividad desde la laptop Admin hacia el resto de dispositivos: servidores y laptops. Esto se demuestra a través de las siguientes figuras:

<center>
  <img src="https://hackmd.io/_uploads/rJJ5sktCMl.png" width="800">
  <br>
  <em>Figura 37: Prueba de Conectividad total (Admin hacia servidores).</em>
</center>

<center>
  <img src="https://hackmd.io/_uploads/H1iQ31tCGx.png" width="800">
  <br>
  <em>Figura 38: Prueba de Conectividad total (Admin hacia usuarios).</em>
</center>

---
## Conclusiones
A lo largo del presente trabajo práctico, se logró implementar y validar exitosamente los conceptos teóricos relacionados con la segmentación, el enrutamiento y la seguridad en redes locales.

Por medio de la configuración de la primera topología se pudo demostrar el propósito fundamental de las VLANs, el cual consiste en el aislamiento lógico de los dominios de difusión. Luego, la comprobación de fallas de conectividad iniciales entre los switches puso de manifiesto la importancia crítica de los enlaces troncales y del estándar IEEE 802.1Q para el correcto transporte de tramas etiquetadas en redes segmentadas.

Posteriormente, en el despliegue de la red simulada del avión, se presentó el desafío de interconectar estas redes aisladas mediante el enrutamiento Inter-VLAN, utilizando subinterfaces lógicas para centralizar el tráfico. Asimismo, la implementación conjunta de NAT y ACLs demostró ser una solución efectiva para el control del tráfico, permitiendo cumplir con los requisitos operativos, estos son: restringir la salida a Internet de la clase Turista, garantizando su acceso exclusivo a los servicios locales, y habilitando la navegación plena para la clase Business.

---
## Referencias
- Tanenbaum, A. S., & Wetherall, D. J. (2012). Redes de computadoras (5.ª ed.). Pearson Educación.
- Kurose, J. F., & Ross, K. W. (2017). Redes de computadoras: Un enfoque descendente (7ma ed.). Pearson Educación.
- Ymant. (s.f.). Redes WAN, MAN, LAN y PAN. ¿Qué son y cómo funcionan?. Ymant. Recuperado el 14 de octubre de 2026, de https://www.ymant.com/blog/redes-wan-man-lan-y-pan/
