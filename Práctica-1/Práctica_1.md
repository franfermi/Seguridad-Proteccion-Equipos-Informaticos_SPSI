# Seguridad y Protección de Sistemas Informáticos
# Práctica 1: Criptosistemas Simétricos

## 1. Partiremos de un archivo binario de 1024 bits, todos ellos con valor 0. Para hacer referencia al mismo voy a suponer que se llama input.bin , pero podéis dar el nombre que os convenga.

Creamos el fichero de la siguiente forma.
-Creamos un fichero de 16 bits:
	echo -e -n '\x00\x00' > aux16.bin
-Teniendo el fichero binario de 2 bytes hacemos lo siguiente:
	cat aux16.bin aux16.bin > aux32.bin
De esta forma sumamos ambos archivos y lo almacenamos, obteniendo así un archivo de 32 bits, así sucesivamente hasta obtener el fichero de 1024 bits. El fichero debe de tener un tamaño de 128 Bytes.

![curl](https://github.com/franfermi/Seguridad-Proteccion-Equipos-Informaticos_SPSI/blob/master/Pr%C3%A1ctica-1/Capturas/input.png)

## 2. Creamos otro archivo binario del mismo tamaño, que contenga un único bit con valor 1 dentro de los primeros 40 bits y todos los demás con valor 0. Me referiré a este archivo como input1.bin.

Podemos crear el archivo input1.bin usando el procedimiento anterior , pero es más sencillo hacer una copia de input.bin y editar el fichero.

![curl](https://github.com/franfermi/Seguridad-Proteccion-Equipos-Informaticos_SPSI/blob/master/Pr%C3%A1ctica-1/Capturas/input1.png)

## 3. Cifrad input.bin con DES en modos ECB , CBC y OFB usando como claves una débil y otra semidébil, con vector de inicialización a vuestra elección, y explicad los diferentes resultados.

DES es un algoritmo de cifrado por bloques, toma un texto plano de una longitud fija y lo transforma en otro texto cifrado de la misma longitud.
Este tipo de cifrado utiliza bloques de 64 bits.

![curl](https://github.com/franfermi/Seguridad-Proteccion-Equipos-Informaticos_SPSI/blob/master/Pr%C3%A1ctica-1/Capturas/comandos_ejer3.png)

Resultados:

* ECB

Cifrado con clave débil:

![curl](https://github.com/franfermi/Seguridad-Proteccion-Equipos-Informaticos_SPSI/blob/master/Pr%C3%A1ctica-1/Capturas/ejer3_ECB_debil.png)

Cifrado con clave semidébil:

![curl](https://github.com/franfermi/Seguridad-Proteccion-Equipos-Informaticos_SPSI/blob/master/Pr%C3%A1ctica-1/Capturas/ejer3_ECB_semidebil.png)

Como se puede observar, ambos cifrados hacen uso de un mismo patrón, al ser un cifrado por bloques, se aplica la misma clave a cada uno de ellos y como todos los bloques son iguales, el resultado es el mismo. Por tanto si utiliza bloques de 64 bits, tendremos 16 bloques que repiten el mismo patrón de cifrado, lo que hace un total de 1024 bits.

* CBC

Cifrado con clave débil:

![curl](https://github.com/franfermi/Seguridad-Proteccion-Equipos-Informaticos_SPSI/blob/master/Pr%C3%A1ctica-1/Capturas/ejer3_CBC_debil.png)

Cifrado con clave semidébil:

![curl](https://github.com/franfermi/Seguridad-Proteccion-Equipos-Informaticos_SPSI/blob/master/Pr%C3%A1ctica-1/Capturas/ejer3_CBC_semidebil.png)

Con clave débil se repite el mismo patrón, esto es debido a que al realizar la operación XOR al bloque con un vector de inicialización a 0, obtenemos el propio vector. A la salida de este bloque se le realiza la suma XOR con el siguiente bloque en texto plano y hace uso del vector de inicialización. Al cifrar dos veces con la misma clave obtenemos el mismo bloque.
Con la clave semidébil no ocurre esta repetición, esto es debido a que las claves débiles vienen dadas por parejas, osea que una pareja cifra y la siguiente descifra.

* OFB

Cifrado con clave débil:

![curl](https://github.com/franfermi/Seguridad-Proteccion-Equipos-Informaticos_SPSI/blob/master/Pr%C3%A1ctica-1/Capturas/ejer3_OFB_debil.png)

Cifrado con clave semidébil:

![curl](https://github.com/franfermi/Seguridad-Proteccion-Equipos-Informaticos_SPSI/blob/master/Pr%C3%A1ctica-1/Capturas/ejer3_OFB_semidebil.png)

De nuevo, en la captura de OFB con clave débil, comprobamos que se vuelven a repetir los patrones, en este caso cada bloque de 64 bits se repite una vez si una vez no, es decir, el primer bloque se repite en el tercero, en el quinto y así sucesivamente. Por otro lado el segundo bloque se repite en cada posición par da lugar al texto descifrado. Esto se debe a que cifrar dos veces con la misma clave equivale a descifrar, por tanto siempre se está cifrando y descifrando con el mismo valor. También por haber usado un vector de inicialización a 0, hace que siempre se utilice la misma suma XOR.
En cambio con la clave semi-débil, no se produce esta repetición de patrones debido a que no ciframos con cada misma pareja clave y como se cifra mediante el bloque anterior hace que sean distintos.

## 4. Cifrad input.bin e input1.bin con DES en modo ECB y clave a elegir, pero no débil ni semidébil. Explicad la forma de los resultados obtenidos.

![curl](https://github.com/franfermi/Seguridad-Proteccion-Equipos-Informaticos_SPSI/blob/master/Pr%C3%A1ctica-1/Capturas/comandos_ejer4.png)

* input

![curl](https://github.com/franfermi/Seguridad-Proteccion-Equipos-Informaticos_SPSI/blob/master/Pr%C3%A1ctica-1/Capturas/ejer4_DES_ECB_input.png)

* input1

![curl](https://github.com/franfermi/Seguridad-Proteccion-Equipos-Informaticos_SPSI/blob/master/Pr%C3%A1ctica-1/Capturas/ejer4_DES_ECB_input1.png)

Al igual que en los ejercicios anteriores vemos que se repiten los mismos patrones en cada bloque, debido a que todos los bytes son 0 y se le aplica a todos los bloques el mismo cifrado. En el caso de input1 como en la primera posición tenemos un 1 el primer bloque cambia con respecto a los demás.

## 5. Cifrad input.bin e input1.bin con DES en modo CBC, clave y vector de inicialización a elegir. Comparad con los resultados obtenidos en el apartado anterior.

![curl](https://github.com/franfermi/Seguridad-Proteccion-Equipos-Informaticos_SPSI/blob/master/Pr%C3%A1ctica-1/Capturas/ejer5_DES_CBC_input.png)

-input

![curl](https://github.com/franfermi/Seguridad-Proteccion-Equipos-Informaticos_SPSI/blob/master/Pr%C3%A1ctica-1/Capturas/captura_ejer5.png)

-input1

![curl](https://github.com/franfermi/Seguridad-Proteccion-Equipos-Informaticos_SPSI/blob/master/Pr%C3%A1ctica-1/Capturas/ejer5_DES_CBC_input1.png)

Al utilizar una división en bloques, la salida de cada bloque es sumada con XOR a la entrada del siguiente bloque, por tanto cada bloque cifrado es distinto al anterior y no podemos detectar ninguna repetición de un mismo patrón en ninguno de los casos.

## 6. Repetid los puntos 4 a 5 con AES-128 y AES-256.

![curl](https://github.com/franfermi/Seguridad-Proteccion-Equipos-Informaticos_SPSI/blob/master/Pr%C3%A1ctica-1/Capturas/comandos_ejer6.png)

-ECB 128 input

![curl](https://github.com/franfermi/Seguridad-Proteccion-Equipos-Informaticos_SPSI/blob/master/Pr%C3%A1ctica-1/Capturas/ejer6_AES_ECB_128_input.png)

-ECB 256 input

![curl](https://github.com/franfermi/Seguridad-Proteccion-Equipos-Informaticos_SPSI/blob/master/Pr%C3%A1ctica-1/Capturas/ejer6_AES_ECB_256_input.png)

-ECB 128 input1

![curl](https://github.com/franfermi/Seguridad-Proteccion-Equipos-Informaticos_SPSI/blob/master/Pr%C3%A1ctica-1/Capturas/ejer6_AES_ECB_128_input1.png)

-ECB 256 input1

![curl](https://github.com/franfermi/Seguridad-Proteccion-Equipos-Informaticos_SPSI/blob/master/Pr%C3%A1ctica-1/Capturas/ejer6_AES_ECB_256_input1.png)

Al igual que en los casos anteriores, con el modo ECB encontramos repeticiones de bloques, en este caso son de 128 bits dando igual que la clave sea fuerte. En input se repite la misma secuencia en los 8 bloques debido a que el contenido es el mismo, en el caso de input1 se produce el cambio por el 1 en la primera posición.

-CBC 128 input

![curl](https://github.com/franfermi/Seguridad-Proteccion-Equipos-Informaticos_SPSI/blob/master/Pr%C3%A1ctica-1/Capturas/ejer6_AES_CBC_128_input.png)

-CBC 256 input

![curl](https://github.com/franfermi/Seguridad-Proteccion-Equipos-Informaticos_SPSI/blob/master/Pr%C3%A1ctica-1/Capturas/ejer6_AES_CBC_256_input.png)

-CBC 128 input1

![curl](https://github.com/franfermi/Seguridad-Proteccion-Equipos-Informaticos_SPSI/blob/master/Pr%C3%A1ctica-1/Capturas/ejer6_AES_CBC_128_input1.png)

-CBC 256 input1

![curl](https://github.com/franfermi/Seguridad-Proteccion-Equipos-Informaticos_SPSI/blob/master/Pr%C3%A1ctica-1/Capturas/ejer6_AES_CBC_256_input1.png)

Con CBC al utilizar una clave fuerte no hay forma de encontrar una sucesión que se repita en el texto cifrado. La diferencia entre AES 128 y AES 256 es el tamaño de la clave, que puede ser de 128 bits o 256 bits.
Con el cifrado DES en modo CBC, si teníamos una clave débil, podíamos observar las repeticiones al igual que en el modo ECB, este problema se soluciona con AES ya que su tamaño de bloque es de 128 bits. (Aunque en el caso de la imagen he utilizado una clave fuerte, he probado con una débil y no se puede encontrar ninguna sucesión).

## 7. Cifrad input.bin con AES-192 en modo OFB , clave y vector de inicialización a elegir. Supongamos que la salida es output.bin.

![curl](https://github.com/franfermi/Seguridad-Proteccion-Equipos-Informaticos_SPSI/blob/master/Pr%C3%A1ctica-1/Capturas/comandos_ejer7.png)

![curl](https://github.com/franfermi/Seguridad-Proteccion-Equipos-Informaticos_SPSI/blob/master/Pr%C3%A1ctica-1/Capturas/ejer7_output.png)

## 8. Descifra output.bin utilizando la misma clave y vector de inicialización que en 7.

![curl](https://github.com/franfermi/Seguridad-Proteccion-Equipos-Informaticos_SPSI/blob/master/Pr%C3%A1ctica-1/Capturas/comandos_ejer8.png)

![curl](https://github.com/franfermi/Seguridad-Proteccion-Equipos-Informaticos_SPSI/blob/master/Pr%C3%A1ctica-1/Capturas/ejer7_output_descifrado.png)

## 9. Vuelve a cifrar output.bin con AES-192 en modo OFB , clave y vector de inicialización del punto 7. Compara el resultado obtenido con el punto 8, explicando el resultado.

![curl](https://github.com/franfermi/Seguridad-Proteccion-Equipos-Informaticos_SPSI/blob/master/Pr%C3%A1ctica-1/Capturas/comandos_ejer9.png)

![curl](https://github.com/franfermi/Seguridad-Proteccion-Equipos-Informaticos_SPSI/blob/master/Pr%C3%A1ctica-1/Capturas/ejer9_output2.png)

Obtenemos la misma salida que descifrando, esto es debido a que si ciframos dos veces con la misma clave y vector de inicialización conseguimos lo mismo que descifrando.

## 10. Presentad la descripción de otro cifrado simétrico que aparezca en vuestra implementación de OpenSSL.

*Cifrado en Base64:*

-¿Qué es Base64?

Es un algoritmo que cifra los datos basándose en un diccionario de 64 caracteres.
ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789+/

-¿Cómo funciona el cifrado en Base64?

Supongamos que tenemos el siguiente texto a cifrar: Buen_día

Cada carácter que compone el texto representa un byte de información, es decir 8 bits, cada bit puede tomar valores 0 o 1.
Para cifrar en Base64 tomamos los 3 primeros caracteres del texto y obtenemos su valor en binario.

B	01000010

u 01110101         

e 01100101

Trás obtener los 24 bits de información, pasamos a dividir en partes de 6 bits, ya que con 6 bits podemos obtener valores entre 0 y 63, y con ese valor, obtenemos un carácter del diccionario base.

Q 010000 	      

n 100111 	        

V 010101         

l 100101

Continuamos con los siguientes caracteres.

n 01101110        			

_	01011111            

d 01100100

Volvemos a cifrar en Base64.

b 011011 	       

l 100101 	        

9 111101        

k 100100

Y por último, a los dos caracteres que faltan realizamos el mismo procedimiento, como faltaría un tercer carácter, éste último lo completamos con 0s.

í	11101101         		

a	01100001

Para finalizar, ciframos en Base64 los últimos caracteres.

7	111011		    

W 010110	    

E 000100

El resultado final es el siguiente:

Buen_día → QnVlbl9k7WE


-¿Cómo funciona el cifrado en Base64?

Para el descifrado tenemos que realizar los pasos anteriores pero hacia atrás. Es decir,
componemos bloques de 24 bits, los dividimos entre 8 bits y por último calculamos su 	correspondiente carácter en ASCII.

## 11. Repetid los puntos 3 a 5 con el cifrado presentado en el punto 10 (el 3 si el cifrado elegido tuviese claves débiles o semidébiles).

*Punto 3, Base64.*

![curl](https://github.com/franfermi/Seguridad-Proteccion-Equipos-Informaticos_SPSI/blob/master/Pr%C3%A1ctica-1/Capturas/comandos_ejer11.png)

![curl](https://github.com/franfermi/Seguridad-Proteccion-Equipos-Informaticos_SPSI/blob/master/Pr%C3%A1ctica-1/Capturas/captura_ejer11_01.png)

Tanto con clave débil como semidébil se obtiene la misma salida. Esta salida da como resultado A debido a que en Base64, 000000 corresponde a al carácter A del diccionario. El punto aparece en cada bloque de 64 bits.

*Puntos 4 y 5, Base64 input.*

![curl](https://github.com/franfermi/Seguridad-Proteccion-Equipos-Informaticos_SPSI/blob/master/Pr%C3%A1ctica-1/Capturas/comandos_ejer11_02.png)

![curl](https://github.com/franfermi/Seguridad-Proteccion-Equipos-Informaticos_SPSI/blob/master/Pr%C3%A1ctica-1/Capturas/captura_ejer11_02.png)

Como podemos observar, el nivel de seguridad de la clave es indiferente en este tipo de cifrado.

*Puntos 4 y 5, Base64 input1.*

![curl](https://github.com/franfermi/Seguridad-Proteccion-Equipos-Informaticos_SPSI/blob/master/Pr%C3%A1ctica-1/Capturas/comandos_ejer11_03.png)

![curl](https://github.com/franfermi/Seguridad-Proteccion-Equipos-Informaticos_SPSI/blob/master/Pr%C3%A1ctica-1/Capturas/captura_ejer11_03.png)

En el caso de input1, como tenemos en la primera posición el bit a 1, es lo único que cambia en la salida.

Aparece el carácter E porque:

1º. Miramos en el diccionario Base64 la posición del carácter E, sería 4.

2º. La posición 4 en binario es: 00000100.

3º. En Base64, se cogen los 6 primeros bits: 000001.

4º. 000001 corresponde a 1.
