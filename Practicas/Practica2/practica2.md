# Pr�ctica 2. Clonar la informaci�n de un sitio web.

## Jos� Antonio Larrubia Garc�a
## Javier Quero Ru�z


** 1. Probando ssh **
Lo primero que hemos hecho es probar el funcionamiento de copia de archivos mediante ssh, como podemos ver en la siguiente imagen:

![imagen] (/Practicas/Practica2/Im�genes/im1)

** 2. Rsync **
Una vez comprobado que tenemos conexi�n y nos funciona ssh perfectamente creamos una carpeta ejemplo
en la m�quina principal y ejecutamos el comando:
* rsync -avz --delete -e ssh root@"ip_servidor_2":/var/www/ /var/www/ *

Donde la opci�n de --delete es para que sincronice tambi�n los ficheros que han sido borrados, 
si no la ponemos los borrados se mantienen en la m�quina que queremos sincronizar a la principal.

Comprobamos que se muestra en la segunda m�quina el fichero creado como prueba para ver que funciona el comando.
Despu�s borramos y de nuevo ejecutamos rsync para probar que la opci�n --delete funciona
Comprobamos que se ha borrado correctamente en el clonado de la segunda m�quina. En la siguiente captura podemos ver ambas ejecuciones de rsync.	

![imagen2] (/Practicas/Practica2/Im�genes/im2)

A�adir que si no nos deja por ssh acceder como root tendremos que darle permisos de la siguiente forma, editar el fichero que se encuentra en 
* /etc/ssh/sshd_config * 
Por ejemplo con el editor vim y buscar la l�nea que pone PermitRootLogin y poner yes una vez hecho es s�lo reiniciar el servicio con
* service ssh restart *  

** 3.  Acceso sin contrase�a por ssh. **
Hacemos lo siguiente:
 
*	ssh-keygen -t dsa *
	enter
	enter
	enter
*	ssh-copy-id -i ./ssh/id_dsa.pub root@192.168.1.101 *

Y probamos si no nos pide la contrase�a.
ssh "ip_servidor" -l root 

Ya no nos pide la contrase�a como podemos ver en la siguiente captura:
		
![imagen3] (/Practicas/Practica2/Im�genes/im3)

** 4. Establecer una tarea **

En este apartado queremos establecer una tarea que se ejecute cada hora para mantener nuestro servidor clonado
actualizado, para que si la m�quina principal se pierde s�lo se pierda como m�ximo el contenido de hace una hora.
En nuestro caso s�lo vamos a mantener actualizado el contenido de nuestro directorio 
* /var/www *

Para esto vamos a usar cron, lo �nico que tenemos que hacer editar el archivo encontrado en * /etc/crontrab *
para establecer tareas en nuestro servidor, en nuestro caso lo que queremos es que se lance cada hora, por tanto 
a�adimos la siguiente l�nea:

* 0 * * * * root rsync -avz --delete -e ssh root@192.168.1.101:/var/www/ /var/www/ *

Quedar�a el archivo en nuestro caso de la siguiente forma:

![imagen4] (/Practicas/Practica2/Im�genes/im4)