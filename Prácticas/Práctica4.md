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

Lo primero que debereos hacer es crear un script con todos los comandos *iptables* que hemos probando a lo largo de la práctica.
***completar con ejercicios***

El script debe presentar el siguiente aspecto:

![IMG][im1]





[im1]:Imagenes/P4/ip_table_final.png
