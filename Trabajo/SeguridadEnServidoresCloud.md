# Seguiradad en la Nube

## Resumen


La seguridad en la nube es un tema muy controvertido en el sector TI. En esta memoria se tratan los principales aspectos de la seguridad en la nube, empezando por una breve descripción de lo que es la nube, los diferentes tipos de la nube, los servicios que ofrece y por último su modelo de despliegue. Después de esta pequeña introducción al mundo de la nube nos centramos en la seguridad en la nube, repasando la principales y más frecuentes amenazas en la nube, para finalmente llegar a algunas buenas prácticas (best practices) para evitarlas. A continuación para concretar nuestro trabajo de forma realista vamos a ver un caso particular de Dropbox Business donde veremos como maneja/previene las amenazas y cual son sus soluciones para tener una buena seguridad.


### Introducción al Cloud Computing

#### ¿Qué es la nube?

“La nube” es un término que apareció alrededor del año 2006 \cite{wiki1} \cite{comienzos} y que se va extendiendo cada vez más dentro del entorno de la tecnología de la información. El origen del término de “cloud computing” es desconocido[^nota1]
[^nota1]:gygyggy


  pero se usa comúnmente para referenciar un conjunto de servicios informáticos ofrecidos a través de internet. Este concepto ya existia en los años 1970 \cite{wiki3}, conocido como recursos de tiempo compartido y ofrecido por las grandes empresas informaticas como IBM \cite{ibmtimesharing}  o DEC  \cite{dectimesharing}. Pero, ¿Qué es exactamente “la nube”?



> ‘Cloud computing’ es un modelo que permite el acceso ubicuo, conveniente y bajo demanda a un conjunto compartido de recursos informáticos configurables (por ejemplo: redes, servidores, almacenamiento, aplicaciones y servicios) que pueden ser rápidamente provisionados y liberados con un mínimo esfuerzo de gestión o de interacción con el proveedor de servicios.
> Definición oficial del cloud computing de NIST (National Institute of Standards and technology)

#### Tipos de nube y sus caraterísticas

Según la definición oficial de NIST del cloud computing \cite{nist}, este modelo está compuesto por cinco características esenciales, tres modelos de servicio principales y cuatro modelos de despliegue.

###### Características esenciales}

Las características esenciales del cloud computing son \cite{nist} \cite{blogtechnet}:

***Autoservicio por demanda:***  el consumidor puede auto-aprovisionar capacidades de cómputo según necesidades sin requerir interacción humana por parte del proveedor de servicios.

***Acceso amplio desde la red:*** los servicios se pueden acceder desde cualquier dispositivo conectado a la red (teléfonos móviles, tablets, portátiles y ordenadores de sobremesa etc)

***Conjunto de recursos:*** los recursos computacionales del proveedor se habilitan para servir a múltiples consumidores mediante un modelo multi-propietario. El consumidor no tiene control o conocimiento sobre la ubicación concreta de los recursos, pero puede saber/indicar la ubicación a alto nivel de abstracción (por ejemplo: país, región o centro de datos).

***Elasticidad:*** los recursos pueden ser rápidamente y elásticamente provisionados y escalados automáticamente según las necesidades del consumidor.

***Servicio medido:*** los sistemas en la nube son capaces de controlar y monitorizar los recursos usados por el consumidor, proporcionando transparencia sobre el uso de recursos tanto para el proveedor como para el consumidor.


#### Modelos de servicio

Los principales modelos de servicio del cloud computing son \cite{nist} \cite{blogtechnet}:



***Software as a Service (SaaS):*** el modelo consiste en proporcionar al consumidor aplicaciones que se ejecutan en la infraestructura cloud del proveedor, a las que el consumidor puede acceder desde cualquier dispositivo mediante una interfaz web o software. El consumidor no se preocupa por la infraestructura cloud que sostiene dichas aplicaciones como red, servidores, sistemas operativos o almacenamiento.  Algunos ejemplos de este modelo de servicios pueden ser Office Online \cite{officeonline}  , ofrecido por Microsoft, o  Google Docs \cite{googledocs} , ofrecido por Google.

