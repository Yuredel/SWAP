# Replicación de una base de datos en MySQL

### Escenario
Disponemos tres máquinas virtualizadas que disponen de UbuntuServer16
como sistema operativo. Las ip's de dichas máquinas son las siguientes:
* máquina1: 192.168.1.101 (maestro)
* máquina2: 192.168.1.102 (esclavo)

### Creación de una Base de Datos
 Para empezar crearemos una pequeña base de datos mediante comandos de MySQL
 ![Img][im1]

 ### Replicar la Base de Datos
 La herramienta que proporciona MySQL es ***mysqldump***,  parte de los  programas de cliente de MySQL, que puede ser utilizado para generar respaldos de bases de datos y ser usados o incluso para ser transferidos a otro servidor de base datos SQL (No estrictamente tiene que ser un servidor MySQL).

Podemos ver todas sus opciones ejecutando:

`mysqldump --help`

Debemos tener especial cuidado con las opciones --quick o --opt ya que carga el resultado en memoria antes del volvado y podría llegar a resultar un problema con bases de datos muy grandes.

### Clonar una Base de Datos
Si quisiéramos clonar la Base de Datos anteriormente creada, deberíamos ejecutar:

`mysqldump contactos -u root -p > /root/contactos.sql`

Si queremos asegurar que la máquina principal no estaba ejecutando ningún tipo de modificación sobre la base de datos mientras estábamos ejecutando la copia, deberemos ejecutar:
~~~~
mysql -u root –p
mysql> FLUSH TABLES WITH READ LOCK;
mysql> quit
~~~~
Esto deberá dejar bloqueada a la máquina principal mientras hacemos el volcado de la base de datos:

`mysqldump contactos -u root -p > /root/contactos.sql`

Para desbloquear a la máquina principal deberemos ejecutar:
~~~~
mysql -u root –p
mysql> UNLOCK TABLES;
mysql> quit
~~~~

Es importante destacar que la copia de seguridad tiene formato de texto plano,pero la orden mysqldump no incluye
sentencias para crear la BD , es decir que deberemos crear previamente la base de datos en la máquina secundaria
~~~~
mysql -u root –p
mysql> CREATE DATABASE ‘ejemplodb’;
mysql> quit
~~~

Y a continuación restauramos la BD (se crearán las
tablas en el proceso):

`mysql -u root -p ejemplodb < /tmp/ejemplodb.sql`

También podemos hacerlo por ssh pero también será necesario haber creado previamente la base de datos.
mysqldump ejemplodb -u root -p | ssh equipodestino mysql


#### Ejemplo
A continuación podemos ver como se hace una copia de la Base de Datos.
* Primero entramos en MySQL por terminal:

    ` mysql -u root –p`

* Bloqueamos la Base de Datos:
![Img][im2]

* Salimos d MySQL, y ejecutamos por terminal el comando de copia:
![Img][im3]
Vemos como se ha creado la copia.

* Volvemos MySQL y desbloqueamos la Base de Datos:
![Img][im4]

### Importar la copia desde la máquina 1.
Desde la máquina secundaria copiaremos la base de datos mediante el comando *scp*.
![Img][im5]

Como se comentaba anteriormente, deberemos crear la Base de Datos en la máquia secundaria antes de restaurarla.
* Primero entramos en MySQL por terminal:

    ` mysql -u root –p`

* Creamos la Base de Datos:

    `create database contacto`

* Restauramos la Base de Datos como se ve en la imagen:
![Img][im6]

### Restaurar la Base de Datos mediante el modelo ***Maestro-Esclavo***
A continuación vamos a automatizar todo el proceso:

#### Máquina Maestra
* Lo primero que debemos hacer es configurar MySQL en la máquina Maestra. Para ello editaremos el fichero que encontramos en:
`/etc/mysql/my.cnf`

  Según la versión, como es mi caso, también podríamos encontrar el fichero en:

  `/etc/mysql/mysql.conf.d/mysqld.conf`

  * Comentamos el parámetro bind-address que sirve para que escuche a un servidor:

    `#bind-address 127.0.0.1`

  * Indicamos el archivo donde almacenaremos el log de errores: `log_error = /var/log/mysql/error.log`

  * Establecemos el identificador del servidor:

    `server-id = 1`

  * El registro binario contiene toda la información que está disponible en el registro de actualizaciones, en un formato más eficiente y de una manera que es segura para las transacciones:
      `log_bin = /var/log/mysql/bin.log`


* Podemos guardar los cambios y restablecer el servicio:
`/etc/init.d/mysql restart`
![Img][im11]

#### Máquina esclavo
La máquina esclavo se configurará igual solo que en el valor de server id se colocará un valor de 2, al descomentar la directiva.
`server-id = 2`




[im1]: Imagenes/P5/BD1.png
[im2]: Imagenes/P5/cop1.png
[im3]: Imagenes/P5/cop2.png
[im4]: Imagenes/P5/cop3.png
[im5]: Imagenes/P5/maq2cop1.png
[im6]: Imagenes/P5/maq2cop2.png
[im7]: Imagenes/P5/bin.png
[im8]: Imagenes/P5/log.png
[im9]: Imagenes/P5/server.png
[im10]: Imagenes/P5/logbin.png
[im11]: Imagenes/P5/restart.png
