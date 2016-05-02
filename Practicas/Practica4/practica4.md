# Práctica 4. Comprobar el rendimiento de servidores web.

## José Antonio Larrubia García
## Javier Quero Ruíz

###1. Apache Benchmark.

Lo primero que hay que hacer es crear la página web en formato html para que las pruebas que se hagan
tengan suficiente carga para que los resultados sean representativos.
En nuestro caso hemos usado directamente el ejemplo que viene en el guión en */var/www* tanto en la 
máquina 1 como en la máquina 2. Uno de los errores que cometimos inicialmente fue olvidarnos de poner 
el html en la máquina 2 y por tanto la cantidad de fallos al acceder era enorme. Nos dimos cuenta en el 
apartado de siege.
En la siguiente imagen vemos el ejemplo usado: 

![im1] (/Practicas/Practica4/Imagenes/im1.png)

Ahora vamos a mostrar una tabla con las medidas desde la máquina 4 a la 1, es decir directamente al servidor
sin pasar por el balanceador, para ello lanzamos *Lanzamos ab -n 1000 -c 5 http://192.168.1.101/prueba.html*.

|M1         | Time taken per tests (s) | Failed requests | Requests per second |
|:---------:|:------------------------:|:---------------:|:-------------------:|
|1          |0,374                     |0                |2670	               | 
|2          |0,362                     |0                |2761	               |
|3          |0,367                     |0                |2722	               |
|4          |0,359                     |0                |2782	               |
|5          |0,371                     |0                |2694	               |
|**Media**  |**0,3666**                |**0**            |**2725,8**           |

En la siguiente imagen vemos un ejemplo de ejecución de la orden ab.

![im2] (/Practicas/Practica4/Imagenes/im2.png)

Las siguientes medidas son desde la máquina 4 a la granja web usando nginx como balanceador. Por tanto en este caso la
orden a usar será la misma pero usando la ip de nuestro balanceador *ab -n 1000 -c 5 http://192.168.1.105/prueba.html*.

|Nginx      | Time taken per tests (s) | Failed requests | Requests per second |
|:---------:|:------------------------:|:---------------:|:-------------------:|
|1          |0,694                     |0                |1441	               |
|2          |0,759                     |0                |1318	               |
|3          |0,679                     |0                |1472	               |
|4          |0,679                     |0                |1472	               |
|5          |0,677                     |0                |1476	               |
|**Media**  |**0,6976**                |**0**            |**1435,8**           |

Sin hacer una gráfica podemos ver ya directamente que si se hicieran peticiones directamente al servidor en lugar de a la 
granja web pasando por el balanceador el servicio es más rápido, algo previsible. 

En la siguiente imagen se puede ver la primera ejecución de ab.

![im3] (/Practicas/Practica4/Imagenes/im3.png)

Las siguientes medidas son al igual que las anteriores desde la máquina 4 hacia la granja web en este caso usando haproxy
como balanceador. La orden ab sigue siendo la misma que antes.

|Haproxy    | Time taken per tests (s) | Failed requests | Requests per second |
|:---------:|:------------------------:|:---------------:|:-------------------:|
|1          |0,541                     |0                |1847	               |
|2          |0,541                     |0                |1847	               |
|3          |0,539                     |0                |1855	               |
|4          |0,549                     |0                |1820	               |
|5          |0,528                     |0                |1892	               |
|**Media**  |**0,5396**                |**0**            |**1852,2**           |

De nuevo sólo con los datos de la tabla podemos ver como haproxy hace un mejor servicio que nginx de balanceador, nada raro
considerando que nginx en un principio es software para servidor web y no como haproxy que si es un balanceador directamente.
Aún así sigue siendo más rápido accediendo al servidor directamente.

Para este caso no hemos hecho captura ya que la salida es similar en todos los casos de ab.

Por último las medidas con pound como balanceador desde la máquina 4.

