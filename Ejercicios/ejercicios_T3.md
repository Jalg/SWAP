#					Ejercicios Tema 3

## 				Jos� Antonio Larrubia Garc�a.

###Ejercicio 1. Buscar con qu� �rdenes de terminal o herramientas gr�ficas podemos configurar bajo Windows y bajo Linux el enrutamiento del tr�fico de un servidor para pasar el tr�fico desde una subred a otra. 
  
Bajo Linux lo podemos configurar con la orden iptables y con el comando route. Toda la informaci�n de la configuraci�n de red 
se encuentra en */etc/network/interfaces*, otras ordenes interesantes son tracert y path ping para analizar por donde pasa el tr�fico hacia nuestro servidor.

En Windows podemos configurarlo en el panel de control > Entorno de red.


###Ejercicio T3.2. Buscar con qu� �rdenes de terminal o herramientas gr�ficas podemos configurar bajo Windows y bajo Linux el filtrado y bloqueo de paquetes.

Bajo Linux se hace a trav�s de iptables y en Windows se puede hacer escribiendo wf.msc por el terminal, que nos llevar� 
al firewall de windows con seguridad avanzada, donde podremos cambiar los valore que deseemos. 
