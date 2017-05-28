# Discos en RAID

RAID es un acrónimo: Redundant Array of Independent Disk, lo que vendría a significar "conjunto redundante de discos independientes".
Hace referencia a un sistema de almacenamiento de datos en tiempo corto que utiliza múltiples unidades de almacenamiento de datos distribuyendo o duplicando los datos según interese. Esto da a lugar a diferentes tipos de RAID.
La distribución o duplicidad de los datos contribuirá a darle robustez al sistema.
La gestión del RAID se puede hacer por hardware o por software.

## Escenario
Disponemos tres máquinas virtualizadas que disponen de UbuntuServer16
como sistema operativo. Las ip's de dichas máquinas son las siguientes:
* máquina1: 192.168.1.101

Previo a la configuración de RAID deberemos añadir a nuestra máquina de trabajo dos nuevos discos virtuales al controlador SATA

![Img][im1]



### Configuración del RAID por software
Lo primero que deberemos instalar es ***mdadm***, que es una herramienta para la gestión de RAID mediante software en Linux. La instalammos por terminal con:

`sudo apt-get install mdadm`

###### Creación del RAID

A continuación deberemos listar las particiones para ver que identificador tiene los nuevos discos. Utilizaremos el comando:

`fdisk -l`

Podemos observar en la imagen  que los identificadores asignados a los discos han sido *sdb* y *sdc*

![Img][im2]


Para crear el RAID utilizaremos la herramienta *mdadm* con la siguiente línea de comandos podremos crear el RAID usando el dispositivo /de/md0, le indicamos el número de dispositivos que vamos a usar (2), y la ubicación:

`sudo mdadm -C /dev/md0 --level=raid1 --raid-devices=2 /dev/sdb /dev/sdc`


A continuación podemos observar la creación del RAID.
![Img][im3]


En este punto, el dispositivo se habrá creado con el nombre /dev/md0, sin embargo,
en cuanto reiniciemos la máquina, Linux lo renombrará y pasará a llamarlo
/dev/md127.

###### Formato del RAID

Puesto que no hemos reiniciado la máquina, usaremos dev/m0 para darle formato. Ejecutaremos por terminal:
`sudo mkfs /dev/mod`
por defecto iniciará el dispositivo de almacenamiento con formato *ext2*
![Img][im4]


###### Montaje del RAID
crearemos una carpeta para montar la unidad RAID:
~~~~
sudo mkdir /dat
sudo mout /dev/md0 /dat
~~~~
Y a continunación comprobamos si el proceso se ha realizado correctamente con:`sudo mount`

Podemos observar en la imagen que el montaje se ha realizado con éxito.
![Img][im5]


También podemos comprobar el estado del RAID con el comando:

`sudo mdadn --detail /dev/md0`

![Img][im6]

###### Configuración de montaje de RAID en el sistema

Para que el RAID se cree al arrancar el sistema debemos  acceder a `/etc/fstab` y allí añadir la líenea correspondiente pero conviene referenciar al RAID mediante su identificador único (UUID).
Para conocer este identificador deberemos ejecutar:

`ls -l /dev/disk/by-uuid/`

Podemos ver en la imagen el UUID que corresponde a *md0*

![Img][im7]


Recordamos el identificador para poder añadir la orden en el fichero *fstab*, ubicado en ***/etc/fstab***

`UUID=ccbbbbcc-dddd-eeee-ffff-aaabbbcccddd /dat ext2 defaults 0 0`

Podemos ver el aspecto del fichero en la   imagen:

![Img][im8]


Para comprobar que el proceso se realizó con éxito, reiniciamos el sistema y volvemos a ejecutar `sudo mount`.
Podemos ver en la imagen como el disco aparece montado en `/dev/md127`


![Img][im9]


### Simulación de un fallo
Usaremos de nuevo la herramienta *mdadn* para, esta vez, simular un fallo de disco, Lo haremos ejecutando por terminal:
`sudo mdadm --manage --ser-faulty /dev/md127 /dev/sdb`

A continuación chequeamos los detalles del disco con:

`sudo mdadm --detail /dev/md127`

 Podemos ver en la siguiente imagen como, tras la ejecución de los comandos, el disco identificado como *sdb* ha caído.

 ![Img][im10]


Aún así comprobamos que aún se puede acceder a */dat*

![Img][im11]








[im1]:Imagenes/P6/vdi.png
[im5]: Imagenes/P6/mount.png
[im3]:Imagenes/P6/creandoRaid.png
[im4]: Imagenes/P6/mkfsRaid.png
[im6]: Imagenes/P6/mountRaid.png
[im2]:Imagenes/P6/sdb_sdc.png
[im7]: Imagenes/P6/uuid.png
[im8]: Imagenes/P6/fstab.png
[im9]: Imagenes/P6/rebootMount.png
[im10]: Imagenes/P6/fallo1.png
[im11]: Imagenes/P6/dat.png
