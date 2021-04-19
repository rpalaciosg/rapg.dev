---
title: "commitizen y alias: mejora tus commits y productividad con git en la terminal"
description: "Mi Git Workflow en git y linux para mejorar la productividad al escribir commits usando la terminal"
date: 2021-01-29T03:34:10-05:00
draft: false
images: ['content/image/thumbnail_blog_post2_commitizen.png']
tags: ["git","conventional-commits","alias","git aliases","commitizen","terminal"]
categories: ["Terminal"]
toc: false
---

![](https://i.imgur.com/BM9is0G.jpg)

Hola, soy Richard y en este post, te explicaré mi flujo de trabajo al usar _Git_ desde la _terminal_, y lo necesario a configurar en tu espacio de trabajo para lograr mejorar tu productividad a la hora de usarlo en tu día a día.

Para mejorar tu productividad cuando usas _git_ desde la terminal, hay 2 cosas importantes que te pueden ayudar a conseguirlo: 

1. Trabaja en buenos _alias_ (_git_ y _linux_)
2. Usar _commitizen_ para asegurar una [convención](https://www.conventionalcommits.org/en/v1.0.0/) al momento de escribir _commits_.


>Te ha pasado, que estás en la zona/concentrado, terminas de corregir un error, o de crear una nueva funcionalidad, y te llega ese pequeño momento de frustración en el que no sabes exactamente qué escribir en tu mensaje de _commit_? (🤦‍♂️ o tal vez solo soy yo!!)

Es molesto sobre todo, cuando te equivocas y tienes que hacer un _--amend_ al darte cuenta de que no lo describiste bien y tener que repensarlo, buscar el último comando, escribir nuevamente el mensaje, etc., aún más si ya hiciste push!!.

Si esto te ha pasado, pienso que esta lectura te va a interesar.


<details>
 <summary><strong>Tabla de Contenidos</strong></summary>
 <ul>
<li><a href="#punto1">1. ¿Por qué tanta conmoción por un mensaje de commit?</a></li>
<li><a href="#punto2">2. ¿Por qué commitizen y no simplemente un cliente gráfico de Git?</a></li>
<li><a href="#punto3">3. Requisitos</a></li>
<li><a href="#punto4">4. Mi configuración de espacio de trabajo para Git</a></li>
<li><a href="#punto5">5. Linux ‘alias’ para acortar comandos</a></li>
<li><a href="#punto6">6. Configurando git aliases</a></li>
<ul><li><a href="#punto6.1">Listar tus git aliases configurados</a></li></ul>
<li><a href="#punto7">7. Usando nuestros “alias”</a></li>
<li><a href="#punto8">8. Usando commitizen para escribir buenos mensajes de commit</a></li>
    <ul>
        <li><a href="#punto8.1">Haciendo nuestro repositorio commitizen friendly</a></li>
        <li><a href="#punto8.2">Escribiendo un commit con Commitizen</a></li>
        <li><a href="#punto8.3">Formateando mi git log en una sola linea (git aliases)</a></li>
        <li><a href="#punto8.4">Formateando y detallando mi git log (git aliases)</a></li>
    </ul>
<li><a href="#punto9">9. Conclusion</a></li>
<li><a href="#punto10">10. Recursos</a></li>
 </ul>
</details>


<h2 id="punto1">1. ¿Por qué tanta conmoción por un mensaje de commit?</h2>

No solo es un mensaje de _commit_, es la historia y evolución de nuestro desarrollo.
Sí, **Git** es una herramienta esencial en nuestro flujo de trabajo como programadores. Pero igual de importante, es escribir correctamente nuestros mensajes de commit, mejor cuando seguimos una convención como [conventional commits](https://www.conventionalcommits.org/en/v1.0.0/).

Lo que queremos lograr con esto, es mantener un historial limpio y fácil de leer de los cambios(_logs_) de nuestro código, y convertirlo en una narrativa que solo al leerla, podamos descubrir y entender el proceso y evolución de nuestro software.

> The git log is a narrative of how development is progressing. Keep it clean.  
_Juan J. Merelo_


<h2 id="punto2">2. ¿Por qué commitizen y no simplemente un cliente gráfico de Git?</h2>
  

Es cierto y válido, actualmente existen herramientas gráficas que facilitan el trabajo, al  versionar tu código con _git_, y sobre todo al visualizar el historial de cambios que has realizado; pero aún no conozco alguno, que integre _linters_ de _commits_ como conventional commits. (_Si conoces alguno que sea open source por favor házmelo saber!!_)

Aparte de esto, la ventaja que obtendremos al usar _commitizen_ y _alias_ a través del terminal, en mi opinión, no tiene nada que envidiarle a una app gráfica, ! Bueno la _UI_ de _logs_ tal vez!; pero como dicen por ahí, “para gustos, colores!". Además, encontré una forma de arreglar esto con un _alias_, el que veremos más adelante.

Basta decir que por el gusto de usar la terminal, además de que, está buenísimo entender bien las bases de git y saber que comandos estás usando realmente; así no tener dificultades con alguna herramienta que te puedas encontrar en el futuro.

<h2 id="punto3">3. Requisitos</h2>

Por lo general, me gusta trabajar sobre linux, por eso para seguir este post y empezar tu configuración es necesario lo siguiente:

- Tener una máquina con _linux_ o [WSL](https://docs.microsoft.com/en-us/windows/wsl/about)  instalado, si estás en _windows 10_.
- Tener instalado [Git](https://git-scm.com/downloads)
- Tener instalado _npm_ y [Node.js](https://nodejs.org/en/)

_Ten en cuenta que sería bueno que ya conozcas las bases de git para entender o darle sentido a esta lectura, pero aun así, intentaré hacerlo fácil de seguir._

<h2 id="punto4">4. Mi configuración de espacio de trabajo para Git</h2>

Como ya te debes imaginar, mi configuración al rededor de Git son alias de linux, git aliases y commitizen.

- **Linux Alias** → se usan para encapsular la ejecución de un conjunto de comandos, en un solo comando abreviado en la terminal, dicho de otra formas, son abreviaciones de nuestros comandos que se configuran en tu sistema linux, en este caso 'git', Ejm:

    ```bash
    # Comando largo
    git commit -m 'mensaje commit'

    #Comando abreviado
    gc 'mensaje commit'
    ```
- **Git aliases** → esta es una característica de Git parecida a la de linux alias, ayuda a simplificar en abreviaciones mas cortas la ejecución de los comandos de git.Ejm:

    ```shell
    $ git config --global alias.co checkout
    $ git config --global alias.br branch
    $ git config --global alias.ci commit
    $ git config --global alias.st status
    ```

- **Commitizen** → [Commitizen](https://github.com/commitizen/cz-cli) nos permite escribir mensajes de commits de forma guiada y rapida a travez de CLI o yo podria decirle TUI.

    Commitizen es un *cli* "command line interface tool" que nos ayuda a escribir mesajes de commits mas amigables siguiendo un estandar de convenciones y buenas practicas, con la ayuda de linters y herramientas que puedes configurar.

Puedes encontrar mi configuración de linux alias y git aliases aquí:

[![My dotfiles](https://github-readme-stats.vercel.app/api/pin/?username=rpalaciosg&repo=dotfiles&show_owner=true?theme=bear)](https://github.com/rpalaciosg/dotfiles)


<h2 id="punto5">5. Linux 'alias' para acortar comandos</h2>

Por lo general al usar la terminal, escribes un comando o combinación de comandos, por ejemplo `git` o `ls`. Aveces es un poco molesto cuando tienes que repetir muchas veces el mismo comando  (y eso que este es uno de los cortos),  entonces es aquí donde puedes usar un alias. 

En este caso configuro un alias `g` para el comando git .

- En sistemas unix donde solemos usar zsh o bash, etc; configuramos un alias de esta forma → alias g='<comando>'.

Ahora abrimos nuestro archivo de configuracion del shell que uses ya `~/.bashrc` de bash o  `~/.zshrc`  de zshell (es el que uso) y agregamos esta linea alias g=git al final del archivo o en la sección #alias si esta ya existe . 

| ![Mi archivo ~/.zshrc](https://i.imgur.com/cyNnGqN.png)| 
|:--:| 
| *Mi archivo [~/.zshrc](https://github.com/rpalaciosg/dotfiles/blob/master/.zshrc)* |

Ahora si nos dirigimos a nuestra terminal, en el directorio de uno de nuestros repositorios de git, podemos usar git, reemplazando el comando `git` por `g`, Ejm:

|![](https://i.imgur.com/GI0UdSg.png)|
|:--:|
|Imagen del terminal ejecutando comando `git status`|

En la imagen anterior vemos que no tenemos diferencia en el resultado al escribir el comando `git status` o `g status` debido a que a la configuración del alias harán lo mismo _"mostrar el estado del repositorio"_.

**Bien logramos acortar el comando git, pero como acortamos las opciones o argumentos que van el comando git?**

Esto lo podemos hacer creando un alias con el comando y los argumentos que necesitemos, un ejemplo `alias gst=git status`, asi al escribir `gst` en nuestra terminal obtendremos la salida del comando git status. **Pruebalo!!**

En el caso de que uses [Zsh](https://www.zsh.org/), existen alias ya pre-configurados para tu comodidad. Esto lo consigues instalado un framework para zsh  llamado [Oh-My-Zsh](https://ohmyz.sh/), y activando su plugin de [Git Ohmyzsh](https://github.com/ohmyzsh/ohmyzsh/tree/master/plugins/git) existente en el framework. 

En la siguiente imagen puedes ver los alias pre-configurados en el plugin _git_ de _oh-my-zsh_.

|![](https://i.imgur.com/SC4K6lO.png)|
|:--:|
|[Oh-My-Zsh Git Aliases](https://jasonm23.github.io/oh-my-git-aliases.html)|

Aunque estos alias son muy útiles, siempre toma un tiempo aprenderlos, incluso no llegas a usarlos todos. Por eso te recomiendo que estos alias los tengas de referencia para crear los tuyos y asi irles aprendiendo durante la marcha según los necesites, como yo lo hice.


<h2 id="punto6">6. Configurando git aliases</h2>

Algo que percibí, es que al usar `linux alias` para comandos git, me limitaban a poder usarlos solo en ambientes linux, y debido a que aveces suelo usar git en windows;   
Basándome en los alias que tiene el plugin Git de oh-my-zsh, decidí configurar esos alias dentro de mi configuración de git como aliases. 
Ademas con el objetivo de aprenderlos, me obligue a crear solo los que necesitaba y usara de forma repetida, ya luego iría agregando nuevos según los necesite.

Para crear un alias en git, puedes usar un comando como este: 

```shell
git config --global alias.[alias_comando] [comando_git]
```

`alias.[alias_comando] [comando_git]` le dice a git que agregue esta abreviación para un comando especifico en la sección [alias] del archivo  de configuración de git `.gitconfig`. 

Esto lo hará ya sea de forma _local_ o _global_,  en este caso el argumento `—global` nos dice que queremos que sea global, es decir que este disponible para todos los repositorios en nuestro sistema. Pero si lo quitamos este sera configurado localmente en un solo repositorio.  

Por ejemplo crearemos el git aliases del comando _status_, escribiendo lo siguiente en nuestro terminal:

```shell
#global
git config --global alias.st status

#local
git config alias.st status
```

Estas lineas nos dice que la abreviación al comando `status` ahora sera `st`

El archivo `.gitconfig` lo podemos encontrar en las siguientes ubicaciones:
- Si la instalación que se realizo fue para uso global de todos los usuarios, estará:
    - Windows: 'C:\Users\<username>\.gitconfig
    - Linux/Ubuntu: ~home\<username>\.gitconfig
- Si lo queremos hacer solo para un repositorio o de forma local, cada repositorio git tiene una carpeta `.git` que suele estar oculta, al ingresar a esta carpeta puedes encontrar el archivo de configuración `.gitconfig`.

Si deseamos configurar varios _alias_ a la vez, abrimos el fichero `.gitconfig`  ya sea _global_ o _local_ y bajo la sección [alias]  empezamos a crear o editar nuestros alias para comandos de git.

|![](https://i.imgur.com/6kwG6Am.png)|
|:--:|
|Mi archivo [~/.gitconfig](https://github.com/rpalaciosg/dotfiles/blob/master/.gitconfig)

De esta forma puedes crear los alias que mas te gusten.  Lo mas recomendable es que crees los que uses mas a menudo y según tus necesidades, ya queda al alcance de tu imaginación.


<h3 id="punto6.1">Listar tus git aliases configurados</h3>

Puedes tener un _alias_, que te muestre un listado de todos tus _alias_ configurados, para crearlo escribe la siguiente línea en tu _terminal_:

```shell
git config --global alias.alias "! git config --get-regexp ^alias\. | sed -e s/^alias\.// -e s/\ /\ =\ /"
```

Luego para probarlo, escribe `git alias` en tu _terminal_ y veras como se listan todos los _git aliases_ que configuraste:

|![](https://i.imgur.com/4qdwBs5.png)|
|:--:|
|Creando un _alias_ para listar `git aliases`|


<h2 id="punto7">7. Usando nuestros "alias"</h2>

Para probar los nuevos _alias_ configurados, crearemos un nuevo repositorio. Entonces, dentro de un nuevo directorio con el nombre que prefieras, abrimos un terminal y ejecutamos el comando `g init` o `git init` para inicializar el repositorio. _como puedes ver usamos el linux alias `g`_

|![](https://i.imgur.com/GbHpFLz.png)|
|:--:|
|Usando _alias_ `g` para el comando `git`|

Ahora podemos crear archivos dentro del repositorio, y para añadirlos al _staging area_ con un `git add <archivo>` o en nuestro caso el comando abreviado `g add README.md`.

|![](https://i.imgur.com/4hCnKYH.png)|
|:--:|
| Usando _alias_ `g add`|

Si hacemos un `g st` o `git status`, nos damos cuenta que los archivos están listos para ser _"commiteados/versionados"_ o registrados en el _log_ del repositorio. _como puedes ver ahora usamos la combinación de linux alias y git aliases_

|![](https://i.imgur.com/Ou3rgvw.png)|
|:--:|
|Usando alias `g status`|


<h2 id="punto8">8. Usando commitizen para escribir buenos mensajes de commit</h2>

Para hacer commit de tus cambios, escribes `git commit`, o si usamos nuestros alias configurados escribiríamos `g commit` o `g c`, al hacerlo se abrirá un editor donde describirás tu mensaje _commit_.

Pero, esto podría ser un poco molesto, si existe una herramienta llamada [commitizen](https://github.com/commitizen/cz-cli), que mejora la experiencia al escribir _commits_ y de paso le añade convenciones de buenas prácticas.

Al usar [commitizen](https://github.com/commitizen/cz-cli) a través de su _CLI_, en lugar de escribir el comando `git commit` podemos usar el comando `cz` y solo escribiendo en nuestro terminal `git cz`, `g cz` o simplemente `cz`, _commitizen_ reconocerá este comando y lanzara una pequeña _app cli_, que de manera interactiva, nos guiará para completar y escribir nuestro mensaje de commit. Podemos ver un ejemplo en la imagen siguiente.

|![](https://i.imgur.com/pbVqOgj.png)|
|:--:|
|Usando [commitizen](https://github.com/commitizen/cz-cli) a traves del comando `cz`|


<h3 id="punto8.1">Haciendo nuestro repositorio commitizen friendly</h3>

Antes de poder usar las ventajas de  [commitizen](https://github.com/commitizen/cz-cli), debemos configurar nuestro repositorio y hacerlo Commitizen friendly como lo llaman los creadores. Esto lo hacemos escribiendo lo siguiente en nuestro terminal:

1. Instalamos el paquete npm esc`npm install -g commitizen` , 
2. Inicializamos un proyecto npm escribiendo `npm init`
3. Configuramos nuestro repositorio para usar `cz-conventional-changelog` adapter, escribiendo:
    ```shell
    commitizen init cz-conventional-changelog --save-dev --save-exact
    ```
    _Esto agregara en el archivo package.json a commitizen como una dependencia de desarrollo._


<h3 id="punto8.2">Escribiendo un commit con Commitizen</h3>

Ahora estamos listos para hacer un commit usando commitizen. 

Hacemos algún cambio en nuestro repositorio, agregamos dicho cambio con `git add` y luego escribimos `g cz` todo desde nuestra terminal.


1. Aparecerá un cli interactivo, que primero nos pedirá elegir el tipo de cambio que estamos realizando ya sea una nueva característica, cambio en documentación, corrección de errores, etc; tal como lo dicta la convención de [conventional-commits](https://www.conventionalcommits.org/en/v1.0.0/) en este caso al estar inicializando el repositorio osea es el primer commit, escogemos `feat` de feature.

|![](https://i.imgur.com/UFNYYlW.png)|
|:--:|
|Usando `g cz`|


2. Especificamos el scope del cambio, aqui escribiremos `*` u `all` ya que es la inicializacion de todo el repositorio.

|![](https://i.imgur.com/3f3maef.png)|
|:--:|
|Escogiendo `scope` del cambio en commitizen`|



3. Seguido a esto nos pide ingresar un mensaje corto para el commit, donde escribiremos _commit inicial_. 
Seguidamente nos pide agregar una descripción mas detallada para el commit, en este caso la podemos dejar en blanco.

|![](https://i.imgur.com/1dnYt3z.png)|
|:--:|
|Describiendo el `commit` con `commitizen`|


4. Luego nos pregunta si hay breaking changes o cambios importantes, en este caso escribimos `No` o `N`.
También nos pregunta si este cambio afecta algún issue o problema abierto donde podemos describirlo, en este caso escribimos `No`.

|![](https://i.imgur.com/s89JycV.png)|
|:--:|
|Especificando _breaking changes_ e _issues_ como parte del commit|

Al final se creara el commit con un mensaje que usa  un formato con convenciones y buenas practicas `feat(*): commit inicial` , y esto con ayuda de `commitizen`.


<h3 id="punto8.3">Formateando mi git log en una sola linea (git aliases)</h3>

Si queremos ver como quedo nuestro mensaje commit, podemos escribir `git log` o `g l` si tenemos configurado un alias, para poder ver el historial de cambios de nuestro repositorio.

|![](https://i.imgur.com/pxr4DtV.png)|
|:--:|
|Resultado de `git log` con formato`|


Te puede parecer curioso que el resultado de haber hecho `git log` en tu equipo no es igual al de la imagen anterior; para que tu git log este formateado en una sola linea y con colores, puedes crear y usar el alias para git pegando en tu terminal el comando a continuación. 

```shell
git config --global alias.l "log --pretty=format:'%Cgreen%h %Creset%cd %Cblue[%cn] %Creset%s%C(yellow)%d%C(reset)' --graph --date=relative --decorate --all"
```

Entonces para usarlo debes escribir `g l` y tendrás un resultado parecido.

En internet encuentras mucha información, sobre modelos y colores del formato en el que se muestra tu git log, su forma de personalizar es muy flexible y con muchas alternativas según tu Sistema Operativo.


<h3 id="punto8.4">Formateando y detallando mi git log (git aliases)</h3>

Tengo configurado un alias diferente también para el comando git log, pero que muestra mas a detalle los archivos ue fueron modificados en cada commit, para eso escribe el siguiente comando en tu terminal:

```shell
git config --global alias.ll "log --graph --name-status --pretty=format:'%C(red)%h %C(reset)(%cd) %C(green)%an %Creset%s %C(yellow)%d%Creset' --date=relative"
```

Entonces si ejecuto `g ll` o `git ll`, obtengo lo siguiente (este es el log de otro repositorio para fines demostrativos):

|![](https://i.imgur.com/eAdEQ13.png)|
|:--:|
|Resultado del alias `g ll` o `git ll`|


<h2 id="punto9">9. Conclusion</h2>

Puedes estar pensando, que tal vez no vale la pena instalar y depender de una librería solo para escribir un commit. Pero como en todo, eso depende:

- de tus necesidades
- de si quieras escribir buenos commits siguiendo una convención.
- ya conoces de memoria la convención Conventional-commits y no necesitas una herramienta
- usas tu propia convención con emojis en tus mensajes de commits
- etc..

Pueden ser muchos puntos de vista, y puede ser que no estes de acuerdo con el mio.

Todo lo compartido en esta lectura, bien o mal, es simplemente mi experiencia, mi gusto y la forma en que a mi me ha funcionado.

Ten por seguro que existen muchas mas formas de hacerlo, e incluso puede que sean mejores;  al final el objetivo de todo este proceso, es poner en evidencia la `importancia de tener una buena narrativa de tu historial de cambios en tu repositorio`, y esto lo logras escribiendo buenos mensajes de commit desde el principio. 

Mi recomendación, es que empieces a usar commitizen en repositorios en los que trabajes de forma individual y siempre al iniciar el repositorio. Si lo vas a usar en un repositorio de equipo, es mejor que el equipo se ponga de acuerdo y dejen claro que se usara una convención y linter de commits, esto les dará muchas ventajas a futuro y menos desacuerdos.

Bueno, eso es todo,  **Muchas gracias por llegar hasta el final!! ✌**, espero haya sido de tu interés, y de ayuda. 


Te invito a que pruebes [commitizen](https://github.com/commitizen/cz-cli) y que configures tus propios alias, ademas de que juegues con el formato de resultado de algunos comandos. 


Eres libre de revisar [mis Dotfiles](https://github.com/rpalaciosg/dotfiles) y darme tu opinion, tengo algunas cosas nuevas que descubrí y que estoy probando.

<strong>Si tienes alguna duda o feedback sobre este contenido no dudes en hacérmelo saber.</strong>
   <ul>
    <li><a href='apalaciosg91@gmail.com'>📧 apalaciosg91@gmail.com</a></li>
    <li><a href='https://github.com/rpalaciosg'>👨🏽‍💻GitHub: rpalaciosg</a></li>
    <li><a href='https://twitter.com/rpalaciosg_'>🐦Twitter: rpalaciosg_</a></li>
    <li><a href='https://www.linkedin.com/in/richardpalaciosgarcia/'>💼LinkedIn: richardpalaciosgarcia</a></li>
   </ul>


<h2 id="punto10">10. Recursos</h2>

- [https://git.wiki.kernel.org/index.php/Aliases#Use_graphviz_for_display](https://git.wiki.kernel.org/index.php/Aliases#Use_graphviz_for_display)
- [https://jasonm23.github.io/oh-my-git-aliases.html](https://jasonm23.github.io/oh-my-git-aliases.html)
- [https://github.com/craftzdog/dotfiles-public](https://github.com/craftzdog/dotfiles-public)
- [https://unsplash.com/photos/91AQt9p4Mo8](https://unsplash.com/photos/91AQt9p4Mo8)
- [https://www.conventionalcommits.org/en/v1.0.0/](https://www.conventionalcommits.org/en/v1.0.0/)
- [https://github.com/commitizen-tools/commitizen](https://github.com/commitizen-tools/commitizen)
- Imágenes almacenadas en [imgur](imgur.com) a traves de [https://hackmd.io/](https://hackmd.io/)