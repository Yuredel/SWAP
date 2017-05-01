# Ejercicios del Tema2: Alta Disponibilidad y Escalabilidad

### Calcular la disponibilidad del sistema si tenemos dos réplicas de cada elemento (en total 3 elementos cada subsistema)
En cualquier sistema con N componentes para calcular la disponibilidad del sistema se calcula como:

As = Ac1 * Ac2 * Ac3 * ... * Acn

En este caso seria : As = Ac1 + (1-Ac1) * Ac2

***Web***

Web_2= 0.85+(1-0.85)* 0.85 = 0.9775 (97.75%) Web_3= 0.9775+(1-0.9775)* 0.85 = 0.9966

***Application***

App_2= 0.9+(1-0.9)* 0.9 = 0.99 App_3= 0.99+(1-0.99)* 0.9 = 0.999

***Database***

Db_2=0.999+(1-0.999)* 0.999 = 0.99999 Db_3=0.99999+(1-0.99999)* 0.999 = 0.9999999

***Domain Name System***

DNS_2= 0.98+(1-0.98)* 0.98 = 0.9996 DNS_3 0.9996+(1-0.9996)* 0.98 = 0.9999

***Firewall***

Firewall_2= 0.85+(1-0.85)* 0.85 = 0.9775 Firewall_3= 0.9775+(1-0.9775)* 0.85 = 0.9966

***Switch***

Switch_2= 0.99+(1-0.99)* 0.99= 0.9999 Switch_3= 0.9999+(1-0.9999)* 0.99= 0.999999

***Data Center***

DC_2= 0.9999+(1-0.9999)* 0.9999 = 0.99999999 DC_3= 0.99999999+(1-0.99999999)* 0.9999 = 0.999999999999

***Internet Service Provider***

ISP_2= 0.95+(1-0.95)* 0.95 = 0.9975 ISP_3= 0.9975+(1-0.9975)* 0.95 = 0.999875

***As*** = Web_3App_3Db_3DNS_3Firewall_3Switch_3DC_3*ISP_3 = 0.9908

***Solucion = 99.08%***

### Buscar frameworks y libreriías para diferentes lenguajes que permitan hacer aplicaciones altamente disponibles con relativa facilidad.
* Forever:
* Pacemaker:
* Keepalived:

* Ruby: Lotus, Nyny, Grape, Pakyow, Celluloid
* PHP: Medoo, Flight, Phpixie, Yii, Codeigniter, Laravel, Phalcon, Kohana.
* Python: Django, Web2py, TurboGears, Webapp2, CubicWeb, Grok, Giotto.
* JavaScript: Dojo, EachJS, Echo3, Ember.js, Kendo UI, Pyjamas, Qooxdoo

### ¿Cómo analizar el nivel de carga de cada uno de los subsistemas en el servidor?
Usando herramientas que monitorice cada servicio por separado, como por ejemplo:
* Munin
* inciga
* Cacti

* Pingdom Tools
* GTmetrix
* WebPagesTest
* Google Page Speed
* YSlow

### Buscar ejemplos de Balanceadores software y hardware (productos comerciales)
###### Balanceadores de carga Software
* Enterprice VA MAX:
* nginx
* Pound
* Pen

* HAproxy
* Zen Load Balancer
* Octopues Load Balancer



###### Balanceadores de carga Hardware
* Barracuda
* Kemp Technologies

* Barracudo Load Balancer ADC
* Coyote Point Equalizer Appliances
* Cisco
* Radware AppDirector OnDemand Switch Series
* Serie BIG-IP de f5
* LoadMaster

### Buscar productos comerciales para servidores de aplicaciones
* Oracle Application Server
* Apache Tomcat
* Windows Server
* Microsoft Azure

* Servidores de aplicaciones Microsoft
* JBoss
* JOnAS
* Oracle WebLogic Server
* WebSphere Application Server
* GlassFish Server


### Buscar productos comerciales para servidores de almacenamiento
* Microsoft Azure
* mLab
* Compose


* Servidor de almacenamiento DELL
* Dell Compellent FS8600
* HP ConvergedSystem 200-HC StoreVirtual Sytem
* IBM EXP2500 Storage Enclosure
