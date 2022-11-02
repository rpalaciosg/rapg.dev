---
title: "Idempotencia en verbos http"
description: "Una descripción breve sobre la famosa idempotencia y su importancia en el los verbos http"
date: 2022-10-17T01:14:21-05:00
images:
tags:
  [
    "http",
    "idempotencia",
    "verbos http",
    "verbos idempotentes",
    "verbos http idempotentes",
    "verbos no idempotentes",
    "apis rest",
  ]
categories: ["http", "buenas practicas"]
toc: false
---

Según Wikipedia el significado de la palabra `idempotencia` es la propiedad de realizar una acción determinada varias veces y aun asi conseguir el mismo resultado que se obtendría si se realizara una sola vez.

En el caso de http, mas específicamente en los Verbos HTTP, la idempotencia nos dice que la ejecución repetida de una petición con los mismo parámetros sobre un mismo recurso tendrá el mismo efecto en el estado de nuestro recurso de un sistema si se ejecuta 1 o N veces. Es decir siempre se tiene el mismo resultado.

Debemos tener en cuenta que existen verbos HTTP no idempotentes, pero es una buena practica respetar este principio de idempotencia para evitar efectos secundarios o no deseados.

La ejecución repetida usando un verbo no idempotente con los mismos datos sobre un recurso no tendrá el mismo efecto.

**Ejemplo verbo No idempotente:**

Tenemos un api la cual tiene como recurso una base de datos, si hacemos una petición http POST el cual es un verbo no `idempotente` para crear un post, al ejecutar la siguiente petición con la misma información, tendremos como efecto que en cada ejecución se creara un recurso nuevo dentro de la base de datos, con los mismos valores pasados en el cuerpo de la petición.

`POST /api/v1/posts`

```json
{
  "description": "post51",
  "tipo": "blog"
}
```

Ahora veremos un ejemplo con el comportamiento de un verbo idempotente.

**Ejemplo verbo idempotente:**

En este caso vamos a usar el verbo http `PUT`, realizaremos una petición de creación/actualización sobre un recurso especifico de la base de datos con determinados paramentos que son los datos enviados en el cuerpo anterior.

Esta petición creara un nuevo recurso en caso de no existir, o lo modificara en caso de que haya cambiado algo en el existente.

`PUT /api/v1/posts/51`

```json
{
  "description": "post51",
  "tipo": "blog"
}
```

Si ejecutamos esta petición por primera vez, creara el nuevo recurso `posts/51` en caso de no existir.

Si repetimos y ejecutas la misma petición N veces, con el verbo idempotente `PUT` enviando los mismo parámetros al mismo recurso `/51`, este se actualizara y se mantendrá igual, es decir tendremos el mismo estado.

Si ejecutamos la petición cambiando algo por ejemplo el recurso `/52`, el efecto que tendrá sera crear un nuevo recurso

Es muy importante tener en cuenta que este comportamiento no solo se produce simplemente por usar un verbo idempotente, es necesario implementar y respetar este principio.

Aquí vemos los Verbos HTTP que son idempotentes:

| Verbo HTTP | Idempotente |
| ---------- | ----------- |
| GET        | Si          |
| POST       | No          |
| PUT        | Si          |
| DELETE     | Si          |

> En desarrollo
