## Práctica 61

### Ejercicio 1: Determinar la parte de la dirección IP que corresponde al host y a la red
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


### Ejercicio 3. Subnetting
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