***Platform as a Service (PaaS):*** el modelo consiste en proporcionar al consumidor la habilidad de desplegar en una infraestructura cloud aplicaciones creadas usando distintos lenguajes de programación, librerías, servicios o herramientas soportadas por el proveedor. De nuevo, el consumidor no tiene control sobre la infraestructura cloud del proveedor, pero puede gestionar los despliegues y la configuración del entorno de despliegue en el cual se van a ejecutar sus aplicaciones. Heroku \cite{heroku} y \cite{bluemix} son ejemplos de plataformas como servicio.

***Infrastructure as a Service (IaaS):*** el modelo consiste en proporcionar al consumidor recursos de procesamiento, almacenamiento, redes o otros recursos computacionales fundamentales en los cuales el consumidor pueda desplegar y ejecutar software arbitrario, el cual puede incluir sistemas operativos u otro tipo de aplicaciones. El consumidor no tiene control sobre la infraestructura cloud del proveedor, pero tiene control sobre los sistemas operativos y los recursos donde estos se ejecutan. Microsoft Azure \cite{azure} es un ejemplo de este modelo de servicio.\\

Entre los proveedores de servicios en la nube más conocidos hoy en día se encuentran Amazon (Amazon Web Services) \cite{amazonwebservices}, Microsoft (Microsoft Azure)\cite{azure}, Google (Google Cloud Platform) \cite{googlecloud} e IBM (IBM Cloud) \cite{ibmcloud}, que ofrecen los tres modelos de servicio previamente mencionados, tal y como se puede observar en la siguiente figura.
![Img][im1]
[im1]: img/cloud.jpg


###### Modelos de despliegue

Los modelos de despliegue del cloud computing son \cite{nist} \cite{blogtechnet}: el modelo de nube privada, nube comunitaria, nube pública y nube híbrida. Los dos modelos más comunes son la nube privada y la nube pública. La nube pública vende servicios en Internet a cualquier tipo de consumidor. Las nubes privadas son redes o centros de datos que pertenecen a una organización y que ofrece servicios a un número limitado de personas. Sea privada o pública, el objetivo de la computación en la nube es ofrecer acceso a recursos de computación y servicios de TI de forma sencilla y escalable.


### Implicaciones de la Seguridad en la nube

Los beneficios de la computación en la nube son claros: elasticidad, escalabilidad y pago por uso, pero muchos debaten si la nube es un entorno lo suficientemente seguro para los datos sensibles. La seguridad de los datos en la nube es un tema muy controvertido en el sector TI, donde algunos creen que la nube es más segura que los ambientes internos de una organización, mientras que otros creen lo contrario. Debido a la complejidad del cloud computing, el debate sobre la seguridad en la nube no es tan sencillo, pero una cosa es cierta: no importa si se trata de una nube pública, privada o híbrida, la seguridad es esencial, y los CSPs\footnote{CSP - Cloud Service Provider (proveedor de servicios cloud)} deben asegurar sus infraestructuras \cite{implicaciones seguridad}.

#### Amenazas en la nube

Al trasladarse a la nube, tanto los proveedores de servicios en la nube como las empresas que usan dichos servicios tienen que hacer frente a las amenazas de la computación en la nube, para disminuir los riesgos que suponen el uso de estos servicios. Según varios artículos en la web \cite{amenazas1}\cite{amenazas2}\cite{amenazas3}, algunas de las amenazas de seguridad en la computación en la nube son las siguientes:


***Facilidad de uso.*** Los usuarios finales requieren facilidad de uso, pero los servicios también pueden ser utilizados fácilmente por atacantes para fines maliciosos.

***Transmisión de datos vulnerable.*** Los datos transferidos entre los usuarios y la nube requieren una encriptación adecuada, para evitar los ataques de tipo man-in-the-middle, donde el atacante puede interceptar los datos transmitidos.

***APIs inseguras.*** Varios servicios en la nube están proporcionados mediante APIs que permiten el acceder, controlar e interactuar con los recursos disponibles. Estas APIs son accesibles desde cualquier lugar en internet, por lo tanto es necesario que las interfaces estén diseñadas de forma segura para minimizar la superficie que ataque y disminuir los daños provocados por problemas de seguridad.

***Amenaza interna.*** La amenaza que suponen los propios usuarios es una de las más importantes, ya que tienen acceso de forma natural a los datos y aplicaciones de una empresa. Por tanto, se pueden desencadenar incidentes de seguridad provocados por algún empleado descontento o accidentes por error o desconocimiento.

