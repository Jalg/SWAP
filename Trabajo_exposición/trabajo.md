# Comparación entre servidores web en Android.

## José Antonio Larrubia García
## Javier Quero Ruíz

Hemos instalado tres servidores web en un móvil con sistema operativo Android para comparar su comportamiento, todos ellos
disponibles en google play.
Los tres servidores han sido: Palapa Web Server, kWS y KSWEB. Todos tienen cuatro estrellas en google play, 
posteriormente nosotros daremos nuestro punto de vista. 
Los dos primeros son gratuitos y el tercero es de pago aunque dan 5 días de prueba. 

###1. Palapa Web Server.

Como hemos dicho anteriormente lo hemos buscado e instalado de google play. Una vez instalado nos aparecerá la siguiente pantalla.

![im1] (/trabajo/capturas/im1.png)

Pulsamos el símbolo de exclamación para terminar la instalación, ya que el otro botón redirige a la página web del autor[1].
Una vez pulsado el botón se bajará algunos paquetes necesarios para su funcionamiento y al acabar tendremos lo que sigue.

![im2] (/trabajo/capturas/im2.png)

La vista principal con toda la información del servidor. Hasta el momento todo deshabilitado ya que no está iniciado el servicio.
Así pues, pulsamos en *start all services* para inicial el servicio.

![im3] (/trabajo/capturas/im3.png)

