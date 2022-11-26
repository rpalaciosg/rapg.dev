---
title: "Resumen: Códigos de Estado HTTP"
date: 2022-11-01T23:43:25-05:00
toc: false
images:
tags: ["http", "http codes", "http status code", "rest api"]
categories: ["http", "buenas practicas", "api", "rest api"]
---

|                                                                                                          ![Imagen del código de estado http 401](https://i.imgur.com/IMB3Pex.jpg)                                                                                                           |
| :-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------: |
| _Image based on Photo by [Ashwini Chaudhary(Monty)](https://unsplash.com/@suicide_chewbacca?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/http-codes?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)_ |

El buen diseño de una `REST API` depende mucho de conocer los principales códigos de estado `HTTP`, y el saber como/cuando usarlos; revela nuestra experiencia como desarrollador.

Para ayudar a dominar los códigos de estado al crear API's; dejo este resumen de los códigos HTTP mas usados o mas comunes:

Existen 5 familias o grupos de códigos de estados HTTP:

1. 1XX -> Información
2. 2XX -> Petición correcta
3. 3XX -> Redirection
4. 4XX -> Error de cliente
5. 5XX -> Error de servidor.

Hay un tweet de [@stevelosh](https://twitter.com/stevelosh/status/372740571749572610). que define de manera graciosa el objetivo de cada rango o familia de codigos **HTTP**.

**English:**

| HTTP Status Code | HTTP Description       |
| :--------------: | :--------------------- |
|       100        | hold on                |
|       200        | here you go            |
|       300        | go away                |
|       400        | you messed up (client) |
|       500        | I messed up (server)   |

**Spanish:**

| Código de Estado HTTP | Descripción del Código        |
| :-------------------: | :---------------------------- |
|          100          | espera                        |
|          200          | aquí tienes                   |
|          300          | vete                          |
|          400          | tu lo has hecho mal (cliente) |
|          500          | yo lo he hecho mal (server)   |

**Algunos de los códigos `HTTP` mas usados:**

## En el rango _100_

- _100_: Es un código muy raro en http, y se puede encontrar al usar websocket. Los websockets usan el código 100 para intercambiar cierta información de protocolo que sirve para establecer la conexión.

## En el rango _200_

- _200_: OK
- _201_: CREATED, devuelve una cabecera `location`, que es una URL de donde se puede consultar el nuevo recurso, creado.
- _202_: ACCEPTED, Encolado en caso de usar colas servicios o workers, también devuelve una cabecera `location` que es una URL de donde se puede consultar el recurso.
- _204_: NO CONTENT, es como si el servidor te dijera, "te entendí pero no voy a decir nada".

## En el rango _300_

- _301_: MOVED PERMANENTLY, es usado para redirección a largo plazo, el navegador guarda en cache la redirección. Ejm: Cuando la pagina cambio de nombre.
- _302_: ENCONTRADO Y REDIRECCIÓN TEMPORAL, redirecciona a otro lugar. Ejm: Redirección en proceso de login.
- _303_: SEE OTHER
- _304_: NOT MODIFIED, se usa cuando el servidor web implementa un tipo de cache.
- _307_: TEMPORARY REDIRECT
- _308_: PERMANENT REDIRECT

> Los códigos 307 y 308 funcionan como 302 y 301 respectivamente (Redirección temporal y permanente), pero debemos recordar que si los métodos usados en la request de la URL son POST, PUT o DELETE y los códigos a usar/retornar son 301 o 302, los métodos se se cambiaran por GET. Tener muy en cuenta esto por que podría dar errores.
>
> - 301 y 302, cambia el método de la request por GET.
> - 307 y 308, mantienen el método enviado en la request(POST, PUT, DELETE).

## En el rango _400_

Se usan cuando el error ha sido provocado por algo que hizo el cliente, Ejm: Se envió mal una petición/request, no se envió un parámetro obligatorio/requerido, o hacer request a una URL que no existe.

- _400_: BAD REQUEST.
- _401 y 403_: UNAUTHORIZED AND FORBIDDEN ERRORS
- _404_: NOT FOUND
- _410_: GONE, `ya no existe` o `se ha ido`, **Nuevo** Ejm: Cuando se publica un tweet polémico y decides borrarlo; y cuando alguien con el URL quiere volver a ver el tweet, podría devolver 410, porque ha sido eliminado y ya no existe.
- _422_: UNPROCESSABLE ENTITY, en caso de que lso parámetros pasados sean inválidos. Ejm: no se envía parámetro correcto u obligatorio en el request.
- _451_: UNAVAILABLE FOR LEGAL REASONS.

## En el rango _500_

En este rango, existen muchos códigos de estados, pero el mas importante es el **500**. Se usando ha habido un error interno en el servidor, tales como una excepción, una conexión dañada o un error en la base de datos, puede darse el caso que nuestro servidor este consultando por detrás a otro servidor y este le este respondiendo a tiempo, etc.

- _500_: INTERNAL SERVER ERROR.
- _502_: BAD GATEWAY.
- _503_: SERVICE UNAVAILABLE.
- _504_: GATEWAY TIMEOUT, el servidor esta tardando mucho en responder.

## Conclusiones y Recomendaciones

Debemos tener en cuenta que como desarrolladores, a pesar de saber el error exacto que podríamos usar o retornar, y aunque sea buena practica responder con el código de estado especifico; debemos tomar muy en cuenta **el punto de vista de la Seguridad**. Seria mejor ser vago/no especifico con el código de estado que retornemos y mostrar un código mas genérico, Ejm: error _500_ o _404_.

Esto con el simple motivo de salvaguardar la seguridad de la app, y evitar que hackers o personas mal intencionadas indaguen en los códigos de respuesta HTTP y facilitandoles encontrar debilidades que pueda tener nuestro sistema.

Podemos ver mas a detalle los códigos de estado HTTP en los siguientes sitios:

- https://httpstatuses.org/
- https://http.cat/
- https://http.dog/
- https://www.restapitutorial.com/httpstatuscodes.html

## Referencias

Obtenido del libro Express in Action, y de un tweet de [@stevelosh](https://twitter.com/stevelosh/status/372740571749572610) y de la explicación en el canal de [makigas.es](https://www.youtube.com/@makigas).
