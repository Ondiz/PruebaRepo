TUTORIAL DE GIT


¿Qué es Git?


Git es un software de control de versiones, es decir, permite gestionar los cambios que se realicen sobre un producto.


Uso


Git se usa desde la consola :)


Primero hay que decirle a Git quien eres:
- Email: git config --global user.email “email”
- Nombre: git config --global user.name “nombre”


- Para inicializar: git init. Se crea un repositorio vacío en /.git/ 
- Para ver el estado del repositorio: git status. Dirá si se ha realizado algún cambio a los archivos que se siguen
- Para añadir un archivo del que se registrarán los cambios: git add nombreArchivo. (Se pueden añadir varios archivos con ‘*.extensión' o todos los archivos de la carpeta con . (. = carpeta actual))
- Para guardar los cambios realizados (lo que se conoce como commit): git commit -m “Mensaje con resumen sobre los cambios” (Antes de que se haga el commit pero después del add los cambios están ‘staged’, es decir, se sabe que han ocurrido cambios en los archivos pero se puede decidir entre cambiar los archivos en el repositorio mediante commit o anular los cambios con reset) Si se ignora el -m en el commit se abrirá un editor de texto para escribir interactivamente el comentario.
- Para ver todos los commits hechos hasta el momento: git log (cambia formato a versión de una línea con git log --pretty=oneline Otra manera elegante de ver el log: git log --pretty=format:'%h %ad | %s%d [%an]' --graph --date=short)
- Se puede guardar todo en un repositorio online como GitHub o Gitorious. Para añadir: git remote add nombre_repositorio URL_repositorio
- Para mandar los cambios al repositorio online: git push -u nombre_repositorio nombre_rama (-u sirve para recordar los parámetros, nombre_rama debe ser master a no ser que haya ramas nuevas) git push sin más sube todos los cambios
- Para recuperar los cambios: git pull nombre_repositorio nombre_rama
- Para ver qué cambios ha habido desde el último commit: git diff HEAD (HEAD es un puntero que refiere al último commit)
- Para quitar archivos de los que se registran los cambios: git reset nombre_archivo
- Dejar las cosas como estaban en el último commit: git checkout nombre_archivo
(Para volver al estado que te interese: git checkout número_hash El número hash puede verse al hacer git log, solo son necesarias las 7 primeras cifras. En este momento se abre una nueva rama para que puedas hurgar, pero no se modifica nada en principio. Para volver al último estado git checkout master (vuelve a la rama master))
- Crear una nueva rama: git branch nombre_rama (con git branch se ve las ramas que hay)
- Para cambiar de rama: git checkout nombre_rama
- Para eliminar archivos (tanto del ordenador como del archivo de cambios): git rm nombre_archivo (después de eliminar hacer un commit con una explicación)
- Para fusionar la rama actual con otra: git merge rama_a_unir
- Para eliminar una rama: git branch -d nombre_rama
- Se pueden etiquetar las versiones: con git tag etiqueta_de_versión se etiqueta la versión actual; para etiquetar las anteriores hay que hacer un checkout primero, es posible ir con el hash y también con notación ^: git checkout etiqueta_de_versión^ irá al padre de la versión. Una vez etiquetadas las versiones se pueden rescatar con la etiqueta en lugar de con el hash. Para ver las etiquetas git tag. Para ver las etiquetas en el log git log --pretty=format:'%h %ad | %s%d [%an]' --graph --date=short master --all 
- Para deshacer un commit: git revert HEAD (o el hash del commit que haya que anular). Esto eliminará el commit pero no lo quitará del log, para eso hay que resetear a antes del commit malo: git reset --hard etiqueta_de_versión. Aunque se haga esto los commits no desaparecen si están etiquetados, con git log --pretty=format:'%h %ad | %s%d [%an]' --graph --date=short master --all pueden verse. La etiqueta puede quitarse con: git tag -d etiqueta_de_versión
- Se pueden corregir commits con git commit --amend -m “Nuevo comentario”
- Para cambiar de carpeta: git mv archivo carpeta. Esto elimina el crea el archivo dentro de la carpeta y elimina el de fuera. Si se hace mv fuera de git hay que eliminar el archivo a mano. 
- Se puede cambiar el archivo .gitconfig para generar aliases. Habría que añadirle:


[alias]
 hist = log --pretty=format:'%h %ad | %s%d [%an]' --graph --date=short 


Y ahora con escribir git hist ejecuta toda la frase


- Se pueden clonar repositorios con git clone repositorio_a_clonar nombre_repositorio_clonado. Se puede ver de donde proviene este repositorio con git remote y git remote show nombre_que_devuelve (será origin seguramente). 
- Si se realizan cambios en el repositorio original, pueden recuperarse en el clon con git fetch y luego git merge origin/master o el equivalente que es git pull




Más:


Tutorial en Code Academy: https://try.github.io/levels/1/challenges/1
Minitutorial: http://rogerdudler.github.io/git-guide/
Visual guide to Git: http://marklodato.github.io/visual-git-guide/index-en.html
Inmersión en Git: http://gitimmersion.com
Libro de Git: http://git-scm.com/book/es/
Git para Windows: http://msysgit.github.io/
Think like a git: http://think-like-a-git.net/
