# Seguridad y Protección de Sistemas Informáticos
# Práctica 1: Criptosistemas Simétricos

## 1. Partiremos de un archivo binario de 1024 bits, todos ellos con valor 0. Para hacer referencia al mismo voy a suponer que se llama input.bin , pero podéis dar el nombre que os convenga.

Creamos el fichero junto con su contenido mediante un bucle for con 1024 iteraciones, que se encarga de pintar un cero en cada iteración.

>>for i in {0..1023}; do printf "0" >> input.bin; done

>>Captura input.bin

## 2. Creamos otro archivo binario del mismo tamaño, que contenga un único bit con valor 1 dentro de los primeros 40 bits y todos los demás con valor 0. Me referiré a este archivo como input1.bin.

Podemos crear el archivo input1.bin a través de una orden usando input.bin y en la posición que indiquemos, escribir un 1, pero es más sencillo hacer una copia de input.bin y editar el fichero.

>>Captura input1.bin

## 3. Cifrad input.bin con DES en modos ECB , CBC y OFB usando como claves una débil y otra semidébil, con vector de inicialización a vuestra elección, y explicad los diferentes resultados.

DES es un algoritmo de cifrado por bloques, toma un texto plano de una longitud fija y lo transforma en otro texto cifrado de la misma longitud.
Este tipo de cifrado utiliza bloques de 64 bits.

Como claves he utilizado:

-Clave débil: 0101010101010101

-Clave semidébil: FE01FE01FE01FE01

-Clave fuerte: FA19234EA6D0F951

Y como vector de inicialización 0.

>>Captura de pantalla de comandos

Resultados:

* ECB

Cifrado con clave débil:

>>Captura ECB_debil

Cifrado con clave semidébil:

>>Captura ECB_semidebil

Como se puede observar, en ambos textos cifrados hacen uso de un mismo patrón, al ser un cifrado por bloques, se aplica la misma clave a cada uno de ellos. Por tanto si utiliza bloques de 64 bits, tendremos 16 bloques que repiten el mismo patrón de cifrado.
En la clave semi-débil tenemos mayor cantidad de caracteres diferentes en el patrón.

* CBC

Cifrado con clave débil:

>>Captura CBC_debil

Cifrado con clave semidébil:

>>Captura CBC_semidebil

(En el cifrado con clave débil me debería de salir un patrón repitiéndose)

* OFB

Cifrado con clave débil:

>>Captura OFB_debil

Cifrado con clave semidébil:

>>Captura OFB_semidebil

De nuevo, en la captura de OFB con clave débil, comprobamos que se vuelven a repetir los patrones, en este caso cada bloque de 8 bits se repite una vez si una vez no, es decir, el primer bloque se repite en el tercero, en el quinto y así sucesivamente. Por otro lado el segundo bloque se repite en cada posición par. Esto se debe a que cifrar dos veces con la misma clave equivale a descifrar, por tanto siempre se está cifrando y descifrando con el mismo valor.

En cambio con la clave semi-débil, no se produce esta repetición de patrones debido a que no ciframos con cada pareja de la clave.

## 4. Cifrad input.bin e input1.bin con DES en modo ECB y clave a elegir, pero no débil ni semidébil. Explicad la forma de los resultados obtenidos.

>>Captura comandos ejer4

* input

* input1

Al igual que en los ejercicios anteriores vemos que se repiten los mismos patrones en cada bloque, debido a que todos los bits son 0. En el caso de input1 como en la primera posición tenemos un 1 el primer bloque cambia con respecto a los demás.

## 5. Cifrad input.bin e input1.bin con DES en modo CBC, clave y vector de inicialización a elegir. Comparad con los resultados obtenidos en el apartado anterior.

>>Captura comandos ejer5

Al utilizar una división en bloques, la salida de cada bloque es sumada a la entrada del siguiente bloque, por tanto cada bloque cifrado es distinto al anterior y no podemos detectar ninguna repetición de un mismo patrón.

## 6. Repetid los puntos 4 a 5 con AES-128 y AES-256.

>>Captura comandos ejer6

* Punto 4:



* Punto 5:
