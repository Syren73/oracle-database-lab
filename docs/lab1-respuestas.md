1. ¿Cuál es la diferencia entre Working Directory, Staging Area y Local Repository? Da un ejemplo de un archivo pasando por las tres.

Working Directory contiene los archivos y carpetas de nuestro proyecto, estos son los archivos sobre los que trabajamos, Staging Area es el segmento donde se almacenan temporalmente los cambios que se quieren realizar sobre archivos antes de realizarlos con un commit, Local Repository contiene un historial de los commits realizados.


 touch ejemplo.md
 git add ejemplo.md
 git commit -m "docs: creación archivo ejemplo"

La primera linea crea el archivo, esto se puede reflejar en nuestro proyecto (Working Directory), la segunda linea indica
a git que mantenga control de versiones del nuevo archivo, este comando se almacena previamente en Staging Area y con la tercera linea
realizamos los cambios indicados previamente, y los cambios realizados son alamcenados en Local Repository. 

2. Si modificas un archivo pero no haces git add, ¿aparece ese cambio en tu próximo commit? Explica por
qué.

Depende de si se había agregado el archivo previamente con git add, en caso de que no sea así, los cambios no aparecerán 
en el próximo commit, esto se debe a que git no hace seguimiento automáticamente de todos los archivos del proyecto, se tiene
que indicar previamente con git add <nombre_archivo> para asegurarse de que los cambios posteriores se vean reflejados.


3. ¿Por qué git status no mostraba las carpetas vacías que creaste en la Parte C? ¿Qué truco usamos para
solucionarlo?

Git no hace control de versiones de carpetas, sino de archivos, si las carpetas están vacias, no hay ningún rastro
que git pueda seguir, para solucionarlo agregamos un archivo que actúa de placeholder en cada una de las carpetas vacias, según 
convenio, .gitkeep
 
4. Explica con tus palabras qué es HEAD

Es un puntero que indica la versión actual en la que estamos trabajando, es decir, 
la branch sobre la que estamos realizando cambios.

5. ¿Qué diferencia hay entre crear una branch con git switch -c y crear una carpeta nueva con mkdir?
¿Cómo lo comprobamos en la Parte G?

mkdir crea una carpeta, una branch es un puntero a un commit, se puede comprobar con ls -la que 
al crear una brach mediante git switch -c, esta no aparece registrada como una carpeta.

6. Durante el conflicto de la Parte H, ¿qué representaba el contenido entre <<<<<<< HEAD y =======? ¿Y
entre ======= y >>>>>>>?

<<<<<<< HEAD; comienzo de la versión existente en el branch activo.
=======; separador entre las versiones de conflicto.
>>>>>>>; termina la versión de la branch que se estaba fusionando

7. ¿Por qué NO se debe hacer git commit --amend sobre un commit que ya se subió con git push?

git commit --amend modifica el historial, elimina el commit anterior y crea uno nuevo con otro hash, esto provoca que si alguien ha
trabajado con el archivo después del push, pero antes del amend, habrá divergencias y el historial de versiones será incompatible. 

8. Si borras por accidente la carpeta .git de tu proyecto, ¿qué se pierde exactamente? ¿Se pierde también
el código fuente que está en el disco.

Se borrara el historial de versiones, lo que significa que se pierden todas las branches y todo el historial de
commits, también se perdería el commit que se estaba realizando antes de borrar la carpeta, ya que se pierde
el Staging Area, pero el código fuente del disco permanece igual, ya que .git no contiene todo el proyecto.


9. Explica con tus propias palabras la diferencia entre Git y GitHub, sin usar la palabra "nube"

Git es una aplicación para control de versiones de archivos en repositorios, GitHub es una plataforma que permite
almacenar/interactuar con múltiples repositorio Git de manera remota. GitHub contiene repositorios que usan el 
sistema de versión de controles Git. GitHub agrega otras características para el control de versiones que no agrega Git.

10. ¿Por qué no se debe subir un archivo .env con contraseñas reales a un repositorio, aunque el
repositorio sea privado?

Que el repositorio sea privado no quiere decir que sea un lugar apropiado para guardar contraseñas y credenciales, aunque el repositorio sea privado, si una persona cualquiera tiene el token de acceso de alguien que tenga autorización, esta persona podrá ver e interactuar con las contraseñas, lo cual supone un problema de seguridad.

11. Un compañero te dice: "hice push y ahora GitHub me rechaza el segundo push con 'non-fast-
forward'". ¿Qué ha ocurrido probablemente y qué comando ejecutarías primero?

El historial de versiones local es diferente del remoto, el primer comando a usar será git pull, para traer el contenido restante;
después habrá que tratar los conflictos si los hay; luego hay que hacer git push otra vez.
   
12. ¿Qué tipo de Conventional Commit (feat, fix, docs, test…) usarías para: añadir un índice de
rendimiento a una tabla, corregir una restricción mal definida, y actualizar el README?

docs: fix constrain definition