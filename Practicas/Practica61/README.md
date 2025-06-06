## Práctica 61

## Ejercicio 1: Determinar la parte de la dirección IP que corresponde al host y a la red
Tarea: Conociendo las siguientes direcciones de host IP, indique la clase de cada dirección,
el ID o la dirección de red, la parte que corresponde al host, la dirección de broadcast para
esta red y la máscara de subred por defecto.

Explicación: En el caso del ID de red, la parte que corresponde al host está formada sólo
por ceros. Escriba sólo los octetos que componen el host. En el caso de un broadcast, la
parte que corresponde al host está formada por todos unos. En el caso de una máscara de
subred, la parte de la dirección que corresponde a la red está formada por todos unos.

a) Complete la siguiente tabla:

| Direccion ip del host| Clase      | Direccion de red |Direccion de host | Broadcast     | Máscara por defecto |
|----------------------|:----------:|------------------|------------------|---------------|---------------------|
|__216.14.55.137__     |C           |216.154.44.0      |137               |216.154.44.255 |255.255.255.0        |
|__123.1.1.15__        |A           |123.0.0.0         |1.1.15            |123.255.255.255|255.0.0.0            |
|__150.127.221.244__   |B           |150.127.0.0       |221.144           |150.127.255.255|255.255.0.0          |
|__194.125.35.199__    |C           |194.125.35.0      |199               |194.125.35.255 |255.255.255.0        |
|__175.12.239.244__    |B           |175.12.0.0        |239.244           |175.12.255.255 |255.255.0.0          |

b) Dada una dirección IP 142.226.0.15
 - ¿Cuál es el equivalente binario del segundo octeto? 11100010
 - ¿Cuál es la Clase de la dirección? Clase B
 - ¿Cuál es la dirección de red de esta dirección IP? 142.226.0.0
 - ¿Es ésta una dirección de host válida (S/N) Sí. 
 - ¿Por qué? No es ni BC ni Red, ni ninguna ip reservada para uso especial

c) ¿Cuál es la cantidad máxima de hosts que se pueden tener con una dirección de red clase C?  
Tiene máscara 255.255.255.0 (/24), así que nos deja 8 bits para direcciones, de las cuales restamos la de BC y la de Red. __Por tanto, 2<sup>8</sup> -2 hosts.__

d) ¿Cuántas redes de clase B puede haber?  
Empiezan por 10 y usan en total 2 octetos (16 bits) para la red. Así que son  2<sup>14</sup> redes (si contamos la red con todo a 1 y la red con todo a 0s). 

e) ¿Cuántos hosts puede tener cada red de clase B?  
Usa máscara /16, así que nos quefan 16 bits para hosts. Por tanto: 2<sup>16</sup> - 2. 

f) ¿Cuántos octetos hay en una dirección IP? ¿Cuántos bits puede haber por octeto?  
En una Ipv4 hay 4 octetos. En cada octeto hay 8 bits. 


## Ejercicio 3
Se desean crear 6 subredes para conectar 64 máquinas a cada una de ellas a partir de la dirección IP de red 220.130.145.0 y máscara 255.255.255.0. ¿Qué direcciones de subred, si existen, se emplean para encaminar correctamente datagramas IP a dichas máquinas?

__Solución:__
Para 6 subredes necesitamos 3 bits (2<sup>3</sup> es 8). Por tanto, _"robamos"_ 3 bits a la parte de hosts.
Siempre se roban los n bits más significativos necesarios (MSB).   
Es una clase red clase C, así que la máscara por defecto sería 255.255.255.0.  
La nueva máscara, que coge esos 3 bits adicionales, sería:  
255.255.255.11100000 ---> 255.255.255.224  
Esto nos deja 5 bits para direcciones de host, por lo que no podríamos direccionar los 64 bits que indica el enunciado. __No es posible generar todas las redes que se piden con ese requisito.__ Podríamos tener máximo 2<sup>5</sup> - 2 hosts por red, es decir, 30.   
Si se admitiera esa relajación de requisitos:

