# Práctica3: Balanceo de carga
### Escenario
Disponemos tres máquinas virtualizadas que disponen de UbuntuServer16
como sistema operativo. Las ip's de dichas máquinas son las siguientes:
* máquina1: 192.168.1.101
* máquina2: 192.168.1.102
* máquina3 (Balanceador de carga): 192.168.1.103

### Qué es el banlanceo de carga y cuando utilizarlo
El tráfico de Internet está en constante crecimiento y por tanto ampliar la memoria del servidor solo es una solución temporal. La opción más razonable es, a largo plazo, configurar más servidores y repartir las peticiones de los clientes entre ellos. Esto incrementa la velocidad de acceso del usuario al servidor, mejora la fiabilidad del sistema y la tolerancia a fallos, permitiendo reparar o mantener cualquier servidor en línea sin que afecte al resto del servicio.
La forma más elemental para hacer este balanceo de carga entre servidores, es utilizar un DNS. Este tipo de balanceo resulta sencillo y eficaz, solo necesitaremos varias máquinas que dispongan de diferentes ip's. El inconveniente del balanceo mediante un servidor DNS, es que este no tendrá en cuenta la carga de trabajo a la que está sometido el servidor.

## Balanceo de carga  con  Round-Robin
Instalaremos nginx, un servidor web de código abierto. La instalación es sencilla mediante terminal:

`sudo apt-get install nginx`