***Tecnología compartida.*** Esta amenaza afecta especialmente a los modelos IaaS, ya que en este modelo se están compartiendo recursos físicos entre los usuarios que los requieren.

***Pérdida de datos.*** Por varias razones, los datos almacenados en la nube podrían perderse, puede que sea por culpa de un empleado del CSP o de la empresa, de un disco duro que falla o un robo de datos etc, por lo tanto los proveedores tienen que protegerse y tener un respaldo de datos que sirva como sistema de restauración de  datos.

***Brecha de datos.*** Los proveedores que proporcionan máquinas virtuales suelen gestionar muchas VMs sobre el mismo anfitrión  físico, lo que podría dar lugar a una violación de datos. Esto podría provocar que una empresa tenga acceso a datos de otra ya que se encuentran en el mismo servidor físico. Este tipo de amenazas se llaman “ataques de canal lateral” en los cuales los datos se roban de componentes compartidos como por ejemplo la caché del procesador.

***Secuestro de cuenta/servicio.*** Hoy en dia la protección proporcionada por las contraseñas, por compleja que sea, no es suficiente para garantizar la autentificación de un usuario, ya que un atacante que conozca la contraseña tendrá acceso a los servicios. Por tanto hay que proporcionar otras formas de autenticaciones más elaboradas como, por ejemplo, una confirmación por SMS, doble factor de autenticación u otra técnica que asegura que el usuario no es un atacante.

***Perfil de riesgo desconocido.*** Los consumidores deben establecer perfiles de riesgo precisos de sus sistemas e infraestructuras, tienen que estar pendientes de las actualizaciones de seguridad y aplicarlas regularmente. Deben tener sistemas IDS \footnote{ IDS - Intrusion Detection System (sistema de detección de intrusiones)} que detecta los accesos no autorizados, y buscar en los datos externos anomalías que pueden indicar la presencia de ataques y falsas alarmas. También deberían tener un SIEM \footnote{ SIEM - Security Information and Event Management (información de seguridad y administración de eventos)} que reúne los datos de los eventos, de las amenazas y los riesgos para proporcionar la información de seguridad más amplia.

***Denegación de servicio (DoS - Denial Of Service).*** Este tipo de ataque usa los recursos de las computadoras como CPU, RAM o los de la red, como el ancho de banda, para sobrecargar el servidor, saturando los canales de comunicación con flujo de información. Eso hace que el servidor no pueda seguir prestando servicios y como consecuencia causa que los servicios o recursos sean inaccesibles.

***Falta de comprensión.*** Los consumidores necesitan tener los conceptos de la nube bien asimilados y saber a qué se enfrentan a la hora de trasladar sus servicios a la nube, y al establecer un acuerdo con un CSP deberían tener claras las respuestas a ciertas preguntas como: ¿De qué servicios se encarga el CSP y de qué servicios se encarga el consumidor? ¿Cuál sería la estrategia de respaldo proporcionada por el CSP? ¿Y en el caso que el CSP no proporcione ninguna, cuál sería la estrategia adoptada por el consumidor? ¿Los usuarios entienden las amenazas? ¿Saben defenderse adecuadamente contra las amenazas de seguridad en la nube? Todos estos aspectos tienen que ser  contemplados por el consumidor antes de trasladarse a la nube.


#### Buenas prácticas para evitar las amenazas en la nube.

Como podemos ver en el apartado anterior existen dos actores principales que actúan para conseguir una buena seguridad en la nube: los proveedores y los consumidores. A continuación vamos a describir lo que deberían hacer o asegurar cada uno de ellos \cite{buenaspracticas}.

###### Proveedores

Buenas prácticas que deben tener en cuenta los proveedores:

***Seguridad del data center.*** La seguridad del edificio debe ser controlada por varios sistemas de seguridad como protocolos de llaves de accesos, escaneos biométricos , vigilancia dentro y fuera del centro.	Asegurar que solo el personal del Data Center (Centro de Datos) pueda tener credenciales de acceso.	El proceso de  selección de los empleados del centro tiene que ser muy riguroso y pasar por varias comprobaciones antes de ser contratados.

***Seguridad del sistema operativo de la máquina Host.***		 El sistema operativo con el cual cada máquina virtual se está ejecutando sobre la máquina anfitriona requiere una seguridad extra por el simple hecho de que si la máquina virtual es vulnerable no afecte a la máquina anfitriona, pero si el SO anfitrión es vulnerable, esta vulnerabilidad se extiende a todas la máquinas virtuales huéspedes y podría dar acceso a los atacantes a todas la máquinas virtuales.

