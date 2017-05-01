
# Ejercicios del Tema1
##### Buscar información sobre las tareas o servicios web para los que se usan más los programas que comentamos al principio de la sesión:
* ***Apache***
* ***nginx***
* ***thttpd***
* ***Cherokee***
* ***node.js***

## APACHE (1995)

Es el más conocido de los servidores web HTTP,  creado en 1995, se trata de un servidor de código abierto, para plataformas Unix. Para  Microsoft Windows, Macintosh y otras plataformas necesitan del protocolo HTTP/1.1. Una de las principales características de Apache es que es extendible mediante módulos, los cuales posibilitan varias tareas:
* Manejo de distintas conexiones.
* Interpretar gran variedad de lenguajes, como PHP,  sin necesidad de recurrir a herramientas externas.
* Ejecución de contenido dinámico dentro del propio servidor sin necesidad de otros medios.
* Carga y descarga de módulos mientras el servidor está ejecutnándose.

Apache permite una configuración distribuida del servidor, además posee unos ficheros *htacces* que permiten configurar los permisos de los diferentes usuarios y controlar los accesos al servidor

## NGINX (2008)

Se trata de un servidor web/proxy inverso ligero de alto rendimiento y un proxy para protocolos de correo electrónico (IMAP/POP3).

Un proxy inverso es un servidor  proxy que, en lugar de permitir el acceso a Internet a usuarios internos, permite a usuarios de Internet acceder indirectamente a determinados servidores internos.
El servidor de proxy inverso es utilizado como un intermediario por los usuarios de Internet que desean acceder a un sitio web interno al enviar sus solicitudes indirectamente.


Es software libre y de código abierto, licenciado bajo la Licencia BSD simplificada; también existe una versión comercial distribuida bajo el nombre de nginx plus.3 Es multiplataforma, por lo que corre en sistemas tipo Unix (GNU/Linux, BSD, Solaris, Mac OS X, etc.) y Windows.4

Es un servidor muy demandando en los últimos tiempos, ya que es capaz de soportar gran carga de trabajo, lo que viene siendo muy necesario debido al aumento del tráfico en internet.
Además de haberse adaptado al volumen del tráfico actual, nginx está diseñedo para soportar miles de conexiones mediante hebras, lo que optimiza el uso de la CPU y la memoria. ES un servidor altamente eficiente y robusto, ya que no da permisos a los usuarios del sistema, pero poco configurable. No permite ni dar permiso ni carga o descarga dinámica de contenidos.

## THTTPD (2003)
 Es un servidor web de código libre disponible para la mayoría de las variantes de Unix. Se caracteriza por ser simple, pequeño, portátil, rápido, y seguro, ya que utiliza los requerimientos mínimos de un servidor HTTP. Esto lo hace ideal para servir grandes volúmenes de información estática.
 * Simple, porque esto maneja solo el mínimo necesario para poner en práctica el protocolo HTTP, algunas veces un poco más que el mínimo.

* Uso mínimo de la memoria para la ejecución.

* Portabilidad,  Se compila para la mayoría de sistemas operativos, incluyendo FreeBSD, SunOS 4, Solaris 2, BSD/OS, GNU/Linux, OSF.

* Rápido, Responde bien sobretodo en escenarios de alta carga de trabajo.

## CHEROKEE (2001)
 Servidor web multiplataforma de código libre.
Es un servidor que pretende ser rápido y completamente funcional, sin dejar de ser liviano frente a otros servidores web. Está escrito completamente en C. Puede usarse como un sistema embebido y extendible mediante módulos.

Soporta distintas  tecnologías web como: FastCGI, SCGI, PHP, CGI, SSI, SSL/TLS.5
Soporta la configuración de servidores virtuales.
.

## NODO.JS (2009)

Es un entorno  JavaScript asíncrono orientado a eventos, lo que significa que  el servidor actuará cuando se produzca el evento. Es código abierto, fue creado con el enfoque de ser útil en la creación de programas de red altamente escalables, como por ejemplo, servidores web.

 Al contrario que la mayoría del código JavaScript, no se ejecuta en un navegador, sino en el servidor.
Node.js incorpora varios "módulos básicos" compilados en el propio binario, como por ejemplo el módulo de red,pero también es posible utilizar módulos desarrollados por terceros, ya sea como archivos ".node" precompilados, o como archivos en javascript plano.

Node.js puede ser combinado con una base de datos documental (por ejemplo, MongoDB o CouchDB) y JSON lo que permite desarrollar en un entorno de desarrollo JavaScript unificado.
