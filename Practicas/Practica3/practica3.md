# Práctica 3. Balanceo de Carga.

## José Antonio Larrubia García
## Javier Quero Ruíz

### 1. Nginx.

Lo primero que tenemos que hacer es instalar nginx, en nuestro caso con  *sudo apt-get install nginx* fue suficiente.

Una vez instalado procedemos a realizar la configuración del mismo para que actúe como balanceador de carga.
Como la configuración inicial no nos sirve, ya que parte de un servidor web, tenemos que modificar el fichero
*/etc/nginx/conf.d/default.conf* en nuestro caso el fichero no estaba pero al crearlo no hubo problemas en una
máquina con ubuntu server 12, en ubuntu server 14 no pudimos modificarlo como balanceador. No nos daba error al 
reiniciar el servicio pero no nos balanceaba sólo mostraba el index de nginx. Encontramos que era en sites-availables
haciendo un enlace simbólico hacia sites-enable pero al hacer esto daba error al reiniciar el servicio y no 
estaba disponible el puerto 80, por tanto reinstalamos en una máquina con ubuntu server 12 y no hubo problemas.

En la siguiente imagen se puede ver como configuramos nuestro balanceador nginx:

![im1] (/Practicas/Practica3/Imagenes/im1.png)

Esta configuración está hecha antes de añadir el reparto de carga en el que la máquina 1 maneja el doble de carga que la 
dos.

Una vez configurado y reiniciado el servicio nginx cambiamos los index de la máquina 1 y 2 para que digan quien es cadda uno,
para saber facilmente cual de las dos es la que está sirviendo y así saber si funciona correctamente.

Para probarlo hacemos un curl y vemos que nos da el index de cada página por tanto funciona correctamente.
En la siguiente imagen se puede ver un ejemplo de ejecución.

![im2] (/Practicas/Practica3/Imagenes/im2.png)

A continuación ya si asignamos la carga de trabajo que manejará cada una de las máquinas, donde suponemos que la máquina 1
es el doble de potente, o tiene el doble de capacidad que la máquina 2(aunque en nuestro caso sean iguales).
En la siguiente imagen se ve como acabaría la configuración de nuevo del archivo */etc/nginx/conf.d/default.conf*

![im3] (/Practicas/Practica3/Imagenes/im3.png)

Procedemos a probar que realmente asigna el trabajo como debe, es decir la máquina 1 sirve el doble de peticiones que la 
la máquina 2. Para comprobarlo desde otra máquina a parte que sería la máquina 4 llamará a la máquina que actúa de balanceador
con un curl como el siguiente *curl http://<ip del balanceador>* en nuestro caso quedaría de la siguiente forma:
*curl http://192.168.1.105*. 

En la siguiente imagen observamos de cada 3 peticiones que llegan la máquina dos atiende solamente a una de ellas y la uno a dos.

![im4] (/Practicas/Practica3/Imagenes/im4.png)

Ya hemos realizado lo pedido con nginx, ahora lo haremos con haproxy.

### 2. Haproxy.

Lo primero que tenemos que hacer es matar nginx con la orden: *service nginx stop* en modo superusuario(root).

Una vez detenido el servicio de nginx procedemos a instalar haproxy, el orden de esto da igual lo importante es
que cuando queramos usar haproxy nginx esté parado y haproxy iniciando, si no habrá un conflicto a la hora de 
escuchar por el puerto 80. Para instalar haproxy usamos apt-get también.

Una vez isntalado debemos modificar su archivo de configuración en este caso lo podemos encontrar en */etc/haproxy/haproxy.cfg*.
En este caso ya hemos añadido que asigne la carga adecuadamente desde el principio.

En la siguiente imagen podemos ver como quedaría el fichero de configuración.

![im5] (/Practicas/Practica3/Imagenes/im5.png)

Una vez tenemos el fichero de configuración modificado tenemos que lanzar haproxy, par ello usamos la siguiente orden:
*/usr/sbin/haproxy -f /etc/haproxy/haproxy.cfg*. Y desde la máquina 4 llamamos de nuevo al balanceador de la misma forma que hicimos
con nginx para comprobar que lo hace correctamente. En la siguiente imagen puede verse un ejemplo de como funciona.

![im6] (/Practicas/Practica3/Imagenes/im6.png)

Como se puede ver funciona correctamente.