***El control del Hipervisor.*** El Hipervisor debe asegurar su buen funcionamiento, separando las diferentes máquinas virtuales que gestiona, evitando cualquier tipo de comunicación o intercambios de datos entre ellas, asegurando la individualidad y la integridad de cada máquina.

***Seguridad de la red.*** La política adoptada por el administrador de la red para la seguridad de la red consiste en prevenir los accesos no autorizados, la modificación de la configuración y el mal uso de la red por la máquina o por otro dispositivo de entrada salida. El administrador también implementar y gestionar varios niveles de seguridad controlando los permisos de los accesos a la red.



###### Consumidores

Buenas prácticas que deberían tener en cuenta los consumidores de servicios en la nube:


***Hardware Firewalls (Cortafuegos hardware).*** Suelen encontrarse en los routers, son fáciles de configurar y protegen todas la máquinas de la red local.

***Software Firewalls (Cortafuegos software).*** Suelen ser instalados en cada máquina de forma individual y solo protegen esa máquina. Básicamente controlan todo acceso o posibilidad de acceso a la máquina por una tercera entidad. Es una herramienta muy potente y de las mejores para proteger las máquinas virtuales del cliente.

***Parches y copias de seguridad.*** Los parches son actualizaciones del software a la última versión aplicadas de forma individual a cada dispositivo, y son muy importantes para protegerse de nuevas amenazas. Las copias de seguridad son importantes también ya que nunca se sabe cuando puede haber una pérdida de datos o un simple corte de conectividad. Usando una copia de seguridad se pueden recuperar los datos perdidos o usar las copias para una continuidad de los servicios del sistema.

***Contraseñas.***	Muchas empresas invierten grandes cantidades de dinero y tiempo en buenos cortafuegos y chequeos de seguridad, pero aún y así puede que hayan brechas, por el simple hecho de tener contraseñas inseguras. Los usuarios deben seguir unos criterios estrictos a la hora de crear contraseñas como la complejidad, una fecha de expiración, usar contraseñas diferentes para cada servicio o no repetir contraseñas usadas anteriormente .

***Seguridad de la máquina virtual.*** Para una buena seguridad de la máquina virtual, ‘the Center for Internet Security’ \cite{centerinternetsecurity} recomienda algunas buenas prácticas (best practices) a seguir:



		* Cortafuegos en los puertos de acceso a la máquina virtual.
		*  El uso de una comunicación cifrada.
		*  La utilización de un sistema operativo reforzado para la VM.
		*  La desconexión de los dispositivos no utilizados
		* La comprobación de la integridad de los archivos.
		* El uso de contraseñas seguras.
		* El uso de copias de seguridad.
		* El uso de registro de auditoría.
		* El uso de hosts basados en detección/prevención de intrusiones  (IDS / IPS).
		* El uso de técnicas de cifrado de datos (File / DB\footnote{BD - Base de Datos}).





### Caso particular

Después de haber visto la descripción del cloud computing, su funcionamiento y los diferentes servicios que ofrece, y haber identificado varias amenazas y las soluciones a ellas, tanto en los proveedores como en los clientes, nos centrarnos en el estudio de un caso particular para ver cómo se aplica todo lo presentado anteriormente en la vida real. Hemos elegido *Dropbox* \cite{dropbox}, ya que es una aplicación cotidiana para muchos de los usuarios del internet. \\

Dropbox es un servicio de alojamiento de archivos multiplataforma en la nube, operado por la compañía *Dropbox, Inc.*. El servicio permite a los usuarios almacenar y sincronizar archivos en línea y entre distintos dispositivos y compartir archivos y carpetas con otros usuarios.
Dropbox como SaaS (Software-as-a-Service) ofrece 3 tipos de cuentas la primera es gratuita, “Free”, la segunda es la “Pro” y la tercera es la “Business”, y se diferencian en la cantidad de almacenamiento ofrecido, herramientas para la administración en equipo y por el coste de los servicios. De todas las versiones, nos vamos a enfocar en un producto en concreto, *Dropbox Business* \cite{dropboxbusiness}, ya que requiere más seguridad que las otras versiones de Dropbox.

