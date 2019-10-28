---
title: "Mi sitio web personal con Hugo y Netlify"
date: 2019-10-27T18:32:46-05:00
author: "Richard Palacios G."
draft: true
toc: false
images:
series:
- Hugo framework
tags: ["Portfolio","Hugo", "Website"]
categories: ["Hugo"]
---

Desde hace algún tiempo he estado enfocándo mi tiempo a aprender más sobre Desarrollo web, y mejorar mis skills como programador.

A pesar de mis esfuerzos por crear un sitio desde cero, y no estar satisfecho con el flujo de trabajo y publicación. Descubrí los generadores de sitios estáticos como [Jekyll](https://jekyllrb.com/), [Lektor](https://www.getlektor.com/), [Hugo](https://gohugo.io/), [nikola](https://getnikola.com/), [ghost](https://ghost.org/) y todos estos tienen la posibilidad de publicarse y desplegarse de forma gratuita mediante [GitHubPages](https://pages.github.com/) incluso sin la necesidad de adquirir un nombre de dominio pagado en primera instancia.

Al inicio probe con `Jekyll` hice fork a un tema que me gustó por su diseño; hice modificaciones que incluso aún puedes ver en [rpalacios.github.io](https://rpalaciosg.github.io/).

El inconveniente con este sitio, es la dificultad de poder probarlo en mi entorno de desarrollo local, esto debido a la forma en que su creador lo había implementado y también sumaba *la falta de conocimiento de mi parte*.  . 
Esto implicaba que para probar los cambios y modificaciones que hiciera en el sitio debía hacerlo directamente en `producción`. 

A pesar de este inconveniente fue muy emocionante para mí tener este sitio ya que a más de ser gratis, y no sentír la necesidad de adquirir un domínio pagado, también me ayudo mucho aprender sobre el flujo de trabajo con git, GitHub, e incluso me ayudó a cumplir con los Pull Request necesarios para tener mi camiseta del [Hactoberfest de 2018](https://twitter.com/rpalaciosg_/status/1090100149714591744).

Después de tener un tiempo con esta experiencia, decidí crear un sitio web nuevo pero que cumpliera las siguientes condiciones:

- Debía ser con un framework generador de sitios estáticos basado en lenguajes conocidos para mí, como Python, o Javascript. 
- Debía ser un tema sencillo,  y responsive.
- El front debía tener un estilo parecido o intentar simular una terminal.

Con esas condiciones o ideas en mente, empecé mi búsqueda y vaya que rápido encontré, dí con este tema [hello-friend-ng](https://themes.gohugo.io/hugo-theme-hello-friend-ng/) queme gustó mucho, del generador de sitios estáticos [Hugo](https://gohugo.io/). 

Al principio quise no tomarlo en cuenta ya que no cumplía una de las condiciones anteriores que es, que el sistema este basado en lenguajes conocidos para mí como Python o Javascript pero `Hugo` está basado [Go](https://golang.org/), lenguaje que he escuchado pero que conozco. 

Aún con ese miedo, el hecho de gustarme su diseño decidí probarlo.

<img src="https://d33wubrfki0l68.cloudfront.net/30790d6888bd8af863fb2b5c33a7f337cdbda243/4e867/images/hugo-logo-wide.svg" alt="logo hugo" position="centstyle="border-radius: 8px; width: 50%; height: 50%;"/>

No pasó mucho tiempo en cuanto a mi elección pero debo decir que hasta ahora estoy encantado. Y no solo por que me gustase el tema, sino por la facilidad, velocidad de implementar un sitio usando este tema [hello-friend-ng](https://themes.gohugo.io/hugo-theme-hello-friend-ng/).

- Además la documentación de `Hugo` me parece muy completa, y tuve la suficiente guía para abordar y resolver ciertos problemas que se me presentaron en el camino.
- Y otra cosa que en mi caso resulto positiva es que el ambiente de `Go` en `Hugo` me resulta más fácil que el uso de Ruby en Jekyll.

Ya entre toda esta secuencia de ventajas, descubrí que no solo `GitHubPages` podia desplegar mi sitio gratuitamente sino también [NetLify](https://www.netlify.com/) y sobre todo me daba una guía de como hacerlo incluso con integración continua, es decir, cuando haga un `PR` al código que está en el repo de Github, `netlify` lo detecta y empezará automáticamente un proceso de construcción y despliegue del sitio con los cambios agregados.

Entonces todos los cambios que se apliquen al repo, se verán reflejados automáticamente en el sitio.

El proceso para ponerlo en vivo fue el siguiente:

  - Los fuentes están alojados en mi [repo público](https://github.com/rpalaciosg/rpalaciosg) en `github`.
  - El contenido compilado o generado está en Netlify el cual detecta los cambios en la rama `master` para implementarlo y desplegarlo.
  - Además estoy usando un nombre de dominio personalizado (https://richardpalaciosg.dev).


1. Hacer un fork del repositorio del tema a usar [hugo-theme-hello-friend-ng](https://github.com/rhazdon/hugo-theme-hello-friend-ng). 

![fork repo del tema](/../../resources/site_img.png)

Esto porque los temas de hugo en los sitios que se despliegan en `netlify` deben estar como submodulo de git, y además en el futuro poder hacer modificaciones propias.

