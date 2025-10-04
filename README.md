# Guía de Comandos de Git y Configuración con GitHub

Esta guía presenta los comandos más importantes de **Git** y configuraciones relacionadas con **GitHub**, con descripciones claras y ejemplos prácticos.

---

## 📑 Índice

1. [Verificación de Git](#verificación-de-git)
2. [Configuración de Usuario](#configuración-de-usuario-en-git)
3. [Inicializar un Repositorio Local](#inicializar-un-repositorio-local)
4. [Gestión de Archivos y Commits](#cambios-en-los-archivos-y-commits)
5. [Alias de Comandos](#alias-para-comandos)
6. [Viajes en el Tiempo (Reset y Reflog)](#viajes-en-el-tiempo-reset-y-reflog)
7. [Ramas y Uniones](#ramas-uniones-y-conflictos)
8. [Tags y Versionado](#tags-y-versionado)
9. [Stash y Rebase](#git-stash-y-git-rebase)
10. [Repositorios Remotos en GitHub](#configuración-y-uso-de-github)
11. [Forks y Upstream](#forks)
12. [Eliminar Ramas Remotas](#eliminar-ramas-remotas)
13. [Issues desde la Terminal](#cerrar-un-issue-desde-la-terminal)
14. [Claves SSH](#crear-una-clave-ssh-para-github)

--- 

<img width="200" height="100" alt="image" src="https://git-scm.com/images/logos/downloads/Git-Logo-2Color.png"/> &emsp; <img width="275" height="100" alt="image" src="https://wallpapers.com/images/featured/github-logo-png-s8wb6yxlatsyp8s1.jpg"/>

[Documentación Oficial de Git](https://git-scm.com/docs)

## Verificación de Git
---

Verificar la versión instalada de git.
```bash
git --version
```

Ver la ayuda general de Git.
```bash
git help
``` 

Ver el manual de un comando específico.
```bash
git help <comando>
```

## Configuración de Usuario en Git
---

Configurar el nombre de usuario global.
```bash
git config --global user.name "<nombre de usuario>"
```

Configurar el correo asociado al usuario.
```bash
git config --global user.email "<correo>"
```

Abre la configuración global en el editor por defecto.
```bash
git config --global -e
```

## Inicializar un Repositorio Local
---

Indicamos a git cual será el nombre por defecto de nuestra rama principal al iniciar un nuevo repositorio, git de manera predeterminada nombra la rama principal como `master` pero se recomienda cambiar a `main`.
```bash
git config --global init.defaultBranch <name>
```

Inicializa el repositorio local.
```bash
git init
```

Mostrar información sobre el repositorio, por ejemplo: nombre de la rama, commits realizados, estado de los archivos, entre otros.
```bash
git status
```

Inicializar el seguimiento a un archivo.
```bash
git add <nombre del archivo>
```

Hacer seguimiento de todos los archivos modificados y lo prepararlos para confirmar.
```bash
git add .
```

Eliminar un archivo del seguimiento.
```bash
git reset <nombre del archivo>
```

Un commit es como hacer una captura de los archvos, los guarda tal cual el estado en que se agregaron. Es similar a hacer un punto de restauración en el tiempo sobre los archivos que se agregaron al seguimiento, `-m` indica que el commit llevará un mensaje, es importante que el mensaje sea claro y que haga referencia a lo que hemos agreagado ya que así será más facil de identificar. 
```bash
git commit -m "Firts Commit"
```

Restablecer el repositorio al último commit.
```bash
git checkout -- .
```

Confimar los cambios realizados en los archivo sin necesidad de hacer antes `add`, esto solo funciona para los archivos que ya tienen seguimiento, para archivos que no tiene seguimiento es necesario hacer antes el `add`.
```bash
git commit -am "msg"
```

Ver los logs dentro de nuestro repositorio. 
```bash
git log
```
Ejemplo:
```bash
	commit a13992ae1a61c2b5f6cfe1fc021403320b0bf2d2 (HEAD -> main) 
	Author: <nombre de usuario> <correo>
	Date:   Mon Aug 11 16:56:33 2025 -0600

			Readme Updated
```

- La primer línea hacer referencia al hash de nuestro commit, es un identificador único.
- La segundo hace referencia al autor del commit.
- La tercer línea indica la fecha exacta en que se realizó el commit.
- La última línea indica el nombre del commit.

### Diferentes formas de agregar archivos al escenario

El siguiente comando añade al seguimiento todos los archivos .html que se encuentren en el repositorio. `*` es un comodín de git.
```bash
git add *.html
```

Agregar todos los archivos .js que se encuentran en la carpeta js.
```bash
git add js/*.js
```

> [!IMPORTANT]
> *Las carpetas que no tienen ningún archivo **no** se agregan automáticamente a git, git por defecto omite las carpetas vacías. Para solucionar esto debemos crear un archivo `.gitkeep` dentro del directorio vacío para que git lo reconozca.*

Git añade todos los archivos y directorios de la carpeta que indiquemos. Ej: `git add css/` añade todos los archivos y directorios de la carpeta css.
```bash
git add <nombre del directorio>
```

## Cambios en los archivos y Commits
---

Mostrar los cambios realizados en un archivo que se modifico luego de hacer un commit.
```bash
git diff
```

Mostrar los cambios de los archivos que ya estan agredados al stage.
```bash
git diff --staged
``` 

### Actualizar mensaje del commit y revertir commits

Modificar un commit.
```bash
git commit --amend
```

El siguiente comando nos permite modificar el mensaje del último commit realizado.
```bash
git commit --amend -m "<mensaje nuevo>"
```

Este comando revierte el ultimo commit realizado.
```
git reset --soft HEAD^
```

> [!TIP]
> Modificando el comando `HEAD^x` sustituyendo la x por un valor numerico podemos revertir commits anteriores al ultimo, por ejemplo `HEAD^2` revertira el commit anterior al ultimo realizado.

### Ignorando Archivos que no Deseamos

Creando un archivo con el siguiente nombre podemos incluir dentro de este el nombre de las carpetas o archivos que deseemos excluir del seguimiento de git.
```bash
.gitignore
```

## Alias para comandos
---
Ver el status del repositorio de manera resumida.
```bash
git status -sb
```

El siguiente comando crea un alias para el comando `status -sb` y los asigna a `s`, etnonces en lugar de escribir `git status -sb` podemos simplemente escribir `git s` y será el mismo resultado.
```bash
git config --global alias.s "status -sb"
```

> [!TIP]
> *Podemos editar el alias desde la configuración de git con: `git config --global -e`*

Este es un alias para el comando `log` donde se le indican distintos parámetros, además se indican los colores que presentará para cada parte del log.
``` bash
git config --global alias.lg "log --graph --abbrev-commit --decorate --format=format:'%C(bold blue)%h%C(reset) - %C(bold green)(%ar)%C(reset) %C(white)%s%C(reset) %C(dim white)- %an%C(reset)%C(bold yellow)%d%C(reset)' --all"
```

## Viajes en el Tiempo: Reset y Reflog
---

Este comando nos permite regresar a un commit en específico, revierte los commits posteriores sin perder ningun cambio realizado gracias al parámetro `--soft`.  
```bash
git reset --soft <hash>
```

> [!TIP]
> 
> `git reset` tiene 3 parámetros:
> 
>	- `--soft`: este parámetro permite revertir un commit sin descartar los cambios realizados en los archivos y manteniendolos en el stage
>	- `mixed`: este parámetro revierte los commits sin eliminar los cambios pero eliminando del stage a los archivos afectados.
>	- `hard`: este parámetro revierte los commits realizados y elimina los cambios realizados en los arcvhicos, a la vez que los elimina del stage.

El siguiente comando nos permite ver el historial de cambios en nuestro repositorio, es util cuando hemos revertido un commit y deseamos regresar a el ya que nos indica el hash de cada commit realizado a lo largo del tiempo.
```bash
git reflog
```

El siguiente comando nos permite regresar a un commit en la linea del tiempo, anque lo hayamos eliminado.
```bash
git resert --hard <hash>
```

## Ramas, Uniones y Conflictos
---

Crear una nueva rama.
```bash
git branch <nombre de la rama>
```

Cambiar de rama.
```bash
git checkout <nombre de la rama>
```

Crear una nueva rama y  movernos a la nueva rama creada.
```bash
git checkout -b <nombre de la rama>
```

> [!NOTE]
> Esta es la forma más común de crear una rama.

### Cambiar el nombre de una rama

Mostrar la rama en la que nos encontramos.
```bash
git branch
```

Cambiar el nombre de una rama.
```bash
git branch -m <nombre de la rama> <nuevo nombre>
```

### Uniones

Fusionar los cambios entre dos ramas.
```bash
git merge <nombre de la rama>
```

> Ej. si realizamos cambios en la rama `dev` y los queremos llevar a la rama `main` debemos estar dentro de la rama `main` para llamar a los cambios de `dev`.

Con el siguiente comando podemos borrar una rama, se recomienda borrar una rama solo cuando ya no la necesitemos.
```bash
git branch -d <nombre de la rama>
```

> [!IMPORTANT]
> ## Existen 3 Tipos de Merge
>
> ### Merge: fast-forward
>
> *fast-forward sucede cuando la rama destino no tiene commits nuevos desde que se creo la rama de trabajo. Git simplemente "avanza el puntero" de la rama destino al último commit de la rama que estás uniendo. No crea commits extra.*
> 
>### Merge: unión automática
>
> *union automática sucede cuando las dos ramas han avanzado, pero los cambio no se pisan. Git puede combinar ambos historiales y crea un commit de merge automáticamente.*
> 
> ### Merge: unión con conflictos
> 
> *unión con conflictos sucede cuando los dos han modificado la misma línea de un archivo o la misma parte del proyecto. Git no puede decidir cuál versión es la correcta -> marca un conflicto. Se debe abrir el archivo, resolverlo manualmente, hacer `git add` y luego `git commit` para terminar el merge.*

## Tags y Versionado
---

Crear tags (etiquetas) sobre los commits.
```bash
git tag <nombre>
```

Listar todos los tags que existen.
```bash
git tag
```

Eliminar un tag en específico.
```bash
git tag -d <nombre>
```

### Versionamiento Semántico

Crear un tag anotado.
```bash
git tag -a <version> -m <mensaje>
```

> [!TIP]
> 
> *El versionamiento es muy recomendado para poder llevar un control claro de los cambios en nuestra aplicación. Ej. v1.0.0 el primer dígito representa una version estable o actualización mayor, el segundo indica que se agrego una nueva característica o funcionalidad y el tercero indica que se corrigio algún bug*

Crear tags sobre commits específicos.
```bash
git tag -a <version> <hash> -m <mensaje>
```

Mostrar la información específica de un tag.
```bash
git show <tag>
```

## Git Stash y Git Rebase
---

### Stash

> [!NOTE]
>**¿Qué es un Stash?**
>Un stash en Git es un área temporal y local donde puedes guardar de forma segura los cambios no confirmados en tu código (tanto preparados como no preparados) para poder limpiar tu directorio de trabajo y trabajar en otra cosa.

[Documentación de Git Stash](https://git-scm.com/docs/git-stash)

Agrega los cambios realizados al stash.
```bash
git stash
```

Mostrar la lista de stash creados junto a su identificador (`hash`).
```bash
git stash list
```

Devolver todos los los archivos stash a la rama y eliminar el stash al que pertenecian.
```bash
git stash pop
```

Eliminar todos los stash.
```bash
git stash clear
```

Traer los archivos de un stash en específico.
```bash
git stash apply <stash>
```

Eliminar un stash en específico.
```bash
git stash drop <stash>
```

Mostrar los archivos y filas modificadas en el stash.
```bash
git stash show <stash>
```

Mostrar los cambios de todos los stash.
```bash
git stash list --stat
```

Guardar un stash con una descripción.
```bash
git stash save "<desc>"
```

> [!WARNING]
> No se recomienta trabajar com más de dos stash a la vez, la acumulación de estos puede generar confusión y desorden.

### Rebase

Fusionar dos ramas.
```bash
git rebase <rama>
```

> [!NOTE]
> Esta funcion a diferencia del `merge` no crea un nuevo commit si no que,  fusiona ambas ramas en la misma linea de tiempo.

El siguiente comando permite crear un rebase interactivo, `x` indica la cantidad de commit's que deseamos afectar.
`git rebase -i HEAD~x`

> [!IMPORTANT]
> 
>  Existen 3 tipos de parametros dentro del rebase interactivo:
> - `squash` fusiona dos o más ramas.
> - `reword` cambia el nombre de uno o mas commits.
> - `edit` permite modificar todo el estado de uno o mas commit, cambiar el nombre, separar commits, renombrar commits, etc. Esta modificacion es muy delicada asi que se debe tener cuidado.

## Configuración y uso de GitHub
---

Agregar un repositorio remoto.
```bash
git remote add origin <url>
```

Listar los repositorios remotos.
```bash
git remote -v
```

Subir un repositorio local a `GitHub`
```bash
git push -u origin <rama>
```

> [!NOTE]
> `git push` enviar los archivos de nuestro repositorio local al repositorio remoto, `<rama>` indica el nombre de la rama a la cual vamos a hacer el push de nuestros archivos, `-u` establece la rama por defecto para todos los demas push que hagamos.

Subir tags.
```bash
git push --tags
```

Subir una nueva rama al repositorio remoto.
```bash
git push --set-upstream origin <rama>
```

Traer los ambios de un repositorio remoto al local.
```bash
git pull -u origin <rama>
```

> [!TIP]
> #### Configuracion Local Recomendada
>
> Indicar a git que usara fast-forward de manera predeterminada para todos los pull.
> ```bash
> git config --global pull.ff only
> ```
>
> Indicar a git que en caso de tener conflictos al traer los cambios remotos al local permite hacer un rebase, lo que nos inicia un rebase interactivo para solucionar los conflictos.
> ```bash
> git config --global pull.rebase true
> ```


Clonar un repositorio
```bash
git clone <url>
```

El siguiente comando trae los cambios del repositorio remoto (commits, tags, etc...) pero no los fusiona a la rama local.
```
git fetch
```

## Forks
---

> [!NOTE]
> **Fork** es simplemente una copia del repositorio donde puedes escribir, haciendo públicos tus propios cambios, como una manera abierta de participación

Agregar un fork.
```bash
git remote add upstream <url del origen del fork>
```

Traer todos los cambios del repositorio original a nuestra rama local del fork.
```bash
git pull upsteam <rama>
```


> **Upsteam** se refiere al repositorio principal del que se extrae una bifurcación. Al bifurcar un repositorio, se crea una copia del repositorio original (upstream) en tu perfil de GitHub o en otro espacio de nombres, lo que permite realizar cambios sin afectar el código base original.

## Eliminar Ramas Remotas
---

Ver todas las ramas existentes, tanto locales com las que ha traido del repositorio remoto.
```bash
git branch -a
```

Elimar una rama que se encuentra en el repositorio local como en el remoto.
```bash
git push origin :<rama>
```

> [!NOTE]
> Si la rama se encuentra unicamente en el repositorio local no funcionara.

Eliminar todas las ramas basura, por ejemplo, las ramas que quedaron de manera local luego de un `pull` y que ya no se encuentran en el repositorio remoto.
```bash
git remote prune origin
```

## Cerrar un Issue desde la terminal
---

> [!NOTE]
> Un Issue es una nota en un repositorio que trata de llamar la atención sobre un problema. Puede ser un error a corregir, una petición para añadir una nueva opción o característica, una pregunta para aclarar algún tema que no está correctamente aclarado o muchas otras cosas diferentes.

Con el siguiente comando realizamos el commit respectivo de los cambios solicitados en nuestro issue y ademas podemos cerrarlo inmediatamente.
```bash
git commit -am "Fixes #<no. issue><mensaje>"
```

## Crear Una Clave SSH para GitHub
---

> [!NOTE]
> Las claves SSH se usan para autenticar conexiones seguras. Git es capaz de usar claves SSH en lugar de la autenticación tradicional mediante contraseña al enviar o incorporar cambios a repositorios remotos.

1. Ingresar a la ruta `/user/mi_usuario`
2. Crear un directorioi llamado `.ssh`
	1.  `mkdir .ssh`
	2. Ingresar al directorio `.ssh` -> `cd .ssh`
	3. Ingresar el siguiente comando para generar la clave:
		1. Forma antigua
			1. `ssh-keygen -t rsa -C "correo@gmail.com"`
		2. Forma más segura
			1. `ssh-keygen -t ed25519 -C "tu_correo@ejemplo.com"`
3.  Una vez creada la clave la podemos subir a GitHub
4.  Agregar la clave privada al agente
	1.  ```
		eval "$(ssh-agent -s)"
		ssh-add ~/.ssh/id_ed25519
		```