### Seguridad de DropBox Business

A continuacion se presenta la arquitectura de la infraestructura de Dropbox y las diferentes capas de seguridad \cite{sec_architecture}.

#### Descripción de la arquitectura de Dropbox Business}

Dropbox ha sido diseñado con varias capas de protección que se adaptan a las diferentes interfaces como el escritorio, el sitio web, móviles y aplicaciones de terceros vinculadas a Dropbox. Todos estos clientes se conectan a servidores seguros que proporcionan acceso a los archivos, de manera que estos se puedan modificar o compartir de forma segura. La figura \ref{fig:arquitectura} muestra la arquitectura de la infraestructura de Dropbox.

![Img][im2]
[im2]:img/arquitectura.png


A continuación vamos a ver los diferentes servicios de esta arquitectura y cómo lo hacen seguro.

***Servicio de aplicación y cifrado.*** Este servicio procesa todas las aplicaciones de Dropbox. Cada archivo se divide en bloques, y cada bloque se codifica o se le aplica un algoritmo hash mediante un cifrado potente. Sólo se sincronizan los bloques modificados. Cuando se produce un cambio, los bloques nuevos o modificados se procesan y se transfieren al servicio de almacenamiento.
\paragraph{Servicio de almacenamiento.} Este servicio se encarga de almacenar en bloques cifrados el contenido de los archivos de los usuarios. La recuperación  de cada bloque individual cifrado de archivos se hace mediante su valor hash y se añade una capa adicional de codificación a todos los bloques de archivos mediante un fuerte cifrado.
***Servicio de metadatos.*** Este servicio se encarga de almacenar la información básica acerca de los archivos del usuario, y se guardan en un servicio distinto al de los bloques de archivos. Estos metadatos funcionan como índice de datos en las cuentas de los usuarios, se dividen y se replican según sea necesario para cumplir con los requisitos de disponibilidad total y rendimiento.  

***Servicio de notificaciones.*** Este servicio se encarga de controlar si se producen cambios en las cuentas de Dropbox y notificarlos. Con este servicio el cliente puede seguir los cambios en tiempo real y detectar si un cambio ha sido hecho por una persona autorizada o no.


###### Otros puntos de la seguridad de la arquitectura

***Centros de datos.***
	Dropbox aloja los sistemas corporativos y de producción en centros de datos de terceros y proveedores de servicios gestionados y situados en los Estados Unidos. Aquí la seguridad se hace por parte de estos proveedores externos, que son los responsables de controlar sus instalaciones, pero, como lo hemos comentado anteriormente, las dos partes tienen que cumplir el acuerdo previamente establecido y las reglas exigidas por el cliente que en este caso es Dropbox.
***Cifrado.***
Dropbox cifra los datos almacenados mediante el estándar Advanced Encryption Standard (AES) de 256 bits, y para la transferencia de datos usa las tecnologías Secure Sockets Layer (SSL)/Transport Layer Security (TLS) creando un túnel seguro protegido por un cifrado con Advanced Encryption Standard (AES) de 128 bits o superior para proteger los datos en tránsito entre las aplicaciones de Dropbox y sus servidores.
***Comprobación de certificado.***
	Dropbox usa un control adicional que es la fijación de certificados, este control asegura que el servicio al que se conecta el cliente es realmente quien dice ser. Este control está pensado para proteger el cliente de ataques más sofisticados por parte de ataques más avanzados.
***Confidencialidad directa total.***
	Para los varios dispositivos y navegadores que usa el cliente, Dropbox usa cifrados potentes y admite confidencialidad directa total. Eso quiere decir que la clave privada de SSL no se puede utilizar para descifrar tráfico de internet que ha tenido lugar anteriormente. Con esta técnica Dropbox agrega otra capa de protección a las comunicaciones cifradas y además todos los cookies de autenticación están marcados como seguros y habilitan una seguridad de transporte HTTP estricta (HSTS\footnote{HTST -   HTTP Strict Transport Security})
{Administración de claves.}
	La infraestructura de administración de claves de Dropbox está diseñada con con controles de seguridad operativa, con un acceso muy limitado a las claves y el intercambio y el almacenamiento de distribuyen para permitir el procesamiento descentralizado. Además de esto Dropbox usa un sistema interno que administra el proceso de intercambio seguro de claves públicas, de manera que las claves privadas se almacenan de forma segura.


