---
title: "Resumen: Códigos de Estado HTTP"
date: 2022-11-01T23:43:25-05:00
draft: false
toc: false
images:
tags: ["http", "http codes", "http status code", "rest api"]
categories: ["http", "buenas practicas", "api", "rest api"]
---

|                                                                                                          ![Imagen del código de estado http 401](https://unsplash.com/photos/PrkG7QC8V_0)                                                                                                          |
| :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------: |
| _Photo by <a href="https://unsplash.com/@suicide_chewbacca?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Ashwini Chaudhary(Monty)</a> on <a href="https://unsplash.com/s/photos/http-codes?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Unsplash</a>_ |

El buen diseño de una `REST API` depende mucho de conocer los principales códigos de estado `HTTP`, el saber como y cuando usarlos pondrá en evidencia la experiencia que tenemos como desarrolladores al crear API's.

A continuación describo un breve resumen general de los códigos `HTTP` mas comunes:

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

** Algunos de los códigos `HTTP` mas usados:**

## En el rango _100_

> Por revisar

## En el rango _200_

- _200_: OK
- _201_: CREATED
- _202_: ACCEPTED
- _204_: NO CONTENT

## En el rango _300_

- _301_: MOVED PERMANENTLY
- _303_: SEE OTHER
- _307_: TEMPORARY REDIRECT

## En el rango _400_

- _401 y 403_: UNAUTHORIZED AND FORBIDDEN ERRORS
- _404_: NOT FOUND

## En el rango _500_

En este rango, existen muchos códigos de estados, pero el mas importante es el **500**.

- _500_: INTERNAL SERVER ERROR

Los errores 500 indican errores en el servidor, tales como una excepción, una conexión dañada o un error en la base de datos, etc.

## Conclusiones y Recomendaciones

Debemos tener en cuenta que como desarrolladores, a pesar de saber el error exacto, es buena practica responder con el código de estado especifico, **PERO desde el punto de vista de la _Seguridad_**; es mejor ser vago en el código de estado que respondemos y mostrar un código de estado mas genérico, por ejemplo: error _500_ o _404_.

Nunca debemos detallar o especificar el código de error o estado HTTP, ya que por motivos de seguridad, evitaremos que hackers indaguen en los códigos de respuesta HTTP y sepan las debilidades que pueda tener nuestro sistema.

## Referencias

Obtenido del libro Express in Action, y de un tweet de [@stevelosh](https://twitter.com/stevelosh/status/372740571749572610).
