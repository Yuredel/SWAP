# Práctica2: Clonar la Información de un sitio Web
## Crear un tar con fichero locales en una máquina remota

#### Escenario
Disponemos dos máquinas virtualizadas que disponen de UbuntuServer16 como sistema operativo.En la práctica anterior, configuramos las interfaces de red para que cada máquina dispusiera de una ip diferent. Partiendo de esta casuística, podremos utilizar las funciones que nos proporciona la herramienta ssh para comunicar ambas máquinas.
#### Probar el funcionamiento de la copia  de archivos por ssh
aUsaremos el comando tar para comprimir el archivo deseado, de la siguiente manera:  

` tar czf - directorio | ssh equipo\_destino 'cat > ~/tar.tgz' `

![Imagen][im1]  
figura1: Ejecución del comando ***tar*** en la máquina origen

## Clonado de una carpeta entre las dos máquinas remotas

#### Instalación de la herramienta *** RSYNC***

La instalación de la herramienta en Linux, es sencilla y puede hacerse fácilmente  desde la terminal mediante el siguiente comando:  

  `sudo apt-get install rsync`


Aunque podemos optar por trabajar como root, utilizaremos el usuario sin privilegios para las tareas que llevaremos a cabo a lo largo de esta práctica. Sin embargo si haremos al usuario dueño de la carpeta del espacio web sobre la que estamos trabajando, de la siguiente manera:

 `sudo chown yurena:yurena -R /var/www/html`

#### Comprobación del funcionamiento de la herramienta

Probaremos el funcionamiento clonando una carpeta de la máquina origen(192.168.1.101) a la máquina destino (192.168.1.102). Ejecutaremos la siguiente instrucción en la máquina destino:

`rsync -avz -e ssh 192.168.1.101:/var/www/html/ /var/www/html/ `

El protocolo ***ssh*** nos pedirá la contraseña para ejecutar la operación, de la misma forma en que lo hizo las anteriores veces que utilizamos este recurso.    
Una vez hayamos introducido la contraseña correctamente podremos comprobar que el contenido del directorio de la máquina origen ha quedado clonado en la máquina destino.

![Imagen][im2]  
figura2: Ejecución de rsync

La herramienta ***rsync*** permite multitud de parámetros para seleccionar que archivos copiar y que archivos no, por ejemplo. A continuación se muestra una ejecución del comando rsync donde se hace una copia del directorio /var/www/html/ pero excluyendo:
* /var/www/html/error
* /var/www/html/stats
* /var/www/html/files/pictures

Esto se realizará mediante las siguientes opciones del comando:

` rsync -avz --delete --exclude=\*\*/stats --exclude=\*\*/error --exclude=\*\*/files/pictures -e ssh  *ip_máquina_origen* :/var/www/html/ /var/www/html/`

* --delete: indica que los ficheros que han sido borrados en la máquina origen también se borren en la máquina destino. Esto hace que el clonado sea perfecto.
* --exculde: indica que algunos ficheros deben ser excluidos o que no deben copiarse

En la siguiente figura podemos ver la ejecución del comando.

![Imagen][im3]
figura3: Ejecución del comando rsync

## Acceso sin contraseña para ***ssh***
Para automatizar esta tarea, necesitaremos que ssh nos permita el intercambio de información entre máquinas remotas, sin contraseña. Para ello, normalmente se utilizará la autenticación con un par de claves públicas-privadas.  
Mediante ssh-keygen podremos generar la clave indicando con la opción -t el tipo de clave.   
Tenemos, pues, que si ejecutamos  en la máquina destino el siguiente comando:

`ssh-keygen -b 4096 -t rsa `

Obtendremos como repuesta la siguiente salida que se muestra a continuación:

![Imagen][im4]

![Imagen][im5]

figuras 4 y 5: creación de la clave pública

![Imagen][im6]
figura6: Ejecución del comando *ssh* sin contraseña

## Programar tareas con  ***CRONTAB***
 En el sistema operativo Unix, ***cron*** es un administrador regular de procesos en segundo plano (demonio) que ejecuta procesos o guiones a intervalos regulares (por ejemplo, cada minuto, día, semana o mes). Los procesos que deben ejecutarse y la hora en la que deben hacerlo se especifican en el fichero crontab.  
Los siete campos están organizados de la siguiente manera:
* Minuto: Indica el minuto de la hora en que la instrucción será ejecutada.
* Hora: Indica el día del mes en que se quiere ejecutar la instrucción.
* Día del Mes: Indica el día del mes en que se quiere ejecutar la instrucción.
* Mes: Indica mediante un entero entre el 1 y el 12, el número del mes en que será ejecutada la instrucción.
* Día de la Semana: Indica el Usuario que ejecuta la instrucción.
* Instrucción: comando y parámetros que se ejecutarán llegado el momento.

Por tanto:

`* * * * * * comando`

representará una tarea que se realiza cada minuto de cada día de cada mes.

Como hemos configurado ssh para que tenga un acceso remoto y sin contraseña, tan solo habremos de añadir la instrucción de acceso mediante ssh a crontab para poder hacer las copias de seguridad de nuestro directorio de forma automática.

#### Establecer una tarea en cron que se ejecute cada hora para mantener actualizado el contenido de ambas máquinas y del software

A continuación se muestra el aspecto del fichero crontab, donde, en la última línea se especifica la realización de una copia de seguridad de los ficheros albergados en el directorio */var/www/html*, durante el primer minuto de cada hora.

![Imagen][im7]








[im2]:Imagenes/rsync.png
[im1]:Imagenes/tar_desde_origen.png
[im3]:Imagenes/rsyncCompleto.png
[im4]: Imagenes/maq1.png  
[im5]: Imagenes/maq1_2.png  
[im6]: Imagenes/maq2.png  
[im7]: Imagenes/crontab.png