Siendo sunetting clásico, entendemos que la red con todo a 1s y todo a 0s no se pueden usar, así que las redes que nos quedan son:  
(dejo un espacio tras los bits de red)
 - 220.130.145.001 00000 --> 220.130.145.32
 - 220.130.145.010 00000 --> 220.130.145.64
 - 220.130.145.011 00000 --> 220.130.145.96
 - 220.130.145.100 00000 --> 220.130.145.128

## Ejercicio 4 
Se desea crear 254 subredes para conectar 254 máquinas a cada una de ellas a partir
de la dirección IP de red 135.100.0.0 y máscara 255.255.0.0. ¿Qué máscara de
subred se emplea para encaminar correctamente datagramas IP a dichas máquinas?

__Solución__
Para 254 subredes neceesitamos 8 bits (2<sup>8</sup> = 256).  
La ip 135.x es una clase B, que por tanto tiene máscara 255.255.0.0.   
Eso nos deja 16 bits de hosts, de los cuales "robamos" 8, quedando 8 bits de host restantes, que permiten direccionar exactamente 254 hosts. Así que se puede hacer. 

La máscara de las subredes sería  
255.255.255.0

### Ejercicio 6
Una organización “A” desea conectar a Internet como máximo 2032 máquinas. A su
vez, otra organización “B” quiere conectar, también a Internet, como máximo 4064
máquinas. Con el objetivo de que dichas organizaciones hagan un uso lo más óptimo
posible del espacio de direccionamiento, el proveedor de “A” le asigna un formato
de encaminamiento entre dominios sin clase (CIDR) a partir de la dirección
205.10.0.0. Asimismo, el proveedor de “B” asigna a esta última organización, un
formato de encaminamiento entre dominios sin clase (CIDR) a partir de la dirección
215.25.0.0.  

a) Indicar la longitud de prefijo en bits de la máscara de CIDR empleada en las
organizaciones “A” y “B”.  

b) Indicar las máscaras de CIDR empleadas por ambas organizaciones.  

c) Indicar las direcciones IP de cada una de las redes de “A” y “B”.

__Solución:__

Dice que son ips "sin clase". Así que no contamos con una máscara por defecto. Se la asignamos nosotros en función de los requisitos. 


 - A necesita hasta 2032 máquinas. Necesita por tanto _11 bits para hosts: 2<sup>11</sup> = 2048, que nos darían para 2046 máquinas. Por tanto, __la red tendría 21 bits__. Sería una red __/21__.

 - B necesita hasta 4064 hosts. Con 12 bits se pueden generar 4096 direcciones. Por tanto, __la longitud de la red será de 20 bits: /20__. 

 - La red de A, tendría como direccion original
 205.10.0.0. 
 La red solicitada sería 205.10.0.0/21 (máscara 255.255.248.0).

 Para B, la direccion original era 215.25.0.0, y la red sería 215.25.0.0/20 (máscara 255.255.240.0)

 ## Ejercicio 7
 Una organización dispone de una única red privada de datos a la cual se conectan
todas sus máquinas, permitiendo, por tanto, la comunicación y compartición de
recursos de computación e información entre sus diferentes empleados. 

Con el tiempo dicha organización decide conectar todas sus máquinas a Internet. 
Para ello, se pone en contacto con el correspondiente proveedor del servicio de acceso (ISP) para contratar una dirección IP oficial para la red de la organización. La dirección resultante ofertada por tal proveedor es la __220.10.8.0__ con la máscara __255.255.255.0__.

Posteriormente, la organización decide distribuir sus máquinas en función de 6 departamentos que se han creado internamente para un mejor reparto de funciones y
actividades dentro la entidad. En este nuevo escenario, se considera que la mejor opción es disponer de 6 redes de datos (una red por departamento), independientes e
interconectadas dentro de la organización a través de un mismo router.

a) Teniendo en cuenta que no se desea contratar ninguna nueva dirección IP para la organización y que se desea mantener la misma dirección IP (220.10.8.0),  
¿cómo se pueden asignar direcciones IP a cada una de las 6 nuevas redes y a las máquinas conectadas a dichas redes?

b) ¿Cuál es el número máximo de máquinas que la organización puede conectar a cada una de sus seis redes departamentales?  

