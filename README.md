Se genero un repositorio en git hub el cual se configuro con un proyecto en node, dicho en el repositorio se le agrego un webhook el cual nos permita identificar y que a su vez detone el pipeline en la instacia de  jenkins configurada cada vez que se genere un commit o push, esto nos permitira realizar una serie de pasos hasta poder llegar al despliegue del aplicativo.

A Continuacion dejo los aspectos tecnicos que se implementaron para poder llegar al resultado.
1.-Se genero una instalacion en jenkins que para poder llevar acabo la generacion de pipelines en ella se configuro el node, ssh y se activaron los trigger para la detonacion de los pipelines
<img width="1064" height="392" alt="image" src="https://github.com/user-attachments/assets/105bcb83-8840-4a36-b992-1e5f60bff1e7" />

<img width="1243" height="463" alt="image" src="https://github.com/user-attachments/assets/901026a8-6bd2-47c1-80e6-b2c503f01413" />
y se instalaron varios plugins para tener una vista de los stage tal como la tenemos. y asi tambien para poder realizar la conexion ssh entre equipos.

2.-commo segundo aspecto se configuro una instancia de docker para poder llevar acabo la construccion de la imagenes el enlace con el servicio docker se hizo atravez de una conexion ssh en la cual se tuvieron que generar keys de seguridad asi tambien de lado de jenkins se instalos el plugin Open SSH.
<img width="1307" height="597" alt="image" src="https://github.com/user-attachments/assets/b2e1d0fd-e5e1-4377-b343-3c6f60389e3c" />
<img width="780" height="307" alt="image" src="https://github.com/user-attachments/assets/a5ac4d1b-d5bf-4ed2-b858-6090461ae475" />


3.-Para temas de proceso de la detonacion del pipelines se genero un repositorio en github al cual se les fue asignado un webhook que apunta diretamente hacia el jenkins, aqui debimos poner el jenkins que se configuro como una instacia local publicarlo y que fuera publico atravez de una herramienta que se llama ngrok
<img width="1220" height="558" alt="image" src="https://github.com/user-attachments/assets/6cdc01e5-2c5b-44b5-b003-bd3a68f3e1d8" />
adicional a esto en el proyecto con el que estamos trabajando debemos de agregar la opcion de triggers para que en el instante que exista un cambios se detone.
<img width="1053" height="502" alt="image" src="https://github.com/user-attachments/assets/f8dcb46e-00be-4145-b07e-2b0b48487fe8" />

adicional quisiera mencionar que antes de interactuar con los repositorios de una cuenta github es necesario generar clavess o credenciales en jenkins para poder realizar actividades de clonado y resguardo de jenkinsfile
<img width="946" height="356" alt="image" src="https://github.com/user-attachments/assets/22865165-f192-4d09-b810-ef3795391583" />

4.-Para poder llevar
4.los requisitos para poder trabajar y ocupar el proceso es tener clonado el proyecto
  -tener instalado un git bash o alguna ora herramienta que termita interactuar con git.
 - En este caso es un proyecto node la compilacion los test y demas stage los realiza en servidor donde fue configurado el jenkins
 - el desarrollador solo se encargara de subir los cambios y el proceso se detonara de manera automatica generara su imagen y la depositara en el ECR y la desplegara en un servicio.
   <img width="485" height="478" alt="image" src="https://github.com/user-attachments/assets/2a00fe6d-f1c2-4e75-8ff0-34818dcf7c36" />

  <img width="941" height="273" alt="image" src="https://github.com/user-attachments/assets/85b0bf0d-9543-404a-bb68-52605ae2c1e8" />



