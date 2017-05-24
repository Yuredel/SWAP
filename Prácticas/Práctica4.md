# Práctica4: Asegurar la granja web
### Escenario
Disponemos tres máquinas virtualizadas que disponen de UbuntuServer16
como sistema operativo. Las ip's de dichas máquinas son las siguientes:
* máquina1: 192.168.1.101
* máquina2: 192.168.1.102
* máquina3 (Balanceador de carga): 192.168.1.103

Durante el desarrollo de esta práctica utilizaremos dos medidas de seguridad para proteger nuestra granja web. Por un lado Instalaremos en los servidores un certificado SSL para poder configurar el protocolo HTPPS, y a continuación configuraremos mediante la ejecución automática de un script, los cortafuegos de la máquina.

## Instalación del certificado SSL
### ¿Qué es el certificado SSL?
fdhdfnghdfg


### Proceso de instalación

Lo primero que debemos hacer es ***activar el módulo ssl***, para lo cual utilizaremos el comando:

`a2enmod ssl`

A continuación, restableceremos el servicio de apache mediante la orden:

`service apache2 restart`

## servicio de cortafuergos mediante la aplicación ***iptables***

Iptables es el nombre de la herramienta de espacio de usuario mediante la cual el administrador puede definir políticas de filtrado del tráfico que circula por la red.

### Comandos para iptables

Lo primero que deberemos hacer es crear un script con todos los comandos *iptables* que hemos probando a lo largo de la práctica.
Para comprobar el estado del cortafuegos deberemos ejecutar:

`iptables -L -n -v`

![Img][im4]

Para las funciones básicas tenemos los siguientes comandos:
~~~~
service iptables start
service iptables restart
service iptables stop
service iptables save
~~~~


También se puede para el cortafuegos y eliminar al mismo tiempo todas sus reglas:

~~~
iptables -F
iptables -X
iptables -t nat -F
iptables -t nat -X
iptables -t mangle -F
iptables -t mangle -x
iptables -P INPUT ACCEPT
iptables -P OUTPUT ACCEPT
~~~

Para denegar cualquier tipo de tráfico de información, podemos hacer:

~~~
iptables -P INPUT DROP
iptables -P OUTPUT DROP
iptables -P FORWARD DROP
iptables -L -n -v
~~~
![Img][im2]

De la misma forma podemos bloquear el tráfico de entrada de la siguiente manera:

~~~
iptables -P INPUT DROP
iptables -P FORWARD DROP
iptables -P OUTPUT ACCEPT
iptables -A INPUT -m state --state NEW, ESTABLISHED -j ACCEPT
iptables -L -n -v
~~~
![Img][im3]

Podemos bloquear el tráfico ICMP (ping), para evitar ataques como el del *ping de la muerte*. Un ping de la muerte es un tipo de ataque enviado a una computadora que consiste en mandar numerosos paquetes ICMP muy grandes (mayores a 65.535 bytes) con el fin de colapsar el sistema atacado. Ejecutaremos:
`iptables -A INPUT -p icmp --icmp-type echo-request -j DROP`

![Img][im5]
Para abrir el puerto 22, el correspondiente al protocolo TCP que permitiendo así el acceso por SSH, ejecutaremos:
~~~~
iptables -A INPUT -p tcp --dport 22 -j ACCEPT
iptables -A OUTPUT -p udp --spot 22 -j ACCEPT

 ~~~~
 ![Img][im6]

Detalle:
 ![Img][im7]

Por descontado la herramienta también puede configurar los puertos HTTP y HTTPS (80/443), para la configuración de un servidor web. Lo haremos mediante la ejecución de:
~~~~
iptables -A INPUT -m state --state NEW -p tcp --dport 80 -j ACCEPT
iptables -A OUTPUT -m state --state NEW -p tcp --dpot 443 -j ACCEPT
~~~~
Para el puerto DNS (53), aplicamos la misma lógica.
~~~~
iptables -A INPUT -m state --state NEW -p tcp --dport 53 -j ACCEPT
iptables -A INPUT -m state --state NEW -p udp --dpot 53 -j ACCEPT
~~~~

Esta ejecución nos incluirá las  siguientes  en la configuracón del cortafuegos.
![Img][img8]
Otra funcionalidad interesante es poder bloquear todo el tráfico que proviene o se dirige hacia una determinada ip. En el primer caso deberíamos ejecutar:

`iptables -I INPUT -s *la_ip_a_bloquear* -j DROP`

En el segundo caso deberemos ejecuta
r:
`iptables -I OUTPUT -s *la_ip_a_bloquear* -j DROP`

También podemos bloquear la entrada o la salida a un determinado dominio mediante:
~~~
iptables -I INPUT -p tcp -d *www.nombredominio.Comparativa* -j DROP

iptables -I OUTPUT -p tcp -d *www.nombredominio.Comparativa* -j DROP

~~~

Podría resultar conveniente  poder aplicar una determinada configuración para un conjunto de puertos. Lo haríamos de la siguiente manera:

~~~~
iptables -A INPUT -i eth0 -p tcp -m multiport --dsport 22,80,443 -m state --state NEW,ESTABLISHED -j ACCEPT
iptables -A OUTPUT -i eth0 -p tcp -m multiport --dsport 22,80,443 -m state --state NEW,ESTABLISHED -j ACCEPT
~~~~

Podremos comprobar el funcionamiento de las configuración añadidad ejecutando el comando ***nestat -tulpn***
Podemos comprobar el estado de un puerto en concreto aplicando un filtro *grep* al comando:
`netstat -tulpn | grep :*número_de_puerto*`


## Automatización de la configuración del cortafuegos
Podemos automatizar la configuración de un cortafuegos mediante un script  que debe presentar el siguiente aspecto:

![IMG][im1]

#### Ejecutar un script durante el arranque del sistema en rc.local
Tenemos dos formas de poder poner en marcha el script dependiendo del sistema que estemos utilizando.
* Podemos poner el fichero directamente en el directorio `/etc/rc.local` y reiniciar el ordenador para que el script se ejecute al reiniciar el sistema.

## Ejecutar un script durante el arranque del sistema con systemd
systemd es un conjunto de demonios o daemons de administración de sistema, bibliotecas y herramientas diseñados como una plataforma de administración y configuración central para interactuar con el núcleo del Sistema operativo GNU/Linux.

Lo primero localizar la ubicación de los script. Estos se hayan albergados en:
`/etc/systemd/system`
Lo primero que deberemos hacer es ubicar en esta ruta un script cuyo nombre sea del tipo "miScript.service". Este fichero debe tener los siguientes permisos de ejecución ***-rwxr-xr-x***
El fichero debe tener este aspecto
***foto***








[im1]:Imagenes/P4/ip_table_final.png
[im2]:Imagenes/P4/iptablesDROP.png
[im3]:Imagenes/P4/ip_NEW.png
[im4]:Imagenes/P4/iptable0.png
[im5]:Imagenes/P4/ping_muerte.png
[im6]:Imagenes/P4/tcpGENERAL.png
[im7]:Imagenes/P4/tcpDETALLE.png
[im8]:Imagenes/P4/tcpudp53Salida.png