|Pound      | Time taken per tests (s) | Failed requests | Requests per second |
|:---------:|:------------------------:|:---------------:|:-------------------:|
|1          |1,051                     |0                |951	               |
|2          |1,034                     |0                |967	               |
|3          |1,046                     |0                |956	               |
|4          |1,043                     |0                |958	               |
|5          |1,033                     |0                |968	               |
|**Media**  |**1,0414**                |**0**            |**960**              |

Podemos decir que pound es de los 3 balanceadores usados en la práctica el más lento aún cuando es directamente un balanceador como
lo es haproxy.

La siguiente imagen se ven las gráficas donde se venn comparadas las medias de time taken per tests y request per second de las tres
tablas anteriores.

![gra1] (/Practicas/Practica4/Imagenes/gra1.png)

En esta primera gráfica no hemos mostrado gailed request por ser siempre 0 en todas las mediciones.

###2. Siege.

Lo primero es instalar siege con la orden *apt-get install siege*.
Una vez instalado repetiremos las medidas que se han realizado con ab.

Las primeras como antes serán desde la máquina 4 hacia la máquina 1 directamente, la orden usada de siege es 
*siege -b -t60s -v http://192.168.1.101/prueba.html*, en la siguiente imagen se ve una primera ejecución de siege.

![im4] (/Practicas/Practica4/Imagenes/im4.png)

Y ahora la tabla con las mediciones.

|M1         | Availability(%) | Reponse time (s) | Failed transactions | Longest transaction |
|:---------:|:---------------:|:----------------:|:-------------------:|:-------------------:|
|1          |100              |0,01              |0	                   |0,15                 |
|2          |100              |0,01              |0	                   |0,1                  |
|3          |100              |0,01              |0	                   |0,17                 |
|4          |100              |0,01              |0	                   |0,06                 |
|5          |100              |0,01              |0	                   |0,16                 |
|**Media**  |**100**          |**0,01**          |**0**                |**0,128**            |

Las siguientes mediciones son desde la máquina 4 hacia la granja web con nginx como balanceador, la orden de siege
por tanto queda de la siguiente forma *siege -b -t60s -v http://192.168.1.105/prueba.html*.

|Nginx      | Availability(%) | Reponse time (s) | Failed transactions | Longest transaction |
|:---------:|:---------------:|:----------------:|:-------------------:|:-------------------:|
|1          |100              |0,01              |0	                   |0,06                 |
|2          |100              |0,01              |0	                   |0,05                 |
|3          |100              |0,01              |0	                   |0,07                 |
|4          |100              |0,01              |0	                   |0,06                 |
|5          |100              |0,01              |0	                   |0,05                 |
|**Media**  |**100**          |**0,01**          |**0**                |**0,058**            |

En este caso la única diferencia es en la transacción mas larga.

Las siguientes son con haproxy como balanceador.

|Haproxy    | Availability(%) | Reponse time (s) | Failed transactions | Longest transaction |
|:---------:|:---------------:|:----------------:|:-------------------:|:-------------------:|
|1          |100              |0,01              |0	                   |0,05                 |
|2          |100              |0,01              |0	                   |0,06                 |
|3          |100              |0,01              |0	                   |0,05                 |
|4          |100              |0,01              |0	                   |0,06                 |
|5          |100              |0,01              |0	                   |0,06                 |
|**Media**  |**100**          |**0,01**          |**0**                |**0,056**            |

Y por último las medidas usando pound.

|Pound      | Availability(%) | Reponse time (s) | Failed transactions | Longest transaction |
|:---------:|:---------------:|:----------------:|:-------------------:|:-------------------:|
|1          |100              |0,01              |0	                   |0,1                  |
|2          |100              |0,01              |0	                   |0,11                 |
|3          |100              |0,01              |0	                   |0,15                 |
|4          |100              |0,01              |0	                   |0,15                 |
|5          |100              |0,01              |0	                   |0,16                 |
|**Media**  |**100**          |**0,01**          |**0**                |**0,134**            |

Y la gráfica correspondiente a las diferencias entre las medias de las transacciones más largas de todos los casos,
no hacemos otras gráficas ya que todas las otras medidas son idénticas.

![gra2] (/Practicas/Practica4/Imagenes/gra2.png)

