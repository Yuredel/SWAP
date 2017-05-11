# Práctica3: Balanceo de carga
### Escenario
Disponemos tres máquinas virtualizadas que disponen de UbuntuServer16
como sistema operativo. Las ip's de dichas máquinas son las siguientes:
* máquina1: 192.168.1.101
* máquina2: 192.168.1.102
* máquina3 (Balanceador de carga): 192.168.1.103

### Qué es el ***banlanceo de carga*** y cuándo utilizarlo
El tráfico de Internet está en constante crecimiento y por tanto ampliar la memoria del servidor solo es una solución temporal. La opción más razonable es, a largo plazo, configurar más servidores y repartir las peticiones de los clientes entre ellos. Esto incrementa la velocidad de acceso del usuario al servidor, mejora la fiabilidad del sistema y la tolerancia a fallos, permitiendo reparar o mantener cualquier servidor en línea sin que afecte al resto del servicio.
La forma más elemental para hacer este balanceo de carga entre servidores, es utilizar un DNS. Este tipo de balanceo resulta sencillo y eficaz, solo necesitaremos varias máquinas que dispongan de diferentes ip's. El inconveniente del balanceo mediante un servidor DNS, es que este no tendrá en cuenta la carga de trabajo a la que está sometido el servidor.

## NGINX
### Balanceo de Carga  con  Round-Robin

#### Configuración
Instalaremos nginx, un servidor web de código abierto. La instalación es sencilla mediante terminal:
~~~~
sudo apt-get update && sudo apt-get dist-upgradde && sudo apt-get autoremove
sudo apt-get install nginx
~~~~
Para poder utilizar el servidor como Balanceador, deberemos acceder al fichero ***/etc/nginx/conf.d/default.conf***, e introducir los siguientes cambios:

![Img][im1]

Para que el servidor deje de funcionar como un servidor web deberemos comentar la siguiente línea del fichero de configuración de *nginx* ubicado en la siguiente ruta:

`/etc/nginx/nginx.conf`

Ahí deberemos comentar la siguiente línea:

`include /etc/nginx/sites-enabled/*`

A continuación pondremos en marcha el servicio de la siguiente manera:

`sudo systemctl start nginx`

Si la configuración es correcta, al efectuar
`systemctl status nginx.service`, podremos ver la siguiente respuesta:
![Img][im2]

#### Puesta en marcha del servicio
Mediante la anteriormente utilizada, curl, podremos lanzar diversas peticiones al Balanceador y podremos apreciar como distribuye las peticiones según la filosofía Round-Robin. Ejecutamos El comando sobre la dirección ip que le hemos adjudicado al balanceador, en este caso *192.168.1.103*.
Vemos en la siguiente figura como se alternan las respuestas del servidor.

![Img][im3]


### Balanceo de Carga Ponderado
#### Cambios en la Configuración
En el archivo situado en, ***/etc/nginx/conf.d/default.conf***, y añadimos a los servidores sobre los que vamos ha hacerles el balanceo, un peso mediante la variable weight. Añadiremos un mayor peso a aquellas máquinas que consideremos más potentes.

![Img][im4]

Esta puede ser una opción interesante en el caso de que tengamos máquinas de diversas capacidades pero esta opción tiene como inconveniente, que no permite mantener las sesiones de forma correcta.
Por último deberemos reiniciar el servicio:

`sudo systemctl restart nginx`
#### Puesta en marcha del servicio
Podemos observar en la imagen que el balanceador envía una tarea a la máquina1, mientras que a la máquina2, le envía dos tareas, tal y como se ha indicado en la configuración.

![Img][im5]

### Balanceo de Carga por IP
Para conseguir dirigir  el tráfico mediante las IP necesitamos volver al archivo de configuración
Hay dos formas de hacerlo,ambos, mediante la modificación del archivo de configuración: */etc/nginx/conf.d/default.conf*

###### Ip_hash
mediante la directiva ***ip_hash***, introduciéndola en el apartado *upstream apaches*.

![Img][im6]

Esta opción controlaría el tráfico desde el servidor, dirigiendo a todos los usarios de un servidor hacía el mismo servidor.

###### Keepalive
Mediante la directiva ***keepalive***, que posibilida identificar al usuario final y dirigir el tráfico de forma más precisa.Escribiremos en el fichero de configuración: */etc/nginx/conf.d/default.conf* lo siguiente:

![Img][im7]

Vemos que keepalive va seguido de un número que indica lo segundos durante los que se mantiene la conexión.



## HAPROXY
Una vez instalado el servidor con :

`sudo apt instal haproxy`

Deberemos modificar el archivo de configuración que se encuentra en ***/etc/haproxy/haproxy.cfg****, y hacemos los siguientes cambios en el archivo:

![Img][im8]

inmediatamente después podemos activar el servidor con:

`sudo /usr/sbin/haproxy -f /etc/haproxy/haproxy.cfg`

Una vez levantado el servidor comprobaremos su efectividad como hicimos con el servidor *nginx* en el apartado anterior. Es decir, lanzando el comando *curl* con peticiones a la máquina balanceadora.

En la siguiente imagen podemos ver como la máquina 3, actúa como balanceadora de carga entre la máquina1 y la máquina2.

![Img][im9]



## Sobrecarga de los Servidores
A continuación simularemos la sobrecarga del servidor tanto para nginx, como para haproxy. Así podremos observar su respuesta y poder hacer una comparativa entre ambos servidores.
### Comando ab
que es , hay que tener apache parametros
#### Comando ab sobre el servidor NGINX
A continuación lanzamos el comando sobre el balanceador Nginx.
![Img][im12]
![Img][im13]

#### Comando ab sobre el servidor HAPROXY
Cuando lanzamos el mismo comando contra el servidor HAproxy obtenemos los siguientes datos

![Img][im10]

![Img][im11]

## Comparativa entre las dos máquinas


[im1]:Imagenes/P3/configuracionRoundRobin.png
[im2]:Imagenes/P3/status.png
[im3]:Imagenes/P3/round-robin.png
[im4]:Imagenes/P3/roundrobinWeight.png
[im5]:Imagenes/P3/salidaWeight.png
[im6]:Imagenes/P3/ip.png
[im7]:Imagenes/P3/keep.png
[im8]: Imagenes/P3/configur_haP.png

[im9]: Imagenes/P3/salidaHA.png
[im10]: Imagenes/P3/sobrecargaHA1.png
[im11]: Imagenes/P3/sobrecargaHA2.png
[im12]: Imagenes/P3/abnginx.png
[im13]: Imagenes/P3/abnginx2.png
