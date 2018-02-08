# Seguridad y Protección de Sistemas Informáticos
# Práctica 3: Protocolos Criptográficos

## 1. Generad un archivo sharedDSA.pem que contenga los parámetros. Mostrad los valores.

Para generar que contenga los parámetros usamos la opción “dsaparam”, en mi caso he elegido un tamaño de 2048 bits.

![curl](https://github.com/franfermi/Seguridad-Proteccion-Equipos-Informaticos_SPSI/blob/master/Pr%C3%A1ctica-3/Capturas/comando_ejer1.png)

Los valores del fichero generado son los siguientes:

![curl](https://github.com/franfermi/Seguridad-Proteccion-Equipos-Informaticos_SPSI/blob/master/Pr%C3%A1ctica-3/Capturas/valores_ejer1.png)

En la parte derecha de la captura se muestran los parámetros generados.

## 2. Generad dos parejas de claves para los parámetros anteriores. La claves se almacenarán en los archivos nombreDSAkey.pem y apellidoDSAkey.pem . No es necesario protegerlas por contraseña.

En la generación del ar de claves usamos la opción “gendsa”, generamos dos pares de claves, un par por cada archivo.

![curl](https://github.com/franfermi/Seguridad-Proteccion-Equipos-Informaticos_SPSI/blob/master/Pr%C3%A1ctica-3/Capturas/comando_ejer2.png)

El contenido de las claves generadas de ambos ficheros es el siguiente:

![curl](https://github.com/franfermi/Seguridad-Proteccion-Equipos-Informaticos_SPSI/blob/master/Pr%C3%A1ctica-3/Capturas/valores_ejer2.png)

Podemos observar en detalles que usamos el algoritmo DSA y que es de tamaño 2048 que es el tamaño de la clave que hemos generado anteriormente.

## 3. “Extraed” la clave privada contenida en el archivo nombreDSAkey.pem a otro archivo que tenga por nombre nombreDSApriv.pem . Este archivo deberá estar protegido por contraseña. Mostrad sus valores. Lo mismo para el archivo apellidoDSAkey.pem .

Para extraer la clave privada de los archivos anteriormente obtenidos, utilizamos la opción “dsa -des3”, tanto con un archivo como con el otro. Como clave de ambos archivos he utilizado la clave por defecto de la práctica pasada “0123456789”.

![curl](https://github.com/franfermi/Seguridad-Proteccion-Equipos-Informaticos_SPSI/blob/master/Pr%C3%A1ctica-3/Capturas/comandos_ejer3.png)

Los resultados obtenidos son los siguientes:

![curl](https://github.com/franfermi/Seguridad-Proteccion-Equipos-Informaticos_SPSI/blob/master/Pr%C3%A1ctica-3/Capturas/valores_ejer3.png)

Si los comparamos con los obtenidos en el ejercicio anterior, observamos que poseen la misma clave privada pero en este caso se encuentran protegidos por contraseña.

## 4. Extraed en nombreDSApub.pem la clave pública contenida en el archivo nombreDSAkey.pem . De nuevo nombreDSApub.pem no debe estar cifrado ni protegido. Mostrad sus valores. Lo mismo para el archivo apellidoDSAkey.pem.

En la extracción de la clave pública, usamos la opción “dsa -pubin” y en el mismo comando si queremos mostrar los resultados de la clave, usamos “-text -noout”. En mi caso me ha salido un poco extenso debido al tamaño de la clave generada, al ser de 2048 bits.

Fichero 1:

![curl](https://github.com/franfermi/Seguridad-Proteccion-Equipos-Informaticos_SPSI/blob/master/Pr%C3%A1ctica-3/Capturas/valores_ejer4_com1-1.png)

![curl](https://github.com/franfermi/Seguridad-Proteccion-Equipos-Informaticos_SPSI/blob/master/Pr%C3%A1ctica-3/Capturas/valores_ejer4_com1-2.png)

Fichero 2:

![curl](https://github.com/franfermi/Seguridad-Proteccion-Equipos-Informaticos_SPSI/blob/master/Pr%C3%A1ctica-3/Capturas/valores_ejer4_com2-1.png)

![curl](https://github.com/franfermi/Seguridad-Proteccion-Equipos-Informaticos_SPSI/blob/master/Pr%C3%A1ctica-3/Capturas/valores_ejer4_com2-2.png)

## 5. Calculad el valor hash del archivo con la clave pública nombreDSApub.pem usando sha384 con salida hexadecimal con bloques de dos caracteres separados por dos puntos. Mostrad los valores por salida estándar y guardadlo en nombreDSApub.sha384.

Para calcular el valor hash del archivo mediante la clave pública obtenida en el apartado anterior, usamos la opción “dgst -sha384” y para mostrar su salida de forma hexadecimal en bloques de dos caracteres separados por dos puntos, utilizamos “-hex -c”.

![curl](https://github.com/franfermi/Seguridad-Proteccion-Equipos-Informaticos_SPSI/blob/master/Pr%C3%A1ctica-3/Capturas/comando_ejer5.png)

Como último argumento en el comando, hay que añadir el archivo el cuál contiene la clave pública.

El valor hash obtenido es el siguiente:

![curl](https://github.com/franfermi/Seguridad-Proteccion-Equipos-Informaticos_SPSI/blob/master/Pr%C3%A1ctica-3/Capturas/valores_ejer5.png)

## 6. Calculad el valor hash del archivo con la clave pública apellidoDSApub.pem usando una función hash de 160 bits con salida binaria. Guardad el hash en apellidoDSApub.[algoritmo] y mostrad su contenido.

Para calcular el valor hash, a diferencia con el ejercicio anterior, tenemos que hacer uso de una función hash de 160 bits, para ello usamos “dgst -ripemd160” y como la salida debe de ser binaria pues añadimos el parámetro “-binary”.

![curl](https://github.com/franfermi/Seguridad-Proteccion-Equipos-Informaticos_SPSI/blob/master/Pr%C3%A1ctica-3/Capturas/comando_ejer6.png)

El valor hash obtenido es el siguiente:

![curl](https://github.com/franfermi/Seguridad-Proteccion-Equipos-Informaticos_SPSI/blob/master/Pr%C3%A1ctica-3/Capturas/valores_ejer6.png)

## 7. Generad el valor HMAC del archivo sharedDSA.pem con clave ’12345’ mostrándolo por pantalla.

Para generar el valor HMAC del archivo sharedDSA, usamos la opción “-hmac” y le asignamos la contraseña especificada en la práctica “12345”, por último añadimos el archivo a partir del cual se quiere generar el valor.

![curl](https://github.com/franfermi/Seguridad-Proteccion-Equipos-Informaticos_SPSI/blob/master/Pr%C3%A1ctica-3/Capturas/comando_ejer7.png)

## 8. Simulad una ejecución completa del protocolo Estación a Estación. Para ello emplearemos como claves para firma/vericación las generadas en esta práctica, y para el protocolo DH emplearemos las claves asociadas a curvas elípticas de la práctica anterior junto con las de otro usuario simulado que deberéis generar nuevamente.

## Por ejemplo, si mi clave privada esta en javierECpriv.pem y la clave pública del otro usuario está en lobilloECpub.pem , el comando para generar la clave derivada será:

	$> openssl pkeyutl -inkey javierECpriv.pem -peerkey lobilloECpub.pem -derive -out
	key.bin

## El algoritmo simétrico a utilizar en el protocolo estación a estación será AES-128 en modo CFB8.

Lo primero que tenemos que hacer es tener todos los archivos necesarios para el ejercicio, para ello tenemos que obtener las claves asociadas a curvas elípticas del otro usuario. Como en la práctica anterior tenemos que hacer:
Generamos una clave a partir de los parámetros de la curva elíptica.

![curl](https://github.com/franfermi/Seguridad-Proteccion-Equipos-Informaticos_SPSI/blob/master/Pr%C3%A1ctica-3/Capturas/comandos_ejer8-01.png)

Extraemos la clave pública y privada a partir de la clave generada.

![curl](https://github.com/franfermi/Seguridad-Proteccion-Equipos-Informaticos_SPSI/blob/master/Pr%C3%A1ctica-3/Capturas/comandos_ejer8-02.png)

Partimos de los siguientes archivos:

A:

-FranciscoDSApriv.pem

-FranciscoDSApub.pem

-FernandezDSApub.pem

B:

-FernandezDSApriv.pem

-FernandezDSApub.pem

-FranciscoDSApub.pem

A → a partir de stdECparam obtiene FranciscoECpriv.pem y FranciscoECpub.pem, envía FranciscoECpub.pem a B.

B → a partir de stdECparam obtiene FernandezECpriv.pem  y FernandezECpub.pem.

El usuario B como tiene la clave pública de A, puede generar la derivada con la pública de A y su clave privada.

![curl](https://github.com/franfermi/Seguridad-Proteccion-Equipos-Informaticos_SPSI/blob/master/Pr%C3%A1ctica-3/Capturas/comandos_ejer8-07.png)

Realizamos la concatenación con las claves públicas de A y B, en B.

![curl](https://github.com/franfermi/Seguridad-Proteccion-Equipos-Informaticos_SPSI/blob/master/Pr%C3%A1ctica-3/Capturas/comandos_ejer8-08.png)

Una vez tenemos la concatenación, la firmamos con la clave DSA privada de B y ciframos la concatenación firmada con la clave derivada generada de B.

![curl](https://github.com/franfermi/Seguridad-Proteccion-Equipos-Informaticos_SPSI/blob/master/Pr%C3%A1ctica-3/Capturas/comandos_ejer8-09.png)

B → manda a A la concatenación cifrada y firmada, junto con su clave EC pública.

A → a partir de la clave EC pública de B, puede generar la derivada con la pública de B y su clave privada.

![curl](https://github.com/franfermi/Seguridad-Proteccion-Equipos-Informaticos_SPSI/blob/master/Pr%C3%A1ctica-3/Capturas/comandos_ejer8-03.png)

A → desciframos la concatenación cifrada y firmada por B, y verificamos la firma con la clave pública de B.

![curl](https://github.com/franfermi/Seguridad-Proteccion-Equipos-Informaticos_SPSI/blob/master/Pr%C3%A1ctica-3/Capturas/comandos_ejer8-10.png)

Como A ya tiene la clave pública de B, puede concatenar ambas claves.

![curl](https://github.com/franfermi/Seguridad-Proteccion-Equipos-Informaticos_SPSI/blob/master/Pr%C3%A1ctica-3/Capturas/comandos_ejer8-04.png)

La concatenación la firma A con su clave DSA privada.

![curl](https://github.com/franfermi/Seguridad-Proteccion-Equipos-Informaticos_SPSI/blob/master/Pr%C3%A1ctica-3/Capturas/comandos_ejer8-05.png)

Y la cifra con su clave derivada generada.

![curl](https://github.com/franfermi/Seguridad-Proteccion-Equipos-Informaticos_SPSI/blob/master/Pr%C3%A1ctica-3/Capturas/comandos_ejer8-6.png)

Dicha concatenación firmada y cifrada se la pasa a B.

B → obtiene la concatenación cifrada y firmada por parte de A y procede a descifrar y verificar su firma.

Descifra con su clave generada derivada y verifica la firma de A con la clave pública de A que ya la tenía de pasos anteriores.

![curl](https://github.com/franfermi/Seguridad-Proteccion-Equipos-Informaticos_SPSI/blob/master/Pr%C3%A1ctica-3/Capturas/comandos_ejer8-11.png)
