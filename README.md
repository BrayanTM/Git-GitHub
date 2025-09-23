<img width="auto" height="75" alt="image" src="https://git-scm.com/images/logos/downloads/Git-Logo-2Color.png" /> <img width="auto" height="100" alt="image" src="https://gist.github.com/user-attachments/assets/c6f202c0-1e7c-4712-8e21-f441be1fa18"/>
# Comandos de Git
[Documentación Oficial de Git](https://git-scm.com/docs)
## Verificación de Git
`git --version`
Indica la versión instalada de git.

`git help`
Muestra la yuda de git.

`git help <comando>`
Muestra el manual del comando indicado.

***
***
## Configuración de Usuario en Git
`git config --global user.name "<nombre de usuario>"`
Con este comando configuramos el nombre de nuestro usuario en git.

`git config --global user.email "<correo>"`
Asignamos el correo que se usará para git, normalmente es el correo que usamos en GitHub pero puede ser cualquier otro.

`git config --global -e`
Verificamos los datos de usuario que introducimos.
***
***
## Inicializar un Respositorio
`git config --global init.defaultBranch <name>`
Indicamos a git cual será el nombre por defecto de nuestra rama principal al iniciar un nuevo repositorio, git de manera predeterminada nombra la rama principal como "master" pero se recomienda cambiar a "main".

`git init`
Inicializa el repositorio local.

`git status`
Muestra información sobre el repositorio, por ejemplo: nombre de la rama, commits realizados, estado de los archivos, entre otros.

`git add <nombre del archivo>`
Inicializamos el seguimiento a un archivo.

`git add .`
Hace seguimiento de todos los archivos modificados y lo sprepara para confirmar.

`git reset <nombre del archivo>`
Elimina un archivo del seguimiento.

`git commit -m "Firts Commit"`
Hace un commit sobre los archivos que agregamos al seguimiento, `-m` indica que el commit llevará un mensaje, es importante que el mensaje sea claro y que haga referencia a lo que hemos agreagado ya que así será más facil de identificar. Un commit es como hacer una captura de los archvos, los guarda tal cual el estado en que se agregaron. Es similar a hacer un punto de restauración en el tiempo.

`git checkout -- .`
Restablece el repositorio al último commit.
***
### Cambiar el nombre de una rama
`git branch`
Muestra la rama en la que nos encontramos.

`git branch -m <nombre de la rama> <nuevo nombre>`
Cambia el nombre de una rama.
***
`git commit -am "msg"`
Confima los cambios realizados en los archivo sin necesidad de hacer antes `add`, esto solo funciona para los archivos que ya tienen seguimiento, para archivos que no tiene seguimiento es necesario hacer antes el `add`.

`git log`
Nos permite ver los logs dentro de nuestro repositorio. Ejemplo:
```
	commit a13992ae1a61c2b5f6cfe1fc021403320b0bf2d2 (HEAD -> main) 
	Author: <nombre de usuario> <correo>
	Date:   Mon Aug 11 16:56:33 2025 -0600

			Readme Updated
```
- La primer línea hacer referencia al hash de nuestro commit, es un identificador único.
- La segundo hace referencia al autor del commit.
- La tercer línea indica la fecha exacta en que se realizó el commit.
- La última línea indica el nombre del commit.

***
### Diferentes formas de agregar archivos al escenario

`git add *.html`
Este comando añade al seguimiento todos los archivos .html que se encuentren en mi repositorio. `*` es un comodín de git.

`git add js/*.js`
Agrega todos los archivos .js que se encuentran en la carpeta js.

*Las carpetas que no tienen ningún archivo no se agregan automáticamente a git, git por defecto omite las carpetas vacías. Para solucionar esto debemos crear un archivo `.gitkeep` dentro del directorio vacío para que git lo reconozca.*

`git add <nombre del directorio>`
Git añade todos los archivos y directorios de la carpeta que indiquemos. Ej: `git add css/` añade todos los archivos y directorios de la carpeta css.

***
### Alias para comandos
`git status --short`
Este comando permite ver el status del repositorio de manera resumida.

`git config --global alias.s "status --short"`
Este comando crea un alias para el comando `status --short` y los asigna a `s`, etnonces en vez de escribir `git status --short` podemos simplemente introducri `git s` y será el mismo resultado.

*Podemos editar el alias desde la configuración de git con: `git config --global -e`*

`git config --global alias.lg "log --graph --abbrev-commit --decorate --format=format:'%C(bold blue)%h%C(reset) - %C(bold green)(%ar)%C(reset) %C(white)%s%C(reset) %C(dim white)- %an%C(reset)%C(bold yellow)%d%C(reset)' --all"`
Este es un alias para el comando `log` donde también se le indican diferentes parámetros y además los colores que presentará para cada parte del log.
***
### Cambios en los archivos
`git diff`
Muestra los cambios realizados luego de un commit en un archivo mediante la consola.

`git diff --staged` 
Muestra los cambios de los archivos que ya estan agredados al stage.
***
### Actualizar mensaje del commit y revertir commits

`git commit --amend`
Este comando permite modificar un commit.

`git commit --amend -m "<mensaje nuevo>"`
Este comando nos permite modificar el mensaje del ultimo commit realizado desde la terminal.

`git reset --soft HEAD^`
Este comando revierte el ultimo commit realizado, modificando el comando `HEAD^x` sustituyendo la x por un valor numerico podemos revertir commits anteriores al ultimo, por ejemplo `HEAD^2` revertira el commit anterior al ultimo realizado.
***
***
## Viajes en el tiempo, resets y reflog
`git reset --soft <hash del commit>`
Este commit nos permite regresar al comit indicado revirtiendo los commits posteriores a este, sin perder ningun cambio realizado gracias al comando `--soft`.
`git reset` tiene 3 parametros:
- `--soft`: este argumento permite revertir un commit sin descartar los cambios realizados en los archivos y manteniendolos en el stage
- `mixed`: este argumento revierte los commits sin eliminar los cambios pero eliminando del stage a los archivos afectados.
- `hard`: este argumento revierte los commits realizados y elimina los cambios realizados en los arcvhicos, a la vez que los elimina del stage.

`git reflog`
Este comando nos permite ver el historial de cambios en nuestro repositorio, es util cuando hemos revertido un commit y deseamos regresar a el ya que nos indica el hash de cada commit realizado a lo largo del tiempo.

`git resert --hard <hash del commit al que deseamos volver>`
Este comando nos permite regresar a un commit en la linea del tiempo, anque lo hayamos eliminado.
***
### Ignorando Archivos que no Deseamos
`.gitignore`
Creando un archivo con este nombre podemos incluir dentro de el el nombre de las carpetas o archivos que deseemos excluir del seguimiento de git.
***
***
## Ramas, Uniones y Conflictos
`git branch <nombre de la rama>`
Este comando nos permite crear una nueva rama.

`git checkout <nombre de la rama>`
Este comando nos permite cambiar de rama.

`git checkout -b <nombre de la rama>`
Este comando también nos permite crear una nueva rama y a la vez movernos a esa rama luego de creada, esta es la forma más comun de crear una rama.

`git merge <nombre de la rama>`
Este comando permite fusionar los cambios entre dos ramas, ej. si realizamos cambios en la rama `dev` y los queremos llevar a la rama `main` debemos estar dentro de la rama `main` para llamar a los cambios de `dev`.

`git branch -d <nombre de la rama>`
Con este comando podemos borrar una rama, se recomienda borrar una rama solo cuando ya no la necesitemos.
***
### Merge: fast-forward

*fast-forward sucede cuando la rama destino no tiene commits nuevos desde que se creo la rama de trabajo. Git simplemente "avanza el puntero" de la rama destino al último commit de la rama que estás uniendo. No crea commits extra.*
***
### Merge: unión automática

*union automática sucede cuando las dos ramas han avanzado, pero los cambio no se pisan. Git puede combinar ambos historiales y crea un commit de merge automáticamente.*
***
### Merge: unión con conflictos

*unión con conflictos sucede cuando los dos han modificado la misma línea de un archivo o la misma parte del proyecto. Git no puede decidir cuál versión es la correcta -> marca un conflicto. Se debe abrir el archivo, resolverlo manualmente, hacer `git add` y luego `git commit` para terminar el merge.*
***
***
## Tags - Etiquetas
`git tag <nombre>`
Este comando permite crear tags (etiquetas) sobre los commits.

`git tag`
Lista todos los tags que existan.

`git tag -d <nombre>`
Elimina un tag en específico.
***
### Versionamiento Semántico

`git tag -a <version> -m <mensaje>`
Este comando permite crear un tag anotado con un mensaje.

*El versionamiento es muy recomendado para poder llevar un control claro de los cambios en nuestra aplicación. Ej. v1.0.0 el primer dígito representa una version estable o actualización mayor, el segundo indica que se agrego una nueva característica o funcionalidad y el tercero indica que se corrigio algún bug*

`git tag -a <version> <hash> -m <mensaje>`
Con este comando podemos crear tags a commits específicos.

`git show <tag>`
Muestra la información específica de un tag.
***
***
## Git Stash y Git Rebase
### Stash
[Documentación de Git Stash](https://git-scm.com/docs/git-stash)

`git stash`
Agrega todos lo cambios realizados despues del ultimo commit al stash y los elimina de la rama.

`git stash list`
Muestra la lista de stash creados, junto con su identificador hash.

`git stash pop`
Regresa todos los cambios del ultimo stash a la rama y elimina el stash al que pertenecian.

`git stash clear`
Elimina todos los stash.

`git stash apply <stash>`
Trae los cambios del stash seleccionado a la rama.

`git stash drop <stash>`
Elimina el stash indicado.

`git stash show <stash>`
Muestra los archivos y filas modificadas en el stash.

`git stash list --stat`
Muestra los cambios de todos los stash.

`git stash save "<desc>"`
Permite guardar un stash con una descripción.

***
### Rebase

`git rebase <rama>`
Llama los cambio de una rama a otra, fusionando las ramas en una sola linea de tiempo, esta funcion a diferencia del `merge` no crea un nuevo commit si no que fusiona las ramas.

`git rebase -i HEAD~x`
Este comando permite interactuar con commits, `x` indica la cantidad de commit que deseamos afectar.

- `squash` permite fusionar dos o más ramas.
- `reword` permite cambiar el nombre de uno o mas commits.
- `edit` permite modificar todo el estado de uno o mas commit, cambiar el nombre, separar commits, renombrar commits, etc. Esta modificaciones es muy delicada asi que se debe tener cuidado.

***
***
## GitHub
### Agregar un Repositorio Remoto
`git remote add origin <url>`
Este comando permite añadir un origen remoto a nuestro repositorio local de git.

`git remote -v`
Lista los repositorios remotos agregados.
***
### Subir un Repositorio Local a GitHub

`git push -u origin <rama>`
Este comando sirve para enviar los archivos de nuestro repositorio local al repositorio remoto, `<rama>` indica el nombre de la rama a la cual vamos a hacer el push de nuestros archivos, `-u` indica que por defecto todos los demas push que hagamos apuntaran a la rama indicada.

`git push --tags`
Este comando permite enviar los tags al repositorio remoto.

`git push --set-upstream origin <rama>`
Utilizamos este comando para subir una nueva rama al repositorio remoto.

***
### Traer Cambios de un Repositorio Remoto al Local

`git pull -u origin <rama>`
Este comando trae los cambios de nuestro repositorio remoto al local, `<rama>` indica la rama de donde traeremos los cambios `-u` establece como predeterminada esa rama para todos los pulls.

`git pull`
Es identico al anterior con la diferencia que este se usa cuando ya se establecio la rama predeterminada.

#### Configuracion Local Recomendada
`git config --global pull.ff only`
Indica a git que usara fast-forward de manera predeterminada para todos los pull.

`git config --global pull.rebase true`
Indica a git que en caso de tener conflictos al traer los cambios remotos al local permite hacer un rebase, lo que nos inicia un rebase interactivo para solucionar los conflictos.

***
### Clonar un Repositorio

`git clone <url>`
Clona el repositorio remoto a una carpeta local, por defecto clona todo el contenido de la rama main.
***
`git fetch`
Este comando trae los cambios del repositorio remoto (commits, tagas...) pero no los fusiona a la rama local.
***
***
## Actualizar un Fork

`git remote add upstream <url del origen del fork>`
Este coamndo permite agregar el repositorio original del cual hemos hecho el fork.

`git pull upsteam <rama>`
Trae todos los cambios del repositorio original a nuestra rama local del fork.

***
***
## Eliminar Ramas Remotas

`git branch -a`
Permite ver todas las ramas existentes, tanto locales com las que ha traido del repositorio remoto.

`git push origin :<rama>`
Este comando permite elimar una rama que se encuentra tanto en el repositorio local como en el remoto, si la rama se encuentra unicamente en el repositorio local no funcionara.

`git remote prune origin`
Elimina todas las ramas basura, por ejemplo las ramas que quedaron de manera local luego de un `pull` y que ya no se encuentran en el repositorio remoto.

***
***
## Cerrar un Issue desde la terminal

`git commit -am "Fixes #<no. issue><mensaje>"`
Con este comando realizamos el commit respectivo de los cambios solicitados en nuestro issue y ademas podemos cerrarlo inmediatamente.

***
***
## Crear Una Clave SSH para GitHub
1. Ingresar a la ruta `/user/mi_usuario`
2. Crear un directorioi llamado `.ssh`
	1.  `mkdir .ssh`
	2. Ingresar al directorio `.ssh` -> `cd .ssh`
	3. Ingresar el siguiente comando para generar la clave:
		1. `ssh-keygen -t rsa -C "correo@gmail.com"`
3.  Una vez creada la clave la podemos subir a GitHub
