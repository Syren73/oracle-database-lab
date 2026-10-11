
1. ¿Qué diferencia hay entre una imagen y un contenedor? Usa como ejemplo lo que hiciste en los ejercicios
G2 y G4.

Una imagen es un archivo binario de solo lectura con los datos necesarios para ejecutar una aplicación, un contenedor es
una imagen en estado de ejecución, en contendor, a su vez, puede contener multiples imágenes.

2. En el Ejercicio G5 el archivo nota.txt desapareció y en el G6 no. Explica por qué.

Los datos almacenados en G6 fueron almacenados en un volumen de datos, lo que permite 
que se separe del ciclo de vida de los contenedores, y evita que se elimine cuando se 
acaba la ejecución del primer contenedor.

3. ¿Qué diferencia hay entre docker ps y docker ps -a, y qué significa STATUS = Exited (0)?

"docker ps" muestra el estado de todos los contenedores en ejecución, "docker ps -a" muestra el estado de todos los contenedores en
ejecución, y todos los contenedores detenidos. "STATUS = Exited (0)" indica que el contendor ha terminado de ejecutarse y que no han ocurrido errores.

4. En -p 8181:8181, ¿qué número corresponde a tu equipo y cuál al contenedor? ¿Qué pasaría con -p 80:8080
en el ejercicio de nginx?

-p 8181:8181
Equipo: 8181, contenedor: 8181

-p 80:8080
Equipo: 80, contenedor: 8080
nginx es un servidor web que escucha por defecto en el puerto 80,  para que funcione correctamente se debería cambiar
el puerto del contendor de 8080 a 80.


5. ¿Por qué un contenedor de Oracle se queda en marcha y el de hello-world termina solo?

El contendor de Oracle se queda abierto para gestionar conexiones, peticiones, etc. El contenedor 
de hello-world realiza su ejecución y termina, ya que la finalización de su ejecución no depende 
del input de un usuario.

6. ¿Qué es el digest de una imagen y por qué lo registramos si ya sabemos que usamos :latest?

El digest de una imagen es la huella digital que tiene una imagen que la identifica, una misma imagen 
puede tener dos digest diferentes, esto quiere decir que son dos versiones distintas. 
:latest sirve para apuntar al ultimo digest de una imagen, es decir, su versión más actualizada, si
solo almacenamos :latest en lugar del digest que corresponda, después de un tiempo, si cambia :latest, 
se perderá la referencia a la versión que se haya usado para dicha ejecución.

7. ¿Qué comando borraría realmente los datos de Oracle? ¿Por qué docker rm oralab-26ai no lo hace?

"docker rm" solo elimina los contenedores detenidos, pero no elimina los volúmenes, 
para eliminar los volumentes el comando completo seria "docker rm -v oralab-26ai" 

8.1.2. Git, organización y evidencia

8. ¿Por qué este laboratorio se hace dentro del repositorio oracle-database-lab, con Issue, branch y Pull
Request, en vez de en una carpeta aparte?

En caso de necesidad, se puede recrear el entorno en otros pc y dispositivos, permite mantener
un historial de los scripts y las salidas que generaron, y permite que sea más fácil introducir 
nuevos miembros en el equipo; solo tienen que leer el repositorio para ver como instalar el entorno.

9. ¿Qué diferencia hay entre source 00-config.sh y bash 00-config.sh? ¿Por qué usamos source?

"source" ejecuta el archivo en la sesión actual de bash, no se abre un subproceso para realizar la ejecución, de manera
que las variables definidas en el archivo se mantienen en la sesión actual.
"bash" abre un proceso independiente de la sesión actual, por lo que las variables de entorno que se hayan definido no 
se podrán usar en la sesión original.

10. Explica cada parte del nombre 20260915T091230Z_02-docker.script.log.

20260915T091230Z_02 = Es el timestamp, identifica el momento en el que se registro el archivo.
02 = Indica la evidencia a la que corresponde según el documento.
docker = Describe brevemente la evidencia.
script.log = Sufijos para indicar la categoría de la evidencia, en este caso, es un log generado por un script.

11. ¿Para qué sirve .gitattributes y qué error evita?

Usar .gitattributes evita problemas de formato entre sistemas que usen diferentes finales de linea, 
difentes sistemas operativos y diferentes tipos de archivos pueden tener finales de linea diferente, 
usando .gitattributes se puede definir las reglas que se quieren aplicar a los archivos para normalizarlos
y que git realice dicho proceso automáticamente.

12. ¿Por qué en este Pull Request elegimos Create a merge commit en lugar de Squash and merge?

Queremos mantener el historial con todos los pasos realizados, si usamos Squash and merge, se 
pierden varios de los pasos pequeños que se han realizado.

