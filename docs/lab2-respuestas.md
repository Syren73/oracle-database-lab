1. ¿Por qué un Issue sin criterios de aceptación es un problema, aunque la descripción general
parezca clara?

* Aunque la descripción sea clara, al no seguir criterios de aceptación, tendrá mala trazabilidad, lo
cual es un problema a largo plazo.  

2. Explica la diferencia entre "Refs #N" y "Closes #N" en un mensaje de commit o en la
descripción de un Pull Request.

* Refs #N es una convención que GitHub reconoce, enlaza automáticamente el commit con el issue numero 'N',
 Closes #N cierra automáticamente el issue 'N' cuando el commit o Pull Request llega al main.


3. ¿Qué ocurre exactamente si intentas hacer git push directamente sobre una branch main
protegida? ¿Es un error tuyo o un fallo del sistema?

* Saltara un error Protected branch update failed" al hacer push, este es el resultado correcto y 
esperado, no es un fallo del sistema.

4. Un compañero te dice: "he aprobado el PR sin mirar los archivos, total ya me fío". ¿Qué riesgo
tiene esa forma de revisar?

* Principalmente, riesgo de seguridad, ya que no se ha hecho ninguna revisión de 
si los archivos han sido modificados o agregados para permitir acceso a información sensible,
tampoco se verifica que los nuevos archivos sean mantenibles o legibles a largo plazo. 

5. Si el reviewer pide un cambio y tú ya habías hecho push de tu branch, ¿tienes que abrir un Pull
Request nuevo? Explica qué ocurre técnicamente con el PR existente cuando haces un nuevo
commit.

* Los commit se agregan automáticamente a la Pull Request de la Branch correspondiente,
por lo que no es necesario crear nuevas Pull Request.

6. Describe con tus palabras la diferencia entre Merge commit, Squash and merge y Rebase and
merge. ¿Cuál usarías para una branch con commits "wip", "fix", "fix2", "ok ya"?

* Merge commit conserva todos los commits de la branch más un
commit de fusión, Squash and merge combina todos los commits de la branch en un único commit,
Rebase and merge reaplica los commits de la branch sobre main sin
commit de fusión. Usaria Squash and merge, ya que son commits que no aportan mucha información, y no
tiene demasiado sentido llenar el historial main con este tipo de commits.

7. ¿Por qué borrar una branch después del merge no elimina el trabajo realizado en ella?

* Porque la branch main contiene el trabajo de la antigua branch tras realizar el merge, 
una vez realizado el merge, se puede borrar la branch fusionada en local y remoto y no habrá perdida de información.


8. ¿Qué información debería contener siempre la descripción de un Pull Request, como mínimo?

* Qué hace el cambio (resumen de una o dos frases) → Summary.
  Por qué se hace (el problema que resuelve, con enlace al ticket) → Related Issue.
  Cómo probarlo (pasos concretos, o enlace a un entorno de pruebas) → Testing.
  Evidencia visual cuando aplica (capturas o vídeos cortos del antes/después, especialmente en cambios de interfaz).

9. Un reviewer escribe solo "esto está mal" como comentario. ¿Qué le falta a ese comentario para
ser útil? Reescríbelo tú con un ejemplo inventado.

* No da información adicional para indicar porque esta mal, como esta mal, que esta mal o donde esta mal, tampoco
ha dado ninguna posible solución para el problema teorico. 

Ej: (suggestion non-blocking): Hay dos typos en la linea numero 43 del archivo INFORMACION.dm, gti = git y Reqest = Request, intenta
cambiarlos cuando puedas. 
  
10. ¿Qué diferencia hay entre que main esté protegida y que simplemente el equipo "se ponga
de acuerdo" en no hacer push directo?

* Puede cometerse errores humanos y que se realice un push sin querer, o en su defecto, puede que 
simplemente alguien ignore una regle hablada y lo haga queriendo, es mejor tener reglas que se 
apliquen siempre independientemente de las intenciones que tengan los miembros del equipo. 

11. Explica con un ejemplo propio la diferencia entre un comentario issue: (blocking) y uno
nitpick: (if-minor) en formato Conventional Comments.

blocking: Esta función permite que el usuario haga login únicamente con un correo electrónico, 
es necesario antes de continuar agregar la condición de contraseña para aumentar la seguridad
de los usuarios.

nitpick: Podriamos cambiar el nombre de las variables para que sea más legible el código:
x1 => x_filas, x2 => x_columnas, y1 => y_filas, y2 => y_columnas. Usamos muchas abreviaturas,
igualmente, esto no afecta a la funcionalidad, asi que no es necesario para aprobar el Pull Request.

Blocking indica que la solicitud tiene que cumplirse para poder aprobar el Pull Request,
nitpick indica una sugerencia que no tiene suficiente peso como para ser una condición en la Pull Request, 
pero que podría ser útil si se implementa.


12. Si tu próximo commit es feat!: cambia la firma de la función principal de la API, ¿qué tipo de
versión SemVer se dispara y por qué?

* MAJOR (2.1.0 → 3.0.0), indica un cambio que rompe la compatibilidad y fuerza un lanzamiento MAJOR.

13. ¿Por qué abrir un Draft PR desde el primer commit estructural puede ahorrar tiempo al
equipo, aunque parezca más lento para el autor individual?

* Asegura que el diseño que se va a desarrollar sea el buscado, evitando que se acabe desarrollando
un diseño que no sea el buscado o tener que refactorizar posteriormente a partir de un diseño incorrecto. Es
más sencillo asegurar que se este en el enfoque correcto desde el principio.