Con la ayuda de la web del autor sabemos que las páginas webs hay que ponerlas dentro del directorio */sdcard/pws/www/*.

Sabiendo esto introducimos un fichero html llamado prueba y accedemos desde un navegador desde el pc para ver que realmente funciona.
Hemos usado como archivo html de prueba el mismo que en la práctica 4.
Podemos ver la estructura de ficheros poniendo *http://192.168.1.145:8080* en el navegador, que es la ip del móvil y el puerto.

![im4] (/trabajo/capturas/im4.png)

Una vez comprobado que nuestra página web de prueba está lista para ser servida probamos a acceder a ella 
poniendo *http://192.168.1.145:8080/prueba.html* en el navegador. 

![im5] (/trabajo/capturas/im5.png)

Aquí podemos ver como nos la muestra por lo que ya sabemos que es funcional no ha hecho falta añadir ninguna configuración extra, 
todo se ha realizado con la configuración que traía de fábrica. 	

Añadir que Palapa incluye lighttpd, php, mysql, msmtp y web admin. Es un servidor bastante completo para ser instalado en un dispositivo android.
Para poder acceder a la interfaz web admin del servidor se necesita un usuario y una contraseña que es admin para ambos campos.

![im6] (/trabajo/capturas/im6.png)

A continuación mostramos algunas capturas sobre algunas de las opciones de web admin.
Por ejemplo proporciona información del dispositivo, como que CPU tiene, la memoria o información sobre la batería.

![im7] (/trabajo/capturas/im7.png)

También información sobre el estado de la conexión.

![im8] (/trabajo/capturas/im8.png)

O información importante de nuestro servidor.

![im9] (/trabajo/capturas/im9.png) 

Como vemos tiene mucha información útil que lo hace muy completo.

Ahora vamos a proceder a ejecutar un benchmark para comprobar su rendimiento y después compararemos el gasto de cpu, batería y memoria 
que dice consumir con el que nos indica powertutor. Para comprobar el rendimiento hemos usado apache benchmark.

Dejamos una captura de la ejecución. Hemos usado la misma orden que en la practica 4 y también hemos hecho cinco ejecuciones para comparar
los datos medios y así sean más fiables.

![im10] (/trabajo/capturas/im10.png) 

Para poder mirar algo mejor el consumo hemos lanzado la ejecución  del benchmark un poco mas grande, ya que con las peticiones que lo habíamos 
hecho apenas podíamos recoger el consumo.

En la siguiente captura podemos ver el consumo según la aplicación.

![im11] (/trabajo/capturas/im11.png) 

Según powertutor.

![im12] (/trabajo/capturas/im12.png) 

Ambas coinciden en que el consumo de la aplicación produce una carga del 16,1% de la CPU. 


###2. kWS.

Volvemos a hacer la misma operación que con el anterior servidor, lo instalamos desde google play y nada más instalarlo vemos
lo siguiente. 

![im13] (/trabajo/capturas/im13.png) 

Damos a *start server* para iniciar el servidor. 

![im14] (/trabajo/capturas/im14.png)

Ya tenemos el servidor iniciado, podemos cambiar de donde lee nuestras paginas web. Una vez hecho esto  
nos vamos al navegador y ponemos la misma dirección que con el servidor anterior para ver nuestra página de prueba.
La sirve perfectamente y no hemos puesto una captura de pantalla ya que es redundante. 

Esta aplicación no nos dice el consumo que tiene por lo que solo podemos verlo con powertutor.

![im15] (/trabajo/capturas/im15.png)

Como vemos consume un 70 % de CPU, 4.3 veces superior a Palapa. 


###3. KSWEB.

KSWEB a diferencia de los dos servidores anteriores es de pago con 5 días de prueba gratuitos.
De nuevo lo buscamos e instalamos en google play como los dos servidores anteriores.
Recién instalado nos salen varios mensajes avisándonos de que una versión de prueba. Vamos a mostrar algunas capturas de sus funcionalidades o 
de la multitud de herramientas con las que puede llegar a trabajar. 

![im16] (/trabajo/capturas/im16.png)

![im17] (/trabajo/capturas/im17.png)

Como vemos en las imágenes anteriores nos avisa en la ventana principal de que la licencia cumple en solo 5
días y que si queremos podemos comprarlo. También nos muestra el servidor y los distintos tipos de 
servidores o funciones que tiene activadas en este momento o desactivadas.

En la siguiente imagen podemos ver el pequeño menú que tiene disponible para usar lighttpd.  

![im18] (/trabajo/capturas/im18.png)

Después podemos ver que como Palapa tiene bastantes utilidades. Añadir que en este caso se puede acceder a la configuración del server 
manual.

![im19] (/trabajo/capturas/im19.png)

Probamos que funciona accediendo a la raíz del server.

![im20] (/trabajo/capturas/im20.png)

Una vez visto esto probamos que funciona sirviendo el html de prueba. No hemos añadido la captura de nuevo porque de nuevo es lo mismo que 
anteriormente.

Por último, el consumo en powertutor es inferior al que dice la aplicación (una media de 17% frente a una media de 40%).
Tiene un consumo parecido a Palapa y por lo tanto mucho mejor que kWS.

![im21] (/trabajo/capturas/im21.png)

###4. COMPARATIVA DE BENCHMARKS Y DE CONSUMO.

A continuación pondremos las tablas de pruebas realizadas con el benchmarks.

|Palapa     | Time taken per tests (s) | Failed requests | Requests per second |
|:---------:|:------------------------:|:---------------:|:-------------------:|
|1          |8.845                    |0                 |113.05               | 
|2          |8.147                    |0                 |122.74               |
|3          |8.655                    |0                 |115.54               |
|4          |8.571                    |0                 |116.67               |
|5          |8.197                    |0                 |122	               |
|**Media**  |**8.483**                |**0**             |**188** 	           |

|kWS        | Time taken per tests (s) | Failed requests | Requests per second |
|:---------:|:------------------------:|:---------------:|:-------------------:|
|1          |20.309                    |0                |49.24                | 
|2          |20.391                    |0                |49.04                |
|3          |19.803                    |0                |50.5                 |
|4          |21.251                    |0                |47.06                |
|5          |23.193                    |0                |43.12	               |
|**Media**  |**20.9894**               |**0**            |**47.792**           |

|KSWEB      | Time taken per tests (s) | Failed requests | Requests per second |
|:---------:|:------------------------:|:---------------:|:-------------------:|
|1          |7.628                     |0                |131.1                | 
|2          |7.779                     |0                |128.56               |
|3          |8.989                     |0                |111.24               |
|4          |9.3                       |0                |107.52               |
|5          |8.286                     |0                |120.73               |
|**Media**  |**8.3958**                |**0**            |**119.83**           |

Las gráficas de las comparativas con la media son:

![im22] (/trabajo/capturas/im22.png)

![im23] (/trabajo/capturas/im23.png)

Por último mencionar a servidores que o no funcionaban para la versión de android probada (kit kat)
o que daban tan poca información que no se podían usar.

SimpleHttpServer -> tan simple que no sabías donde meter los ficheros para leerlos y nada de información extra.
HSP -> No tenía mala pinta en un principio pero no funcionaba.

###5. Conclusiones.

Actualmente buscando web server en play store salen muchas opciones, nosotros hemos probado tres. La primera, Palapa Web Server, es una opción muy completa 
y totalmente gratuita, la segunda, kWS, mucho más simple, sin una gran interfaz pero también gratuita y la tercera, KSWEB, también una opción muy completa 
aunque de pago.

Si comparamos las tres en función de consumo de CPU y de las pruebas realizadas con apache benchmark nos quedamos con Palapa Web Server, ya que es gratuita y
muestra rendimientos muy similares a KSWEB, igualándolo o incluso superándolo en todos los aspectos en los que los hemos comparado aunque solo haya sido por
muy poca diferencia. Además es una herramienta muy visual y fácil de usar.

###6. Referencias.

[1] http://alfanla.com/palapa-web-server/