13. Describe las cuatro capas de la estrategia de contraseñas (Parte D) y qué pasaría si te saltas la primera.

En la primera capa, indicamos a git que archivos debe ignorar, es decir, archivos que no
queremos que se queden en el historial, como pueden ser archivos donde guardamos credenciales de login.

En la segunda capa, creamos una plantilla que se puede usar como referencia para saber el formato
y restricciones de los datos guardados, longitud de contraseña, caracteres especiales, etc.

En la tercera capa, tenemos el archivo real, en memoria local, es decir
dentro del dispositivo, pero sin que git lo maneje.

En la cuarta capa, se cargan las variables de entorno del archivo de contraseñas y se configura para que 
cualquier cambio realizado se exporte automáticamente al archivo correspondiente, las contraseñas en si no 
se escriben directamente, se acceden mediante variables de entorno del terminal actual.

14. ¿Por qué no escribimos la contraseña directamente en el comando docker run, aunque el script no se suba
a Git?

La contraseña puede quedar expuesta aunque el script no se suba a git, puede filtrarse el historial de comandos del
terminal, y dependiendo de los parámetros, se puede llegar a filtrar la contraseña

15. Si descubres tu contraseña en un commit ya publicado, ¿basta con borrarla en un commit nuevo? ¿Qué
debes hacer?

Rotar la contraseña, comprobar quien tiene a acceso a la Branch donde se ha publicado, revisar si 
se han realizado modificaciones usando dicha contraseña sobre cualquier archivo y, si se han realizado cambios sin
autorización, cargar un backup. 

16. ¿Por qué no usamos SPOOL ni @archivo.sql con sqlplus dentro del contenedor, y qué hicimos en su lugar?

La imagen de Oracle no contiene Database Actions, hemos tenido que instalar un componente independiente, ORDS, 
es un servicio REST de Oracle.

17. ¿Qué hace WHENEVER SQLERROR EXIT SQL.SQLCODE al inicio de V000 y V001, y qué pasaría sin esa
línea?

Cuando ocurre un error de ejecución SQL, se temina la ejecución, sin esta linea, en caso de que 
hubiera un error, este se podría arrastrar, el código se podría seguir ejecutando ignorando los errores de líneas anteriores, lo cual
puede terminar en resultados incorrectos.

18. ¿Qué es una migración y por qué V000 y V001 no se deben editar una vez aplicadas?

Una migración es un script SQL versionado y numerado que lleva la base de datos de un estado
al siguiente. Una vez creada una versión, esta no se debe modificar, ya que si se modifica, 
seria una nueva versión, si por el motivo que fuese hay un error en v001 que se quiera arreglar, se debe publicar una
nueva versión V002. 

19. ¿Por qué en SQL Developer se usa el servicio FREEPDB1 y no FREE ni un SID?

El parámetro FREE solo te conecta al contenedor raíz, donde no esta permitido crear tablas
ni usuarios, al usar un servicio, la conexión se realiza en un espacio de trabajo designado
donde si se pueden crear tablas y usuarios.

20. ¿Qué aporta SQLcl frente a SQL*Plus, y por qué un DBA debe dominar ambas?

SQLcl se instala en el equipo personal del desarrollador , SQL*Plus se instala en 
el contenedor, SQL*Plus se puede encontrar en cualquier servidor Oracle desde 1982, por lo 
que es necesario saber usarlo, y SQLcl es la herramienta moderna que se usa dia a dia y 
que tiene brinda multiples facilidades respecto a SQL*Plus.

21. ¿Por qué el curso pasa de Git Bash a Ubuntu en WSL 2? Da al menos dos problemas concretos de Git Bash
que desaparecen en Ubuntu.

No hay gestor de paquetes usando Git Bash, en Ubuntu si, adicionalmente, Ubuntu tiene 
acceso a las herramientas de Linux, lo cual facilita hacer operaciones de seguimiento 
más complejas, o por lo menos con mayor facilidad que si se usa Git Bash

22. ¿Por qué clonamos el repositorio en ~/oracle-database-lab y no trabajamos sobre la carpeta de Windows
(/mnt/c/...)? ¿Y por qué recomendamos bash frente a zsh para los scripts del curso?

Podemos trabajar en la carpeta de Windows, pero cada operación cruza entre los dos sistemas (Ubuntu -> Windows), lo cual
hace que los procesos sean varias veces más lentos. Por reglas profesionales, los scripts compartidos se escriben en bash,
y por ahora, los scripts que hemos escrito en este curso están escritos en bash, por lo que recomendaría usar bash 
sobre zsh durante el curso.

