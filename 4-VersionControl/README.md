<!--YAML HEADER
---
title : Introduccion a Git utilizando Github Desktop
part of : BITSS PUC-Chile
time : 3 hours
author: Garret Christensen
affiliation: UC Berkeley
---
-->

Taller de Git & GitHub Desktop
==============================
BITSS PUC-Chile 2017
------------------------------
Fernando Hoces de la Guardia

Gracias a [Garret Christensen](http://www.ocf.berkeley.edu/~garret) por proveer el material original para este entrenamiento.

Básicamente, estamos tratando de evitar una situación como esta:
![http://www.phdcomics.com/comics/archive/phd101212s.gif](http://www.phdcomics.com/comics/archive/phd101212s.gif)

Y acercarnos un poco a esto:

![Git xkcd comic](https://imgs.xkcd.com/comics/git.png)


### Contexto:

A un nivel fundamental, el problema es que rara vez creamos productos perfectos en el primer intento. Añadimos, borramos y revisamos constantemente. En el caso de tareas de procesar texto, como en el ejemplo de PhD Comics, las consecuencias son menores, como el tiempo que te toma en encontrar el archivo correcto, o la vergüenza de enviar la versión incorrecta a un colega.

Cuando trabajas con tus datos, sea en recolección, limpieza, transformaciones, o análisis, puede que ya trabajes de una forma que es auto-documentante. Esto ocurre cuando estas escribiendo código y no ocupando herramientas de 'point & click' (GUI  - Graphical User Interface). La ventaja de esto es que es reproducible, la desventaja es que si tienes la versión incorrecta toda linea de producción de tu estudio se estanca.

Una forma relativamente común de definir tu flujo de trabajo se puede encontrar [aqui](https://bids.github.io/2017-01-12-ucb/lessons/R/reproducible_workflow.html). Si hacen clases en pre-grado, miren el protocolo del [Project TIER](http://www.projecttier.org/).  

La meta aspiracional es que yo debería ser capaz de entrar en tu laboratorio en la noche, borrar todos tus archivos excepto tu código y datos originales, y tu deberías ser capaz de ejecutar un solo comando para regenerar TODO, incluyendo todos los resultados, tablas y figuras en su forma final. Esto es lo que se entiende por 'flujo de trabajo de un-click'.


En el otro extremo, cuando no puedes encontrar la versión correcta de tu procesacimento o análisis de datos, pierdes la habilidad de recrear cualquier resultado que fue generado en el pasado. Si tus resultados no son reproducibles, también adolecen de los siguientes problemas:

1. No son verificables
2. Son mas difíciles de explicar
3. No son extendibles


Por esta razón, necesitamos saber cual es la versión exacta que estamos utilizando y que ha cambiado con respecto a la versión previa. Hay muchas soluciones en este espacio. Algunos mantienen diferentes revisiones manualmente, separando todo en una serie de carpetas. Otros ocupan software que registra cada acción tomada (STATA o SPPS 'logs'). También hay quienes utilizan alguna función del tipo 'control de cambios' en su GUI (Graphical User Interface).


Todas estas soluciones adolecen del mismo problema, en tanto obligan al usuario a pensar que es una versión y como se deben manejar cambios a través de versiones. Por ejemplo si estas documentando tu flujo de trabajo en logs (SPSS o STATA) y quieres saber de donde salió ese resultado que generaste la semana pasada, tienes que manualmente buscar en el log de el día en cuestión, más todos los logs que potencialmente te pudieron llevado a generar ese resultado.

Git, or `git`, es un software que elimina ese problema. Es un programa de control de versiones que te ayuda, de manera muy precisa, a registrar *todos* los cambios en archivos de texto, con o sin colaboradores. Noten que `.txt, .do, .R, .md, .tex`, y muchos otros formatos son archivos de texto. Otros formatos como `.doc, .docx, .xls, .xlsx, .pdf, .dta` no son archivos de texto (`.csv` es complicado, pero la respuesta corta es no). De esta forma hay un alto valor en utilizar Git o Gihub en archivos con codigo (.do), pero no hay mucho valor en usarlo en archivos con datos (.dta). La mayor barrera para la adopción masiva de Git en la comunidad científica (publicado por primera vez en el 2005) es que no es particularmente intuitivo. Sus desventajas son:

1. Difícil de entender
2. Difícil de usar correctamente

Y sus ventajas son:

1. Nunca mas vas a borrar o perder un archivo de manera accidental.
2. Siempre vas a ser capaz de volver a la versión anterior en tu flujo de trabajo.
3. Fácil descubrir que ha cambiado (i.e. origen del problema), y cuando

Afortunadamente para nosotros, Github y otras compañías han creado aplicaciones que apuntan a proveer acceso a git de manera amigable para el usuario. Usuarios con mas experiencia usan Git en la linea de comandos (Terminal en Mac y Git Shell/Bash en Windows). Pero estas aplicaciones pueden llevar a cabo las principales funciones de Git, lo cual es suficiente para nuestras necesidades.

Puede que necesitemos utilizar la linea de comandos para hacer algunas cosas. [Aquí](http://swcarpentry.github.io/shell-novice/02-filedir/) hay algo de ayuda, y no dudes en preguntar.

### Antes de empezar:

* Asegurence de tener un editor de texto en su computador.
  * **Windows:** Notepad
  * **Mac:** Textedit -  cambien los defaults como se indica [aqui](http://www.iphonehacks.com/2017/06/plain-text-mode-textedit-mac.html). O instalen un editor.
Como [Atom](http://atom.io), Sublime o Notepad++ (el editor de do-files de Stata también funciona).

* Descargar e instalar el [GitHub Desktop app](http://desktop.github.com).

* [Crear](https://github.com/join?source=header-home) una cuenta en Github.com.

## Forking

Vamos a ocupar nuestra nueva cuenta de Github para hacer *fork* `fork`<sup>1</sup> de un respositorio -- el mismo repositorio en el cual fue creado este taller!

* Vayan a [https://github.com/fhoces/BITSS_PUC_CHILE_2017](https://github.com/fhoces/BITSS_PUC_CHILE_2017)

* Busquen el botón que dice 'fork' en la esquina superior derecha y hagan click

Este repositorio va a ser copiado a tu cuenta (pero **no** a tu computador), permitiendo modificarlo como lo desees. Dado que el 'fork' vive en los servidores de Github, cualquier cambio que se hagan a esos servidores ya van a estar respaldados para ti.

* Para evitar confusiones, cambien el nombre del repositorio a algo así como `GitTaller` en la seccione de settings.

### Clonando, Creando y Modificando
The options in the Github app under the "+" button are to add, create, or clone a repository. *Adding* is finding and telling the app that a repository is already on your computer. *Creating* creates a new repository. *Cloning* is copying an existing repository from your GitHub account.

To clone a public repository that doesn't belong to you, click the download button that is just to the left of the "Download ZIP" button on the repository's GitHub.com page, or drag and drop the URL from your browser into the open GitHub Desktop app (oddly, there is no way to type the URL directly into the app.)  

* Clone your fork of the workshop repository. Navigate to it on your computer to verify that it's there.

* What files are in there? Do you see anything you don't understand? If not, try this: [[Mac](http://www.macworld.co.uk/how-to/mac-software/how-show-hidden-files-in-mac-os-x-finder-funter-macos-sierra-3520878/)][[Windows](https://support.microsoft.com/en-us/help/14201/windows-show-hidden-files)]
If you do see the hidden files, *never ever ever* mess with them.

Now that you've successfully cloned a repository, we'll create our own.

* Create a new repository. Give it a name like `codepoetry_<yourname>` *What files are in it?*
* Create a text file called `README.md` using your text editor. Give the file three lines of text:

>Turning and turning in the widening gyre

> The falcon cannot hear the falconer;

> Things fall apart; the centre cannot hold;

* Save the file in `codepoetry_<yourname>`

What's different about Github Desktop?

* Click on the `README.md` file in Github Desktop.

Git keeps files in three areas. The workspace, the staging area, and the repository.
![SWC Git areas](https://swcarpentry.github.io/git-novice/fig/git-staging-area.svg)

Github Desktop automatically adds any file you change to the staging area. That's what the checkmark next to the file name means.

* Uncheck and recheck `README.md`.

* Commit, or permanently store, `README.md` by giving a concise but helpful message like `add README` in the Summary area then clicking on `Commit to master`.

* Create a second file called `regressions.do` using the Stata do file editor. Give it the lines:

`clear all`

`set more off`

`sysuse auto`

`reg price mpg`

* Save the .do file.

* Add a fourth line of text to `README.md` and save it.

> Mere anarchy is loosed upon the world,

* Uncheck `regressions.do` and commit *only* `README.md` with a message like `add line on anarchy`.

* Recheck `regressions.do` and commit it with a message like `add regressions.do`.

(We're using `add` to mean more than one thing here. Sorry.)

* Add a fifth line to `README.md`:
>The blood-dimmed tide is loosed, and everywhere

* Commit the change.
* Add a sixth line to `README.md`:
>The ceremony of innocence is drowned;

* Commit the change.


#### Undoing
There are several ways to undo things with git, not all of which are possible with Github Desktop. The GH methods are to:
1. Right click on the file on the file and Discard changes. *What areas is this dealing with? Note this is like `git reset filename` on the command line.*

2. Click on a change in the History section, and click on Revert.

3. Click on the settings gear and click Undo latest commit.

Yes, you can undo an undo. Just make sure when you are undoing changes that you are looking in your text editor at the most up to date version (close the file and reopen it.)

But what if you'd like to undo *all* the changes back to a certain point? [This is not possible in Github Desktop.](http://stackoverflow.com/questions/34790794/going-back-to-a-previous-commit-in-github-desktop) For that you have to use the command line.

* Revert the commit that added the fifth line to `README.md`.

* Revert the revert so you have the full six lines of `README.md` again.

We'll try one quick command in the command line. (See the SWC lesson [here](https://swcarpentry.github.io/git-novice/05-history/).)

* Open Git Shell (Windows) or Terminal (Mac).
* Navigate (using `cd`) to inside the folder that is the repository.
* Enter `git status` to make sure you're in your repository.
* Enter `git log` to see the record of your changes.
* Enter `git checkout <hash> <filename.txt>` where `<hash>` is the unique letter and number string refering to the place you want to jump back to and filename is the specific file.
* Verify that the file has changed back to the point you want.
* To get the latest version back, type `git checkout HEAD <filename.txt>` or `git checkout master` which will send you to the tip of the `master` branch. (I know, we haven't talked about branches yet! So let's do that now.)

Atlassian has a great [explanation](https://www.atlassian.com/git/tutorials/resetting-checking-out-and-reverting) of the differences between revert, reset, and checkout.  

### Branching:
Git uses branches to let you experiment on new ideas or bug fixes.

* Create, name, and sync a new `experimental` branch with the 'create new branch' button.
* Make changes to `regressions.do` making the regressions robust to heteroskedasticity, save, and commit them to `experimental`.
* Oh wait, no. Emergency, you have to go back to the main (master) branch.
* Change a different part of `regressions.do`. Add a line at the end:
`summ length`

* Merge the experimental branch into the master branch. In Github Desktop this is done by clicking on Update from. Make sure you're *in* Master and Update from experimental.

#### Conflicts
Between the experimental branch and the main branch, make and commit some conflicting changes (that is, changes to the same lines of the same file). Then try and merge. *What happens?*
* Change the regression line to read `reg price mpg weight` in master. Save and commit to master.
* Change the regression line to read `reg price mpg length, robust` in experimental. Save and commit to experimental.
* Try and merge.
* View the conflict (`<<<<<<<` `=======` and `>>>>>>>`), resolve the conflict by editing the weird part out of the file yourself, saving, and committing.

There's a conflict tutorial [here](https://bids.github.io/2017-01-12-ucb/lessons/git/).

### Publishing (pushing and pulling):

You can store stuff online at GitHub.com (or any server with Git installed), which will enable you to work on multiple computers.

Git frequently refers to `push`ing (sending) and `pull`ing (retreiving). Github Desktop simplifies this and just calls it "Sync".

To publish your repository on the web.
* Just click the Publish button.

Now we want to make sure that we can make changes online via GitHub.com, and then sync them to your computer (pulling).

* Go back and forth between making a local change, committing, and pushing it to the web, and making remote (online) changes (click the pencil button to edit, then commit at the bottom of the screen), being sure to sync between each commit. Eventually you'll screw up and not sync enough. (That is, change a file online and commit it. Don't sync. Make a contradictory change locally and commit it. Try and sync. *What happens?*)

<!--Aside: This tutorial is written in Markdown. If you want something *not* to render markdown, comment it out like this. Same as HTML.-->


### Collaborating:
Thus far we've been working solo. Now we'll collaborate. GitHub is built for this. Thousands of people contribute code to large open source coding projects without ever meeting in person. It's also great for just a few people to collaborate on simpler coding projects.

There are two ways to collaborate:

1. Make everyone you trust a collaborator. For small projects with trusted collaborators only.
2. Pull requests. For big projects--let anyone make suggestions (called pull requests) and the owner gets to choose whether to accept.

We'll probably only have time for #1.

1. Pair up with a neighbor. One of you be A and one be B for this exercise.
2. In the settings tab for A's repository on Github.com (that A published above), add B as a collaborator.
3. B accept the invitation, and clone A's repository so you have it on your own computer.
4. B make a change, commit, and sync (push) the change.
5. A sync (pull) B's changes, make your own changes, commit, and push.
6. After handing off back and forth successfully, make simultaneous conflicting changes. *How do you resolve the conflicts?*
7. Switch roles between A & B and repeat.

If we have time for Pull Request collaboration, or you have questions, we will follow Github's [guide](https://help.github.com/desktop/guides/).

### Additional Git Topics:

#### Pull Requests:
This is how you suggest changes to repositories to which you aren't a full fledged collaborator. Try this with a partner if you have time. Clone a repo you don't own, make a change, submit a pull request, and ask the owner to merge the pull request. Switch roles.

#### Command Line:
Many, if not most, experienced users will use Git via the command line. (Terminal on a Mac, the Git Shell that came with the Desktop app, Windows PowerShell, there are a lot of options. They're all where you type commands for your computer to execute.) You can read why [here](http://programmers.stackexchange.com/questions/173297/why-learn-git-when-there-are-gui-apps-for-github). Basically, it's more powerful.

There are a million and one online tutorials for Git in the command line. [Software Carpentry's](http://swcarpentry.github.io/git-novice/) is good, as is [Atlassian's](https://www.atlassian.com/git/tutorials/). The basic stuff is all nicely summarized [here](http://rogerdudler.github.io/git-guide/) in a single page.


**1.** For more on forking, see [https://help.github.com/articles/fork-a-repo/](https://help.github.com/articles/fork-a-repo/)