###### Control y visibilidad

Dropbox adapta y personaliza su servicio Dropbox Business según las demandas particulares de sus organizaciones. Dropbox ha desarrollado varias herramientas con características de control y visibilidad disponibles a través de la Consola de administración de Dropbox Business y de sus diversas interfaces de usuario \cite{sec_control}. A continuación vamos a ver estas herramientas y su forma de hacer que Dropbox Business sea seguro.\\

***Gestión de acceso e identidades***



* ***Integración de servicios de directorio activo.***
Para simplificar la tarea de otorgar y anular permisos, los servicios de Dropbox Business están integrados con LDAP\footnote{ LDAP - Lightweight Directory Access Protocol (Protocolo Ligero/Simplificado de Acceso a Directorios)} o Active Directory (Directorio Activo), o utilizan uno de los proveedores de gestión de identidades.

* ***Inicio de sesión único (SSO - Single Sign-On)***\cite{sso}.
	Dropbox usa un sistema de inicio de sesión único (SSO) proporcionado por otros proveedores oficialmente respaldados, y  es un procedimiento de autenticación que permite al usuario acceder a varios servicios con una única instancia de identificación. También usa una solución propia que cumple con SAML 2.0 (Security Assertion Markup Language 2.0).

* ***Verificación en dos pasos.***
	Es un técnica muy común hoy en día, utilizada especialmente por la entidades bancarias a la hora de hacer transferencias o en las compras on-line y consiste en solicitar un código de seguridad de seis dígitos, además de la contraseña requerida en el momento de iniciar sesión o vincular un nuevo dispositivo. Dropbox usa esta verificación de forma opcional pero es aconsejable ya que añade otra capa de seguridad.

* ***Dos cuentas Dropbox (personal y de trabajo).***
	Dropbox Business permite a los usuarios elegir conectarse a su Dropbox personal o a su Dropbox de trabajo en todos sus dispositivos y eso permite una separación entre los archivos de la cuenta del trabajo y los de la cuenta personal.




***Uso compartido y controles de archivos***


El objetivo principal de Dropbox es compartir archivos, pero de manera controlada, de forma que no permita accesos no autorizados o un mal uso de los servicios. Los administradores están continuamente controlando quién puede compartir un archivo o quien no, y hasta donde llegan los permisos de cada usuario.



* ***Permisos de carpetas y archivos compartidos***
	Las restricciones de permisos para carpetas y archivos se limita a dos hechos bastante comunes: los permisos de lectura/escritura que consisten en habilitar la escritura (modificar) un archivo o una carpeta, o solo habilitar el permiso de lectura, y el acceso con contraseñas y fechas de caducidad para vínculos compartidos que consiste en definir quienes pueden acceder al contenido por medio de contraseñas y establecer un fecha de caducidad para los vínculos compartidos a fin de proporcionar un acceso temporal.
* ***Recuperación e historial de versiones***
	Dropbox Business permite la recuperación de los datos eliminados o modificados anteriormente de forma ilimitada, es decir, sin restricción temporal, de esta forma se pueden seguir los cambios en los datos y la recuperación de versiones anteriores.



***Acciones administrativas***


Las acciones del administrador son muy variadas y algunos de los objetivos que tienen incluyen supervisar los dispositivos vinculados y aplicaciones de terceros además de las sesiones web activas. Los administradores tienen autorización para cerrar sesiones abiertas, eliminar copias locales, revocar accesos de aplicaciones de terceros y como medida de seguridad proactiva puede restablecer contraseñas de cada usuario o equipo.



* ***Desvincular dispositivos***
	Como hemos visto antes, el administrador puede desvincular las computadoras y los dispositivos móviles vinculados a las cuentas de usuarios y lo puede hacer mediante la consola de administración. En el caso de tratarse de una computadora, la desvinculación elimina los datos de autentificación y ofrece la opción de eliminar copias locales de los archivos, en el caso de los dispositivos móviles la desvinculación elimina los archivos marcados como favoritos, los datos de la caché y por último la información del inicio de sesión.
* ***Borrado remoto***
	El borrado remoto proporcionado por Dropbox business permite proteger los datos de las empresas cuando los empleados abandonan el equipo o extravían un dispositivo, de esta forma se pueden eliminar datos o copias locales en las computadoras o en los dispositivos móviles.  
