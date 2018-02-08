# Seguridad y Protección de Sistemas Informáticos
# Práctica 2: Criptosistemas Asimétricos

## 1. Generad, cada uno de vosotros, una clave RSA (que contiene el par de claves) de 768 bits. Para referirnos a ella supondré que se llama nombreRSAkey.pem. Esta clave no es necesario que esté protegida por contraseña.

Para generar la clave usamos la opción “genrsa” y especificamos el tamaño de 768 bits.

![curl](https://github.com/franfermi/Seguridad-Proteccion-Equipos-Informaticos_SPSI/blob/master/Pr%C3%A1ctica-2/Capturas/Generar_clave_RSA.png)

El contenido de la clave generada es el siguiente:

![curl](https://github.com/franfermi/Seguridad-Proteccion-Equipos-Informaticos_SPSI/blob/master/Pr%C3%A1ctica-2/Capturas/clave_RSA_ejer1.png)

## 2. “Extraed” la clave privada contenida en el archivo nombreRSAkey.pem a otro archivo que tenga por nombre nombreRSApriv.pem. Este archivo deberá estar protegido por contraseña cifrándolo con AES-128. Mostrad sus valores.

Para extraer la clave privada del archivo anterior usamos la opción “rsa”, especificamos el tipo de cifrado que se le va a realizar y la contraseña que contendrá el archivo de salida.

![curl](https://github.com/franfermi/Seguridad-Proteccion-Equipos-Informaticos_SPSI/blob/master/Pr%C3%A1ctica-2/Capturas/extraer_key.png)

Para poder ver su contenido se nos pide que introduzcamos la contraseña que anteriormente hemos asignado.

![curl](https://github.com/franfermi/Seguridad-Proteccion-Equipos-Informaticos_SPSI/blob/master/Pr%C3%A1ctica-2/Capturas/clave_RSA_privada_ejer2.png)

Una vez introducida podemos ver su contenido.

![curl](https://github.com/franfermi/Seguridad-Proteccion-Equipos-Informaticos_SPSI/blob/master/Pr%C3%A1ctica-2/Capturas/clave_RSA_ejer2.png)

## 3. Extraed en nombreRSApub.pem la clave pública contenida en el archivo nombreRSAkey.pem . Evidentemente nombreRSApub.pem no debe estar cifrado ni protegido. Mostrad sus valores.

Para extraer la clave pública a partir de la clave generada en el ejercicio 1, usamos la opción “rsa -pubout”.

![curl](https://github.com/franfermi/Seguridad-Proteccion-Equipos-Informaticos_SPSI/blob/master/Pr%C3%A1ctica-2/Capturas/obtener_key_pub_ejer3.png)

Estos son los valores de las claves pública/privada extraídas.

![curl](https://github.com/franfermi/Seguridad-Proteccion-Equipos-Informaticos_SPSI/blob/master/Pr%C3%A1ctica-2/Capturas/mismo_modulo_priv_pub_ejer3.png)

## 4-5. Reutilizaremos el archivo binario input.bin de 1024 bits, todos ellos con valor 0, de la práctica anterior. Intentad cifrar input.bin con vuestras claves pública. Explicad el resultado.

En este caso para cifrar input.bin con nuestra clave pública obtenida, usamos “rsautl -pubin -encrypt”, pero obtenemos el siguiente error:

![curl](https://github.com/franfermi/Seguridad-Proteccion-Equipos-Informaticos_SPSI/blob/master/Pr%C3%A1ctica-2/Capturas/comando_ejer4-5.png)

El error que nos devuelve es debido a que el tamaño de la clave es menor al tamaño del archivo el cual se intenta cifrar.

## 6. Diseñad un cifrado híbrido, con RSA como criptosistema asimétrico. El modo de proceder sería el siguiente:

* El emisor debe seleccionar un sistema simétrico con su correspondiente modo de operación.

He utilizado aes-128-cbc.

* El emisor generará un archivo de texto, llamado por ejemplo sessionkey con dos líneas. La primera línea contendrá una cadena aleatoria hexadecimal cuya longitud sea la requerida por la clave. OpenSSL permite generar cadenas aleatorias con el comando openssl rand . La segunda línea contendrá la información del criptosistema simétrico seleccionado. Por ejemplo, si hemos decidido emplear el algoritmo Blow sh en modo ECB, la segunda línea deberá contener -bf-ecb.

Para generar la cadena aleatoria hexadecimal, usamos la opción “rand -hex” y especificamos 	el tamaño.

* El archivo sessionkey se cifrará con la clave pública del receptor.

Usamos la opción “rsautl -pubin -encrypt” para cifrar el archivo creado anteriormente con la 	clave pública obtenida en el ejercicio 3.

* El mensaje se cifrará utilizando el criptosistema simétrico, la clave se generará a partir del archivo anterior mediante la opción -pass file:sessionkey.

El mensaje lo cifraremos con el cifrado  aes-128-cbc que es el especificado en la segunda 	línea de sessionkey.txt.

En la siguiente captura se muestran los tres últimos comandos realizados:

![curl](https://github.com/franfermi/Seguridad-Proteccion-Equipos-Informaticos_SPSI/blob/master/Pr%C3%A1ctica-2/Capturas/comandos_ejer6.png)

## 7. Utilizando el criptosistema híbrido diseñado, cada uno debe cifrar el archivo input.bin con su clave pública para, a continuación, descifrarlo con la clave privada. comparad el resultado con el archivo original.

Primero desciframos el sessionkey cifrado con la clave pública, con la clave privada del receptor.
Introducimos la contraseña anteriormente asignada.

![curl](https://github.com/franfermi/Seguridad-Proteccion-Equipos-Informaticos_SPSI/blob/master/Pr%C3%A1ctica-2/Capturas/comando_ejer7.png)

De esta forma ya tenemos el sessionkey descifrado y el receptor podría ver su contenido y en especial el tipo de cifrado que se ha utilizado.

Y segundo, desciframos el mensaje que se encuentra cifrado con el método de cifrado del sessionkey, con dicho cifrado.

![curl](https://github.com/franfermi/Seguridad-Proteccion-Equipos-Informaticos_SPSI/blob/master/Pr%C3%A1ctica-2/Capturas/comando02_ejer7.png)

Por último, comprobamos que el contenido de input_descifrado.bin es el mismo que el original.

![curl](https://github.com/franfermi/Seguridad-Proteccion-Equipos-Informaticos_SPSI/blob/master/Pr%C3%A1ctica-2/Capturas/input_descifrado_ejer7.png)

## 8. Generad un archivo stdECparam.pem que contenga los parámetros públicos de una de las curvas elípticas contenidas en las transparencias de teoría. Si no lográis localizarlas haced el resto de la práctica con una curva cualquiera a vuestra elección de las disponibles en OpenSSL . Mostrad los valores.

Para generar el archivo usamos la opción “ecparam -name” y especificamos el nombre de la curva elíptica, en mi caso he elegido *secp192k1*.

![curl](https://github.com/franfermi/Seguridad-Proteccion-Equipos-Informaticos_SPSI/blob/master/Pr%C3%A1ctica-2/Capturas/comandos_ejer8.png)

![curl](https://github.com/franfermi/Seguridad-Proteccion-Equipos-Informaticos_SPSI/blob/master/Pr%C3%A1ctica-2/Capturas/par%C3%A1metros_ejer8.png)

En el fichero de salida se muestran los parámetros extraídos de la curva elíptica.

## 9. Generad cada uno de vosotros una clave para los parámetros anteriores. La clave se almacenará en nombreECkey.pem y no es necesario protegerla por contraseña.

Con “ecparam -genkey” generamos la clave a partir de los parámetros de la curva elíptica.

![curl](https://github.com/franfermi/Seguridad-Proteccion-Equipos-Informaticos_SPSI/blob/master/Pr%C3%A1ctica-2/Capturas/comandos_ejer9.png)

En el fichero de salida podemos observar la clave privada y pública que contiene y el tipo de curva elíptica seleccionada.

![curl](https://github.com/franfermi/Seguridad-Proteccion-Equipos-Informaticos_SPSI/blob/master/Pr%C3%A1ctica-2/Capturas/valores_ejer9.png)

## 10. “Extraed” la clave privada contenida en el archivo nombreECkey.pem a otro archivo que tenga por nombre nombreECpriv.pem . Este archivo deberá estar protegido por contraseña cifrándolo con 3DES . Mostrad sus valores.

Vamos a extraer la clave privada contenida en el archivo generado en el ejercicio anterior, cifrándolo con 3DES, para ello usamos la opción “ec -des3” e insertamos la contraseña.

![curl](https://github.com/franfermi/Seguridad-Proteccion-Equipos-Informaticos_SPSI/blob/master/Pr%C3%A1ctica-2/Capturas/comandos_ejer10.png)

En la siguiente imagen podemos observar que ambos archivos tienen la misma clave privada.

A la izquierda tenemos la clave generada por los parámetros de la curva y a la derecha la clave privada generada en este ejercicio.

![curl](https://github.com/franfermi/Seguridad-Proteccion-Equipos-Informaticos_SPSI/blob/master/Pr%C3%A1ctica-2/Capturas/valores_clavePriv_ejer10.png)

## 11. Extraed en nombreECpub.pem la clave pública contenida en el archivo nombreECkey.pem. Como antes nombreECpub.pem no debe estar cifrado ni protegido. Mostrad sus valores.

Por último para generar la clave pública a partir de la clave generada desde los parámetros, usamos la opción “ec -pubout” e indicamos el fichero de salida en el cual se almacenará la clave pública.

![curl](https://github.com/franfermi/Seguridad-Proteccion-Equipos-Informaticos_SPSI/blob/master/Pr%C3%A1ctica-2/Capturas/comandos_ejer11.png)

Los valores obtenidos en el fichero de clave pública son los siguientes:

![curl](https://github.com/franfermi/Seguridad-Proteccion-Equipos-Informaticos_SPSI/blob/master/Pr%C3%A1ctica-2/Capturas/valores_clavePub_ejer11.png)

Si comparamos la clave pública con la del fichero de clave por parámetros, observamos que es la misma.

![curl](https://github.com/franfermi/Seguridad-Proteccion-Equipos-Informaticos_SPSI/blob/master/Pr%C3%A1ctica-2/Capturas/valores_clavePub2_ejer11.png)
