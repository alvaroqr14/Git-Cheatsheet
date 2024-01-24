# Git-Cheatsheet

### Comandos generales
- mkdir directorio	(crear directorio)
- cd directorio		(mover a un directorio)
- ls			(listar archivos en un directorio)

### Git configuracion

*--global indica que es para todos los repositorios en la computador
- git --version					(saber versión instalada)
- git config --global user.name “nombre” 	(cambiar nombre)
- git config --global user.email “email”		(cambiar email)
- git config --global -e				(editar config)
- git config --global init.defaultBranch main	(cambiar el nombre de la rama por default a main)
- git config core.autocrlf true			(para omitir mensaje de warn con caracter CRLF)
- git config --global pull.rebase true 	 (define por default que el pull sea de tipo rebase)

**Alias**
- git config --global alias.s “status -sb” 	(para generar alias de status)
- git config --global alias.lg "log --graph --abbrev-commit --decorate --format=format:'%C(bold blue)%h%C(reset) - %C(bold green)(%ar)%C(reset) %C(white)%s%C(reset) %C(dim white)- %an%C(reset)%C(bold yellow)%d%C(reset)' --all" (para generar alias de log)

**Ayuda**
- git help --all			(ayuda general)
- git command -help		(ayuda para el comando)

### git para el ordenador

- git init			(inicializamos la carpeta como repositorio)
- git status		(estado de nuestras modificaciones, nuevos archivos y ramas)
- git status --short 	(muestra de forma resumida el status)
- git add patrón 		(agrega todos los cambios al stage)

  **Wildcard o patrones:**
  - . : todos los archivos del directorio actual y subdirectorios
  - --all o -A : todos los archivos del repositorio
  - *.java : todos los archivos java del directorio actual
  - **/*.java :  todos los archivos java del directorio actual y sus subdirectorios
  - Documentation/*.txt : todos los archivos java del directorio Documentacion y sus subdirectorios
  - git add foo.? : todos los archivos en el directorio que empiezan con “foo” y extension de 1 caracter

**Deshacer cambios**
- git restore nombreArchivo	(quita cambios de un archivo (no subido al stage))
- git reset nombreArchivo	(remueve los archivos del stage)
- git rm --cached file		(marcar el archivo como untracked y mantener el archivo)
- git checkout -- .		(restaura los archivo al commit previo de cambios no subidos al stage)

**Ver cambios**
- git diff				(muestra los cambios entre lo actual (no subido al stage) y el commit anterior) -> no se usa mucho
- git diff	--staged			(muestra los cambios entre lo actual y el commit anterior) -> no se usa mucho se usa mas un editor de código

**Guardar cambios**
- git commit -m “mensaje” 	(guardar el stage en el repo local)
- git commit -am “mensaje” 	(combinar git add (solo para archivos trackeados) y git commit)
- git commit --amend 		(reemplazar en el commit anterior con el commit actual)
- git log 				(muestra logs de commits del repo actual)

**Trabajo con ramas**
- git branch			(muestra la lista de ramas locales e indica en que rama estas)
- git branch -a			(muestra la lista de ramas locales y remotas e indica en que rama estas)
- git branch nombreRama		(crear rama)
- git branch -m nombreActual nombreNuevo 		(renombrar rama)
- git checkout nombreRama		(cambiar rama)
- git checkout -b nombreRama		(crear y moverse a la rama creada)
- git branch -d nombreRama		(eliminar rama si ya se hizo merge)
- git branch -D nombreRama		(eliminar rama incluso si no se hizo merge)

- git merge nombreRama		(une rama actual con la rama indicada y crea un nuevo commit)

  - Sin conflictos se llama fast-forward
  - Con conflictos entra a un estado de resolucion, luego de corregir usar git add
  - Recomendación utilizar los editores de código

**Moverse entre commits**
- git reset --hard hash 	(regresa al commit del hash o se puede usar HEAD^x, donde x indica el numero de commits anterioes, elimina los commits posteriores y elimina cambios posteriores)
- git reset --soft hash		(regresa al commit del has, elimina los commits, pero no elimina cambios)
- git reset --mixed hash		(regresa al commit del has, elimina los commits, pero no elimina cambios y los saca del stage)
- git revert HEAD		(hace lo mismo que el reset pero el cambio lo hace en un nuevo commit)

- git reflog			(muestra todos los movimientos hechos en un repo)

- git rebase nombreRama		(une rama indicada con la rama actual pero mueve los commits de la rama actual adelante del ultimo commit de la rama indicada)
- git rebase -i HEAD~indice		(permite realizar acciones sobre los commits anteriores (indice))

**Trabajo con tags**
- git tag						(listar los tags)
- git tag -d nombreTag				(eliminar tag)
- git tag -a nombreTag hash -m “mensaje” 	(crear tag anotado)
- git show nombreTag 				(mostrar datos del tag)

**Trabajo con el stash**
- git stash					(guarda los cambios en el stash)
- git stash list					(lista los stash)
- git stash pop					(trae el stash 0 (funciona como una cola , ultimo en entrar primero en salir)
- git stash drop index				(borra el stash en ese indice)
- git stash apply index				(aplica el stash de ese indice)
- git stash save “mensaje”			(guarda el stash con ese mensaje)
- git stash clear					(limpia todos los stash)

### Git para remoto (GitHub)

- git remote add origin urlGithub 	(vincular a github)
- git push -u origin nombreRama	(publicar en rama remota y relaciona la rama remota con la rama actua para el trabajo remoto(push, pull, etc.))
- git push origin nombreRama		(publicar en rama remota (la crea si no existe))
- git fetch origin				(trae todos los cambios remotos (referencias) al repositorio local)
- git pull origin nombreRama		(traer cambios de rama remota)
  - pull es la combinacion de 2 comandos fetch y merge
- git push origin branch --tags		(push tags)
- git clone urlGithub nombreCarpeta	(clonar repo remoto a local)
- git remote remove origin		(eliminar enlace remoto)