###3. Httperf.

Lo primero es instalarlo, podemos de nuevo hacerlo usando el repertorio de paquetes , en este caso la orden sería*apt-get
*apt-get install httperf*.

Para las primeras mediciones de httperf lo haremos desde la máquina 4 a la máquina 1 directamente, se usa la orden 
*httperf --hog --server 192.168.1.101 http://192.168.1.101/prueba.html --port80 --num-conns 1000* donde se especifica el 
server al que le haces la petición y donde esta el archivo el puerto donde debe mirar y el número de peticiones, en nuestro
caso hemos puesto 1000 ya que era lo que se usaba en apache benchmark.
Para saber más de las opciones de httperf se pueden ver en *man httperf*.

La siguiente imagen muestra un ejemplo de ejecución.
![im5] (/Practicas/Practica4/Imagenes/im5.png)

A continuación en la tabla mostramos 5 medidas.

|M1         | Connection rate(conns/s)| Avg connection time(ms) | Reply time (ms) |
|:---------:|:-----------------------:|:-----------------------:|:---------------:|
|1          |715,8                    |1,4                      |0,7              |
|2          |647,5                    |1,5                      |0,8              |
|3          |739                      |1,4                      |0,7              |
|4          |648,9                    |1,5                      |0,8              |
|5          |666,1                    |1,5                      |0,8              |
|**Media**  |**683,46**               |**1,46**                 |**0,76**         |

Ahora lo ejecutaremos desde la máquina 4 a la granja web con nginx como balanceador, la orden de httperf en este caso sería la siguiente
*httperf --hog --server 192.168.1.105 http://192.168.1.105/prueba.html --port80 --num-conns 1000*

|Nginx      | Connection rate(conns/s)| Avg connection time(ms) | Reply time (ms) |
|:---------:|:-----------------------:|:-----------------------:|:---------------:|
|1          |485,5                    |2,1                      |1,4              |
|2          |502,2                    |2                        |1,3              |
|3          |494,4                    |2                        |1,4              |
|4          |507,2                    |2                        |1,3              |
|5          |483,1                    |2,1                      |1,4              |
|**Media**  |**494,48**               |**2,04**                 |**1,36**         |
		
Las siguientes medidas serán con haproxy como balanceador.

|Haproxy      | Connection rate(conns/s)| Avg connection time(ms) | Reply time (ms) |
|:---------:|:-----------------------:|:-----------------------:|:---------------:|
|1          |546,2                    |1,8                      |1,1              |
|2          |553                      |1,8                      |1,1              |
|3          |556,1                    |1,8                      |1,1              |
|4          |570,8                    |1,8                      |1,1              |
|5          |550,5                    |1,8                      |1,1              |
|**Media**  |**555,32**               |**1,8**                  |**1,1**          |

Y por último las medidas con pound como balanceador.

|Pound      | Connection rate(conns/s)| Avg connection time(ms) | Reply time (ms) |
|:---------:|:-----------------------:|:-----------------------:|:---------------:|
|1          |428,5                    |2,3                      |1,6              |
|2          |448                      |2,2                      |1,5              |
|3          |467,2                    |2,1                      |1,4              |
|4          |443                      |2,3                      |1,5              |
|5          |446                      |2,2                      |1,4              |
|**Media**  |**446,54**               |**2,22**                 |**1,48**          |

En la siguiente imagen podemos ver las 3 gráficas comparando las medias de cada una de las tablas.

![gra3] (/Practicas/Practica4/Imagenes/gra3.png)

Podemos por tanto decir que cada benchmark evalúa de forma distinta al servidor web dando distintos tipos de 
rendimiento, así por tanto podremos poner a prueba a nuestro server con un benchmark donde se de información concreta
sobre algo que estemos buscando. Es decir si queremos probar la transación más larga tenemos siege o si queremos ver las peticiones
que sirve por segundo tenemos el apache o si quisieramos saber el tiempo de respuesta el httperf.

Una buena forma de evaluar el rendimiento nuestro server y en este caso elegir balanceador según lo que estemos buscando.




