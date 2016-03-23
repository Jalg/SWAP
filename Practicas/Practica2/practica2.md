# Práctica 2. Clonar la información de un sitio web.

## José Antonio Larrubia García
## Javier Quero Ruíz


**1. Probando ssh**

Lo primero que hemos hecho es probar el funcionamiento de copia de archivos mediante ssh, como podemos ver en la siguiente imagen:

![im1] (/Practicas/Practica2/Imágenes/im1.png)

**2. Rsync**

Una vez comprobado que tenemos conexión y nos funciona ssh perfectamente creamos una carpeta ejemplo
en la máquina principal y ejecutamos el comando:
*rsync -avz --delete -e ssh root@"ip_servidor_2":/var/www/ /var/www/*

Donde la opción de --delete es para que sincronice también los ficheros que han sido borrados, 
si no la ponemos los borrados se mantienen en la máquina que queremos sincronizar a la principal.

Comprobamos que se muestra en la segunda máquina el fichero creado como prueba para ver que funciona el comando.
Después borramos y de nuevo ejecutamos rsync para probar que la opción --delete funciona
Comprobamos que se ha borrado correctamente en el clonado de la segunda máquina. En la siguiente captura podemos ver ambas ejecuciones de rsync.	

![im2] (/Practicas/Practica2/Imágenes/im2.png)

Añadir que si no nos deja por ssh acceder como root tendremos que darle permisos de la siguiente forma, editar el fichero que se encuentra en 
*/etc/ssh/sshd_config* 
Por ejemplo con el editor vim y buscar la línea que pone PermitRootLogin y poner yes una vez hecho es sólo reiniciar el servicio con
*service ssh restart*  

**3.  Acceso sin contraseña por ssh.**

Hacemos lo siguiente:
 
*ssh-keygen -t dsa*
enter
enter
enter
*ssh-copy-id -i ./ssh/id_dsa.pub root@"ip_server"*

Y probamos si no nos pide la contraseña.
*ssh "ip_servidor" -l root* 

Ya no nos pide la contraseña como podemos ver en la siguiente captura:
		
![im3] (/Practicas/Practica2/Imágenes/im3.png)

**4. Establecer una tarea**

En este apartado queremos establecer una tarea que se ejecute cada hora para mantener nuestro servidor clonado
actualizado, para que si la máquina principal se pierde sólo se pierda como máximo el contenido de hace una hora.
En nuestro caso sólo vamos a mantener actualizado el contenido de nuestro directorio 
*/var/www*

Para esto vamos a usar cron, lo único que tenemos que hacer editar el archivo encontrado en * /etc/crontrab *
para establecer tareas en nuestro servidor, en nuestro caso lo que queremos es que se lance cada hora, por tanto 
añadimos la siguiente línea:

*0 * * * * root rsync -avz --delete -e ssh root@"ip_server":/var/www/ /var/www/*

Quedaría el archivo en nuestro caso de la siguiente forma:

![im4] (/Practicas/Practica2/Imágenes/im4.png)
