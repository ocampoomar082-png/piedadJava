Se genero un repositorio en git hub el cual se configuro con un proyecto en node, dicho en el repositorio se le agrego un webhook el cual nos permita identificar y que a su vez detone el pipeline en la instacia de  jenkins configurada cada vez que se genere un commit o push, esto nos permitira realizar una serie de pasos hasta poder llegar al despliegue del aplicativo.

A Continuacion dejo los aspectos tecnicos que se implementaron para poder llegar al resultado.
1.-Se genero una instalacion en jenkins que para poder llevar acabo la generacion de pipelines en ella se configuro el node, ssh y se activaron los trigger para la detonacion de los pipelines
<img width="1064" height="392" alt="image" src="https://github.com/user-attachments/assets/105bcb83-8840-4a36-b992-1e5f60bff1e7" />

<img width="1243" height="463" alt="image" src="https://github.com/user-attachments/assets/901026a8-6bd2-47c1-80e6-b2c503f01413" />
y se instalaron varios plugins para tener una vista de los stage tal como la tenemos. y asi tambien para poder realizar la conexion ssh entre equipos.
