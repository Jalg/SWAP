#					Ejercicios Tema 2

## 				José Antonio Larrubia García.

###Ejercicio 1. Calcular la disponibilidad del sistema si tenemos dos réplicas de cada elemento (en total 3 elementos en cada subsistema). 

	  
Original			

**Web**			85%		
**Application**	90%		
**Database**	99,9%		
**DNS** 		98%		
**Firewall**	85%		
**Switch** 		99%		
**Data Center** 99,99%	
**ISP** 		95%		

**Duplicado**				

**Web**			97,75%			
**Application**	99%			
**Database**	99,9999%		
**DNS** 		99,96%		
**Firewall**	97,75%		
**Switch** 		99,99%		
**Data Center** 99,99%		
**ISP** 		99,75%		

**Triplicado**

**Web**			99,66%	
**Application**	99,9%
**Database**	99,9999999%
**DNS** 		99,9992%
**Firewall**	99,66%
**Switch** 		99,9999%
**Data Center** 99,99%
**ISP** 		99,9875%

La disponibilidad del sistema será: **99,198%**.


###Ejercicio 2. Buscar frameworks y librerías para diferentes lenguajes que permitan hacer aplicaciones altamente disponibles con relativa facilidad. 

- **Strongloop**: es el más popular framework de código abierto para Node.js.

- **Locomotive**: es otro framework para Node.js. Tiene integración sin problemas con cualquier motor de base de datos.

- **Microsoft Operations Framewotk**: framework para productos de Microsoft. 

- **Linux-HA**: proyecto que mantiene un conjunto de bloques para sistemas de cluster de alta disponibilidad para Linux.


###Ejercicio 3. ¿Cómo analizar el nivel de carga de uno de los subsistemas en el servidor? 

Hay muchas herramientas que permiten analizar el nivel de carga de los subsistemas como ya vimos en Ingeniería de Servidores.  Algunos de ellos son: 

- **Top**: esta orden nos permite conocer en tiempo real la actividad del sistema.

- **Vmstat**: que también puede dar información sobre accesos a discos y estadísticas de memoria.

- **SysStat**: es un paquete de monitorización.


En prácticas vimos algunos más como Munin, Nagios o Ganglia. 

###Ejercicio 4. Buscar ejemplos de balanceadores software y hardware (productos comerciales). Buscar productos para servidores de aplicaciones y para servidores de almacenamiento. 

Algunos ejemplos de balanceadores software y hardware son:

- **Cisco**.

- **Barracuda**.

- **Pound**.

- **Zen Load**. 

Por otra parte algunos productos para servidores de aplicación y de almacenamiento son: 

- **WebSphere** de IBM.

- **WebLogic** de Oracle.

- **JOnAs**.

- De almacenamiento podemos encontrar servidores de HP, de Western Digital o de IBM. Un ejemplo de ellos es el WD Sentinel DX4000.