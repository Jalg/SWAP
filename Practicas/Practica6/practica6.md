# Práctica 6. Discos en RAID.

## José Antonio Larrubia García
## Javier Quero Ruíz

###1. Configuración del RAID por software.
Con la máquina apagada le hemos añadimos dos discos de un 1Gb cada uno, llamados disco1 y disco2.

![im1] (/Practicas/Practica6/Imagenes/im1.png)

Después instalamos mdadm para poder configurar RAID. Lo hacemos con orden *apt-get install mdadm*.
Buscamos la información de ambos discos con fdisk -l.

![im2] (/Practicas/Practica6/Imagenes/im2.png)

Creamos el RAID1 usando el dispositivo /dev/md0, *mdadm -C /dev/md0*...

![im3] (/Practicas/Practica6/Imagenes/im3.png)

Le damos formato con *mkfs /dev/md0*.

![im4] (/Practicas/Practica6/Imagenes/im4.png)

Creamos el directorio en el que se montara RAID:
*mkdir /dat*
*mount /dev/md0 /dat*

Comprobamos el estado del RAID

![im5] (/Practicas/Practica6/Imagenes/im5.png)

Por úlitmo configuramos el sistema para que monte el RAID al arrancar el sistema. Para ello debemos editar el archivo
/etc/fstab.
Antes obtenemos el UUID del RAID, ya que lo necesitaremos.

![im6] (/Practicas/Practica6/Imagenes/im6.png)

Editamos /etc/fstab quedando como en la imagen:

![im7] (/Practicas/Practica6/Imagenes/im7.png)


###2. Simulación de error en un disco.

Simulamos el fallo.

![im8] (/Practicas/Practica6/Imagenes/im8.png)

Comprobamos que se ha producido el fallo:

![im9] (/Practicas/Practica6/Imagenes/im9.png)

En la imagen anterior podemos ver que se ha producido el fallo (faulty spare).
Ahora procedemos a retirar en caliente el disco que falla.

![im10] (/Practicas/Practica6/Imagenes/im10.png)

En la captura anterior vemos como se ha retirado el disco que fallaba.
Y por último podemos volver a añadir un nuevo disco que reemplaza al disco que hemos retirado.

![im11] (/Practicas/Practica6/Imagenes/im11.png)

###3. Configaración NFS.

Insatalamos en la máquina en la que tenemos el RAID con: apt-get install fs-kernel-server nfs-common rpcbind.
En la máquina en la que haremos las peticiones instalamos
Comprobamos que se ha instalado perfectamente con grep. 

![im12] (/Practicas/Practica6/Imagenes/im12.png)

Configuramos el NFS. 
Creamos una carpeta *mkdir /compartido*.
Cambiaremos el nombre del usuario y grupo propietarios de la carpeta, para que no sean propiedad de nadie, y los permisos de acceso, para que todos los usuarios dispongan de todos los permisos sobre ella.
*chown nobody:nogroup /compartido*.
*chmod -R 777 /compartido*.

![im13] (/Practicas/Practica6/Imagenes/im13.png)

Después de esto, debemos editar el archivo /etc/exports. Este es el archivo donde se indican a NFS las carpetas que vamos a compartir. Y reiniciamos el servicio.

![im14] (/Practicas/Practica6/Imagenes/im14.png)

En /etc/exports se pone la ruta del fichero con el cliente y las opciones, al poner * es que cualquier
cliente podrá acceder a esa carpeta compartida, entre parentesis van las opciones.

Por ejemplo:
rw, es lectura escritura.
sync, evita responder peticiones antes de escribir los cambios pendientes en disco.,
no_root_squash, deshabilita root squash que evita que los usuarios con privilegios los mantengan sobre la carpeta compartida.
no_subtree_check, deshabilita subtree_check que hace que cuando el directorio compartido es un subdirectorio mayor, nfs compruebe los directorios
por encima para verificar sus permisos y características.

Ahora nos vamos al cliente.
He instalamos apt-get install nfs-common rpcbind.

Creamos un punto de montaje para las carpetas compartidas.


*sudo mkdir -p /mnt/nfs/home*
*sudo mkdir -p /mnt/nfs/compartido*
Una última precaución que debemos tener en cuenta es que, aunque hayamos dado permisos de escritura sobre las carpetas compartidas en la configuración NFS del servidor.

![im15] (/Practicas/Practica6/Imagenes/im15.png)

Realizamos el montaje de las carpetas compartidas y con df -h probamos que se haya montado bien.
![im16] (/Practicas/Practica6/Imagenes/im16.png)

Ya tenemos configurado NFS, para probarlo creamos ficheros y carpetas dentro de la compartida y vemos que en la otra máquina también aparecen.

![im17] (/Practicas/Practica6/Imagenes/im17.png)
![im18] (/Practicas/Practica6/Imagenes/im18.png)

Para la parte de NFS nos hemos basado en el siguiente tutorial:
http://somebooks.es/?p=5598