* ***Transferencia de  cuenta***
	El control del administrador se expande todavía más con esta nueva característica que le permite transferir datos entre cuentas de usuarios como, por ejemplo, el aprovisionamiento de una nueva cuenta de usuario.



***Visibilidad - Registros de actividades completos***

\paragraph{}
Los administradores de Dropbox Business pueden generar informes de actividades en cualquier momento para tener un control y poder auditar todas las actividades que los usuarios realizan. Los informes de actividad proporcionan, entre otros puntos, datos sobre cambios en la configuración de contraseñas o verificación en dos pasos (aunque no pueden ver las contraseñas de los usuarios), y sobre los inicios de sesión (tanto correctos como intentos fallidos), sobre la vinculación de aplicaciones de terceros a las cuentas Dropbox, sobre el uso compartido de las carpetas, ficheros y enlaces a estos. Además, cada usuario puede ver las actividades realizadas sobre sus archivos y carpetas desde la página de eventos del usuario.

\subsubsection{Seguridad de la información}

Dropbox consigue mantener la confianza de sus usuarios mediante la evaluación de los riesgos y la mejora continua de la seguridad, confidencialidad, integridad y disponibilidad de los servicios que ofrecen. Entre otros, los puntos más importantes para mantener la seguridad al día son las políticas de seguridad, el control de acceso, la seguridad de la red y la administración de cambios \cite{sec_seg_inf}.


***Políticas de seguridad.***
Las políticas de seguridad de Dropbox Business se aplican a varios activos/servicios que ofrecen, como la seguridad de la información, seguridad física, respuesta a incidentes, acceso lógico, acceso físico a los sistemas de producción, gestión de cambios y asistencia.

***Control de acceso.***
Dropbox mantiene un control de acceso estricto a sus empleados, para disminuir la amenaza interna que hemos visto previamente, controlando los acceso mediante un directorio central y un sistema de autenticación combinado entre contraseñas seguras, claves SSH y autenticación en dos pasos. El acceso remoto a los servicios por parte de los empleados requiere el uso de una VPN protegida con autenticación en dos pasos y bajo previa aprobación del equipo de seguridad. El control de acceso está definido en las políticas internas, que requieren que los empleados usen los métodos de autenticación previamente mencionados. Los metadatos y otros datos de las cuentas de los usuarios también se encuentran bajo el control de acceso, de esta manera los clientes pueden estar seguros de que los detalles de sus cuentas están bajo supervisión.

***Seguridad de la red.***

La seguridad de la red es uno de los puntos más importantes, por lo que Dropbox identifica y reduce los riesgos mediante pruebas y auditorías de las aplicaciones y redes, pruebas de penetración y otros aspectos de la seguridad. Además, aplican técnicas de supervisión y seguridad de la red que están diseñadas para ofrecer múltiples capas de protección y defensa.\\

Dropbox emplea técnicas de protección como cortafuegos, supervisión de la red y sistemas de detección de intrusiones, garantizando la seguridad del entorno de producción y que sólo el tráfico permitido pueda llegar a la infraestructura interna.

***Administración de cambios.}

Todos los cambios de la infraestructura o aplicaciones están previamente autorizados mediante una política de administración de cambios antes su implementación en las aplicaciones. Todos los cambios están gestionados y guardados mediante un sistema de control de versiones y deben someterse a procedimientos de pruebas de control de calidad para verificar que cumplen los requisitos de seguridad. Todos los cambios de código están revisados manualmente pasan un control de calidad.


\section{Conclusiones}

Ya sabemos qué es la nube y cuáles son, en general, las ventajas y los riesgos de usar los servicios que ofrece. Todos los métodos que hemos visto para implementar la seguridad deberían hacer la nube un entorno lo suficientemente seguro para sobrepasar cualquier tipo de incidente, aunque el error humano puede provocar brechas en la seguridad. Remarcamos que la seguridad en la nube debería ser una relación entre los proveedores y los consumidores, donde cada uno tiene la responsabilidad de asegurar su entorno. Teniendo esto en cuenta, los servicios ofrecidos por la nube deberían ser mucho más flexibles y seguros que los métodos tradicionales. Pero como cada proveedor es diferente, tenemos que evaluar los áreas de seguridad que ofrecen antes de migrar a la nube.



\section{Referencias}
\bibliography{bibliografia}