c) Indicar las direcciones IP de cada una de las 6 redes de la organización y las máscaras
asociadas a dichas direcciones

__Solución__  
Con subnetting o VLSM. Como no se indican necesidades especícifas por departamento, podemos usar subnetting (todas las subredes con la misma máscara). 
Son 6 departamentos. Descartando las redes todo a 1s y todo a 0s, necesitaríamos 3 bits adicionales para hacer las subredes. Quedando:
 - 27 bits para la red
 - 5 bits para hosts => 32 - 2 = 30 hosts máximo por red.  
 Por tanto, pasaríamos a usar una máscara 
 255.255.255.224.0

 Las 6 subredes serían (descartado todo 1 y todo 0):
 - R1: 220.10.8.001 00000 --> 220.10.8.32
 - R2: 220.10.8.010 00000 --> 220.10.8.64
 - R3: 220.10.8.011 00000 --> 220.10.8.96
 - R4: 220.10.8.100 00000 --> 220.10.8.128
 (Como se puede observar, van de 32 en 32 en decimal)
 - R5: 220.10.8.160
 - R6: 220.10.8.192

## Ejercicio 8 
Responda a las siguientes cuestiones:  
a) Dada la dirección 200.2.1.130/27 ¿Cuáles son las direcciones IP de Hosts válidas?  

/27 llega hasta el último octeto con todo a 1s, y coge 3 bits del mismo.   
En binario sería:  
200.2.1.100_00010  (separao con _ red y host)  
Por tanto, la red sería 200.2.1.128
Y la dirección de BC sería con el host todo a 1s:
200.2.1.100_11111 --> 200.2.1.159  
__Por tanto, los host válidos van desde 200.2.1.129 hasta 200.2.1.158__

b) Dada la IP 134.141.7.7/24, ¿cuáles son las direcciones IP de Hosts válidas?  
Al ser /24 el cálculo es sencillo, ya que los host abarcan justo el último octeto. Como no podemos usar los host con todo a 0s (red) y todo a 1s (BC), los hosts válidos van desde 134.141.7.1 a 134.141.7.254


c) Dada la IP 220.8.7.100 y la máscara 255.255.255.240, ¿cuáles son las direcciones IP
de Hosts válidas?  
De la máscara: 240<sub>10</sub> = 11110000<sub>2</sub>
De la ip: 100<sub>10</sub> = 0110_0100<sub>2</sub> (separo red y host).   
Por tanto, la red es 220.8.7.96. Y el BC sería 220.8.7.211  
Los host válidos irían desde 220.8.7.97 a 220.8.7.210 


d) ¿Cuántas direcciones IP serán asignadas en cada subred de 134.141.0.0/24?  

Nos quedan 8 bits para hosts --> 256 ips. 254 para hosts.   

e) ¿Cuántas direcciones IP serán asignadas en cada subred de 220.8.7.0/28?  

Nos deja 4 bits para direcciones ips. Es decir 16 direcciones (2 menos para hosts). 

f) ¿Cuántas direcciones IP serán asignadas en cada subred de 10.0.0.0/14?  
Nos quedan 12 bits para direcciones. Es decir, 4096 direcciones.   

g) ¿Cuántas direcciones IP serán asignadas en cada subred de 11.0.0.0 255.192.0.0?  
192 es 11000000, así que es una red de 10 bits. Quedan 22 para direcciones. Por tanto, 2<sup>22</sup> direcciones posibles. 


h) Diseñas una red para un cliente, y el cliente te pide que utilices la misma máscara
de subred para toda las subredes. El cliente utiliza la red 10.0.0.0 y necesita 200
subredes, con 200 hosts como máximo en cada subred. ¿Qué máscara trabajará
mejor y permitirá mayor crecimiento en el número de host por subred a futuro?
 
Para 200 hosts como máximo necesitamos 8 bits, que nos permitirá 256-2 hosts. Así que para ese requisito necesitamos una /24 o máscara 255.255.255.0. 

Pero nos piden priorizar el crecimiento de hosts. Así que priorizamos el requisito de 200 subredes. Para 200 subredes necesitamos 8 bits. La ip es de clase A por lo que su máscara es una /8. Si sumamos 8 bits más, será una /16. Es decir, máscara 255.255.0.0

