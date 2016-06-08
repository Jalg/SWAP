#					Ejercicios Tema 3

## 				José Antonio Larrubia García.

###Ejercicio 1. Buscar con qué órdenes de terminal o herramientas gráficas podemos configurar bajo Windows y bajo Linux el enrutamiento del tráfico de un servidor para pasar el tráfico desde una subred a otra. 
  
Bajo Linux lo podemos configurar con la orden iptables y con el comando route. Toda la información de la configuración de red 
se encuentra en */etc/network/interfaces*, otras ordenes interesantes son tracert y path ping para analizar por donde pasa el tráfico hacia nuestro servidor.

En Windows podemos configurarlo en el panel de control > Entorno de red.


###Ejercicio T3.2. Buscar con qué órdenes de terminal o herramientas gráficas podemos configurar bajo Windows y bajo Linux el filtrado y bloqueo de paquetes.

Bajo Linux se hace a través de iptables y en Windows se puede hacer escribiendo wf.msc por el terminal, que nos llevará 
al firewall de windows con seguridad avanzada, donde podremos cambiar los valore que deseemos. 
