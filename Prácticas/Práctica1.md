# Práctica1: Preparación de las Herramientas
### Instalación de máquinas virtuales
La instalación de las máquinas de UbuntuServer16, lo haré sobre VirtualBox.
En un momento determinado de la instalación debemos indicarle que instale LAMP.   
LAMP es el acrónimo usado para describir un sistema de infraestructura de internet que usa las siguientes herramientas:Apache, MySQL y PHP. La combinación de estas tecnologías es usada principalmente para definir la infraestructura de un servidor web, utilizando un paradigma de programación para el desarrollo.

![Imagen][im1]  
figura1: Instalación de LAMP en la máquina de UbuntuServer16


#### Comprobación de la instalación
Una vez realizada la instalación, he instalado, mediante el siguiente comando, un entorno gráfico para facilitar el futuro trabajo con las máquinas:

<code>  apt-get install --no-install-recommends lubuntu-desktop <code>





Podemos comprobar la versión de Apache que ha sido instalada en nuestra máquina mediante el comando:

<code> apache2 -v <code>

![Imagen][im2]  

figura2: Versión de apache que ha sido instalada

Esto sirve como comprobación de que el servidor web ha sido instalada.Otra forma sería comprobarlo mediante el comando ***ps***
PS se utiliza para obtener una instantánea de los procesos en el sistema , algunas de sus opciones son:
* a: E liminar la restricción BSD "only yourself" para agregar procesos de otros usuarios.
* u: Utilizar el formato orientado al usuario.
*  x : Eliminar la restricción BSD "must have a tty" para agregar procesos que no tengan una tty asociada.

Usando estas opciones del comando PS, combinadas con el comando grep nos permitirá ver los procesos de apache que ese están ejecutando en la maquina. Ejecutamos pues, la siguiente combinación de comandos que nos proporcionará la salida que se muestra en la imagen a continuación.

 <code> ps aux | grep apache  <code>
 

![Imagen][im3]

figura3: Versión de apache que ha sido instalada

### Configuración de las Interfaces de red
Aunque las herramientas web están funcionando, la configuración de red, no está finalizada. Lo primero será cambiar la configuración de la red de la herramienta de virtualización, en este caso, VirtualBox.

Con la máquina apagada, y en la sección de configuración de las interfaces de red nos aseguramos que  nuestro primer adaptador sea del tipo * NAT*, y añadiremos un segundo adaptador del tipo *Red Interna*. Debemos fijarnos en el nombre de la red (inet) ya que cuando creemos una segunda máquina, el nombre de la red debe coincidir para que la comunicación entre ambas sea posible.

Al ejecutar el comando *ifconfig*, podemos observara que la interfaz que no está configurada es la que recibe el nombre enp0s8.

Buscaremos el archivo de configuración de interfaces en la siguiente dirección: *** /etc/network/interfaces***.. Dentro del archivo añadiremos las siguientes líneas para la configuración de la interfaz:
~~~
auto enp0s8
iface enp0s8 inet static
address 192.168.1.101
ateway 192.168.1.1
netmask 255.255.255.0
network 192.168.1.0
broadcast 192.168.1.255
~~~

Repetiremos el proceso en la configuración de la segunda máquina, sólo que cambiaremos la dirección(address), por otra que no esté en uso, por ejemplo la 192.168.1.100.

![Imagen][im4]

figura4: Ejecución de *ifconfig* una vez configurada la interfaz

### Ejecución del comando CURL mediante la interfaz configurada

Una vez que tengamos las máquinas instaladas y los servidores LAMP configurados,
comprobaremos  que  Apache  está  funcionando.  Para  ello,  usando  un  editor  de  texto
plano, crearemos el archivo HTML llamado prueba.html en el directorio /var/www/html, luego ejecutaremos el comando curl, para lo cual usaremos la interfaz recientemente configurada. Tan sólo deberemos escribir en la terminal:

<code> curl http:// direcciónInterfaz/nombrefichero.html <code>

Recordemos que la dirección ip de la máquina es 192.168.1.101, y el nombre del archivo es prueba.html. En la siguiente imagen podemos ver el resultado dicha ejecución, es el contenido completo del archivo.

![Imagen][im5]

figura5: Ejecución del comando CURL



[im1]: Imagenes/P1.png
"Instalación de LAMP en la máquina de UbuntuServer16"

[im2]: Imagenes/versionapache.png
  "Versión de apache que ha sido instalada"

[im3]:Imagenes/apache.png
  "Versión de apache que ha sido instalada"

[im4]: Imagenes/interfaz.png
  "Ejecución de *ifconfig* una vez configurada la interfaz"

[im5]: Imagenes/funciona.png
"Ejecución del comando CURL"