## Ejercicio 9 
Responda a las siguientes cuestiones:  
a) Calcular la dirección de red y dirección de broadcasting (difusión) de las máquinas con las siguientes direcciones IP y máscaras de subred (si no se especifica, se utiliza la máscara por defecto):  

 - 18.120.16.250 / máscara 255.0.0.0  
 Red: 18.0.0.0. BC: 18.255.255.255

 - 18.120.16.255 / 255.255.0.0  
 Red 18.120.0.0. BC: 18.120.255.255

 - 155.4.220.39 / 255.255.0.0  
 Red 155.4.0.0. BC: 155.4.255.255

 - 194.209.14.33 / 255.255.255.0  
 Red: 194.209.14.0. BC: 194.209.14.255  

 - 190.33.109.133 / 255.255.255.0  
 Red: 190.33.109.0. BC: 190.33.109.255

b) Suponiendo que nuestro ordenador tiene la dirección IP 192.168.5.65 con máscara 255.255.255.0, indicar qué significan las siguientes direcciones especiales:
 - 0.0.0.0: es una direccion virtual para referenciar a cualquier dirección o ruta por defecto. 
 - 0.0.0.29: Reservada por la IANA, como todas las 0.0.0.0/8
 - 192.168.67.0: Es una direccion de red clase C, no sasignable a hosts. 
 - 255.255.255.255: Direccion de BC de la subred (los router nos envian BC a otras subredes). 
 - 192.130.10.255: BC de la red 192.130.10.0. 
 - 127.0.0.1: IP de loopback o localhost. Equivale a nuestra ip. 

d) Viendo las direcciones IP de los hosts públicos de una empresa observamos que
todas están comprendidas entre 194.143.17.145 y 194.143.17.158, ¿Cuál es
(probablemente) su dirección de red, broadcasting y máscara?

Suponiendo que cubran todo el rango posible de ips de su subred:
Si la primera es 194.143.17.145, la red podría ser la 144 -> 194.143.17.10010000. Parece una /28. 
La última 194.143.17.158. Por tanto la de BC sería la 159 -> 194.143.17.10011111. 
Por tanto:
 - Red: 194.143.17.144
 - BC: 194.143.17.159
 - Máscara: /28 o 255.255.255.240

## Ejercicio 10 

Se tiene la IP 155.10.0.0 y se quieren implementar 450 subredes y 90 host. Encontrar la máscara de subred, las direcciones para las subredes 0 a 5 y si las siguientes
direcciones IP son válidas para host.
a) 155.10.47.28
b) 155.10.255.0
c) 155.10.64.128
d) 155.10.128.64
e) 155.10.244.0

la ip 155.10.x.x es Clase B. Con máscara 255.255.0.0 o /16. 
Si se quieren 450 subredes necesitamos 9 bits (512 subredes). Quedando una máscara /25. Eso nos deja 7 bits para hosts, que admiten hasta 128 - 2 hosts. Es factible el enunciado. 

La máscara de las subredes sería 255.255.255.128  
155.10.0.0_0000000 sería la ip con esa máscara
Las direcciones de las primeras 5 redes, excluyendo la todo a 0s:
155.10.0.1_0000000 --> 155.10.0.128
155.10.00000001.0_0000000 --> 155.10.1.0
155.10.00000001.1_0000000 --> 155.10.1.128
155.10.00000010.0_0000000 --> 155.10.2.0
155.10.00000010.1_0000000 --> 155.10.2.128

a) 155.10.47.28 --> 155.10.00101111.0_0011100
 Es válida. Es una ip de la red 155.10.0010111.0 -> 155.10.47.0  

b) 155.10.255.0. Se ve rápido que tiene a 0 todos los bits de hosts. Es una red. Inválida. 

c) 155.10.64.128 --> 155.10.01000000.1_0000000  
Es una direccion de red, porque tiene a 0 todos los bits de hosts. No es válida.   

d) 155.10.128.64  
155.10.1000000.0_1000000. Es válida. 

e) 155.10.244.0  
155.10.11110100.0_0000000. Es una red. No válida. 








