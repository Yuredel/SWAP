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

## Balanceo de carga  con  Round-Robin
#### Configuración
Instalaremos nginx, un servidor web de código abierto. La instalación es sencilla mediante terminal:
~~~~
sudo apt-get update && sudo apt-get dist-upgradde && sudo apt-get autoremove
sudo apt-get install nginx
~~~~
Para poder utilizar el servidor como Balanceador, deberemos acceder al fichero***/etc/nginx/conf.d/default.conf***, e introducir los siguientes cambios:
![Img][im1]

Para que el servidor deje de funcionar como un servidor web deberemos comentar la siguiente línea del fichero de configuración de *nginx* ubicado en la siguiente ruta:

`/etc/nginx/nginx.conf`

Ahí deberemos comentar la siguiente línea:

`include /etc/nginx/sites-enabled/*`

A continuación pondremos en marcha el servicio de la siguiente manera:

`sudo systemctl start nginx`

Si la configuración es correcta, al efectuar 'systemctl status nginx.service', podremos ver la siguiente respuesta:
![Img][im2]

#### Puesta en marcha del servicio
Mediante la anteriormente utilizada, curl, podremos lanzar diversas peticiones al Balanceador y podremos apreciar como distribuye las peticiones según la filosofía Round-Robin. Ejecutamos El comando sobre la dirección ip que le hemos adjudicado al balanceador, en este caso *192.168.1.103*.
Vemos en la siguiente figura como se alternan las respuestas del servidor.
![Img][im3]






# Solucionando problemas
## Al levantar el NGINX
## El servidor

[im1]:/Imagenes/P3/configuracionRoundRobin.png
[im2]:/Imagenes/P3/status.png
[im3]:/Imagenes/P3/round-robin.png
