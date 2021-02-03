---
title: "Commitizen y alias: Git Workflow para productividad en tu terminal"
date: 2021-01-29T03:34:10-05:00
draft: true
toc: true
images:
tags: ["git","conventional-commits","alias","commitizen","terminal"]
categories: ["Terminal"]
---

> Se que has pasado el tedioso momento de tener que pensar que escribir en tu mensaje commit, o tener que hacer un--amend  por que te diste cuenta que no lo describiste bien y sobre todo tienes que volver escribir ese comando nuevamente.

Hola, soy Richard.

En este post explicare mi flujo de trabajo con **Git**, y como configurar tu terminal para mejorar tu productividad a la hora de usarlo en la terminal.

 
Actualmente, **Git** es una herramienta esencial en nuestro flujo de trabajo como programadores, ya sea durante el desarrollo de proyectos o durante nuestro aprendizaje.

Ademas es muy importante, no solo por buenas practicas sino porque nos ayudara a versionar y manejar nuestra base de código y conocimiento de una forma mas adecuada y ordenada la cual agradeceremos desde el primer momento.

<br>

### Por que no simplemente usar un cliente gráfico de Git?

Es cierto actualmente existen herramientas gráficas que te facilitan el trabajo al versionar tu código con git, y sobre todo al visualizar el historial de cambios que has realizado, aunque también suelen tener algunos puntos en contra que a mi parecer no me terminan de convencer; como pagos de licencia, limite de repositorios a manejar, sin son repositorios de github deben ser públicos;  para mi  aunque estas herramientas te dan vistosos beneficios, estas cosas las que no me han permitido hacer completamente el cambio . 

En fin,  basta decir que por el gusto de usar la terminal, no esta de mas entender bien las bases de git y saber que comandos estas usando realmente; asi no tener dificultades con alguna herramienta que te puedas encontrar en el futuro.

<br>

## Prerequisitos

- Tener instalado [Git]([https://git-scm.com/downloads](https://git-scm.com/downloads))
- Tener instalado npm y [Node.js]([https://nodejs.org/en/](https://nodejs.org/en/))

Ten en cuenta que seria bueno que ya conozcas *las bases de git para entender o darle sentido a esta lectura, pero aun asi, intentare hacerlo fácil de seguir..*

<br>

## Mi configuracion de Git

- **Alias** → para entradas o ejecucion rapida de comandos en el terminal, estos son abreviaciones de nuestros comandos que se configuran en tu sistema en este caso 'git', Ejm:

    ```bash
    # Comando largo
    git commit -m 'mensaje commit'

    #Comando abreviado
    gc 'mensaje commit'
    ```

    [rpalaciosg](https://github.com/rpalaciosg)
    [![custom title](image)](https://github.com/rpalaciosg)

    <a href="https://github.com/rpalaciosg" target="_top">mi github</a>