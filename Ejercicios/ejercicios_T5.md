#					Ejercicios Tema 5

## 				José Antonio Larrubia García.


###Ejercicio 1. Buscar información sobre cómo calcular el número de conexiones por segundo.

Podemos realizarlo con benchmarks como son apache benchmark o siege. 
Realizan una serie de peticiones para comprobar el rendimiento del balanceador y a la vez nos dan información sobre él, entre
otras nos pueden indicar el número de conexiones por segundo, el número de fallos, etc.

###Ejercicio 3. Buscar información sobre características, disponibilidad para diversos SO, etc de herramientas para monitorizar las prestaciones de un servidor.

Para Windows Server 2008 podemos usar la herramienta Monitor de Confiabilidad y Rendimiento que trae el propio sistema 
operativo. Podemos monitorizar las bases de datos, caché, colas de solicitud de servicio HTTP, la interfaz de red, etc.

Para Ubuntu. Top, vmstat o sar son los más conocidos. 
Su principal uso es monitorizar la actividad del procesador en tiempo real, tanto la orden top como la orden vmstat tienen 
una interfaz facil de usar y cómoda para obtener la información.

Hay otras herramientas más vistosas como Monitorix. Da información sobre el tráfico de red, estadísticas de email, tráfico de servidor web, de carga MySQL, de uso de proxy, etc. 