#					Ejercicios Tema 5

## 				Jos� Antonio Larrubia Garc�a.


###Ejercicio 1. Buscar informaci�n sobre c�mo calcular el n�mero de conexiones por segundo.

Podemos realizarlo con benchmarks como son apache benchmark o siege. 
Realizan una serie de peticiones para comprobar el rendimiento del balanceador y a la vez nos dan informaci�n sobre �l, entre
otras nos pueden indicar el n�mero de conexiones por segundo, el n�mero de fallos, etc.

###Ejercicio 3. Buscar informaci�n sobre caracter�sticas, disponibilidad para diversos SO, etc de herramientas para monitorizar las prestaciones de un servidor.

Para Windows Server 2008 podemos usar la herramienta Monitor de Confiabilidad y Rendimiento que trae el propio sistema 
operativo. Podemos monitorizar las bases de datos, cach�, colas de solicitud de servicio HTTP, la interfaz de red, etc.

Para Ubuntu. Top, vmstat o sar son los m�s conocidos. 
Su principal uso es monitorizar la actividad del procesador en tiempo real, tanto la orden top como la orden vmstat tienen 
una interfaz facil de usar y c�moda para obtener la informaci�n.

Hay otras herramientas m�s vistosas como Monitorix. Da informaci�n sobre el tr�fico de red, estad�sticas de email, tr�fico de servidor web, de carga MySQL, de uso de proxy, etc. 