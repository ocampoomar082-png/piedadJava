Integración del repositorio con Jenkins para despliegue automatizado
Se creó un repositorio en GitHub que contiene un proyecto desarrollado en Node.js. A dicho repositorio se le configuró un webhook que permite detectar eventos como commits o pushes, y que a su vez activa automáticamente el pipeline en la instancia de Jenkins previamente configurada. Esta integración permite ejecutar una serie de etapas definidas en el pipeline, culminando en el despliegue del aplicativo de forma automatizada.
A continuación, se detallan los aspectos técnicos implementados para lograr este resultado:
- Instalación y configuración de Jenkins
Se realizó la instalación de Jenkins en un entorno controlado. Para habilitar la ejecución de pipelines, se configuraron los siguientes componentes:
- Integración con Node.js para compilar y ejecutar el proyecto.
- Configuración de acceso por SSH para conexión segura con servidores remotos.
- Activación de triggers que permiten la ejecución automática del pipeline ante eventos provenientes del repositorio GitHub.

<img width="1064" height="392" alt="image" src="https://github.com/user-attachments/assets/105bcb83-8840-4a36-b992-1e5f60bff1e7" />

<img width="1243" height="463" alt="image" src="https://github.com/user-attachments/assets/901026a8-6bd2-47c1-80e6-b2c503f01413" />

Además de la configuración inicial, se instalaron múltiples plugins en Jenkins con el objetivo de mejorar la experiencia de desarrollo y operación. Entre ellos destacan los complementos que permiten visualizar gráficamente las etapas (stages) del pipeline, facilitando el seguimiento de cada fase del proceso de integración y despliegue. Asimismo, se instalaron extensiones específicas para habilitar la conexión SSH entre equipos, lo cual fue fundamental para la comunicación segura entre Jenkins y otros servicios.

2.- Configuración de instancia Docker para construcción de imágenes
Como segundo componente técnico, se implementó una instancia de Docker destinada a la construcción automatizada de imágenes del aplicativo. La conexión entre Jenkins y el servicio Docker se estableció mediante una sesión SSH, para lo cual fue necesario generar claves de seguridad que garantizaran la autenticidad y confidencialidad de la comunicación.

- Del lado de Jenkins, se instaló el plugin OpenSSH para habilitar esta funcionalidad.

- Esta integración permite que Jenkins envíe instrucciones de construcción directamente al entorno Docker, asegurando que las imágenes se generen de forma controlada y reproducible.

<img width="1307" height="597" alt="image" src="https://github.com/user-attachments/assets/b2e1d0fd-e5e1-4377-b343-3c6f60389e3c" />
<img width="780" height="307" alt="image" src="https://github.com/user-attachments/assets/a5ac4d1b-d5bf-4ed2-b858-6090461ae475" />


3.-Publicación de Jenkins y configuración de Webhook para detonación de pipelines
Para habilitar la ejecución automática de pipelines ante cambios en el código fuente, se creó un repositorio en GitHub al que se le asignó un webhook dirigido directamente a la instancia de Jenkins. Dado que Jenkins fue configurado inicialmente como una instancia local, fue necesario exponerla públicamente para que GitHub pudiera comunicarse con ella.
- Para lograr esto, se utilizó la herramienta Ngrok, la cual permite crear túneles seguros desde una red pública hacia servicios locales. Esta solución permitió publicar temporalmente la instancia de Jenkins con una URL accesible desde GitHub, facilitando así la integración continua.
- El webhook se configuró para detectar eventos como push o commit, y activar el pipeline correspondiente en Jenkins.
- Esta arquitectura garantiza que cada modificación en el repositorio desencadene automáticamente el proceso de construcción, pruebas y despliegue del aplicativo.

<img width="1220" height="558" alt="image" src="https://github.com/user-attachments/assets/6cdc01e5-2c5b-44b5-b003-bd3a68f3e1d8" />
- Como parte de la mejora continua del proyecto, se identificó la necesidad de incorporar triggers que permitan la ejecución automática del pipeline en el instante en que se detecten cambios en el repositorio. Esta funcionalidad es clave para garantizar una integración continua eficiente y sin intervención manual.
- Los triggers se configuran en Jenkins mediante la opción "GitHub hook trigger for GITScm polling", la cual permite que Jenkins escuche activamente los eventos enviados por el webhook del repositorio.
- Al detectar un evento como push, Jenkins inicia de forma inmediata el pipeline correspondiente, asegurando que los procesos de construcción, pruebas y despliegue se ejecuten en tiempo real.
- Esta configuración refuerza la automatización del flujo de trabajo, reduce tiempos de respuesta y mejora la trazabilidad de los cambios aplicados al código fuente.


<img width="1053" height="502" alt="image" src="https://github.com/user-attachments/assets/f8dcb46e-00be-4145-b07e-2b0b48487fe8" />

adicional quisiera mencionar que antes de interactuar con los repositorios de una cuenta github es necesario generar clavess o credenciales en jenkins para poder realizar actividades de clonado y resguardo de jenkinsfile

<img width="946" height="356" alt="image" src="https://github.com/user-attachments/assets/22865165-f192-4d09-b810-ef3795391583" />


4.- Requisitos técnicos para operar el flujo de integración y despliegue continuo
Para que el proceso automatizado funcione correctamente, es necesario cumplir con ciertos requisitos técnicos que aseguran la correcta interacción entre el entorno local del desarrollador, el repositorio GitHub y la instancia de Jenkins:
- Clonado del proyecto: El desarrollador debe contar con una copia local del repositorio, obtenida mediante el comando git clone.
- Herramienta de interacción con Git: Es indispensable tener instalado Git Bash u otra terminal compatible que permita ejecutar comandos Git desde el entorno local.
- Compilación y pruebas en servidor Jenkins: Dado que se trata de un proyecto desarrollado en Node.js, las etapas de compilación, ejecución de pruebas y demás fases del pipeline se realizan directamente en el servidor donde Jenkins fue configurado.
- Responsabilidad del desarrollador: El desarrollador únicamente debe encargarse de realizar cambios en el código y subirlos al repositorio mediante push. A partir de ese momento, el proceso se ejecuta de forma automática:
- Se detona el pipeline en Jenkins.
- Se clona el proyecto en el servidor Jenkins
- Se instalan dependencias.
- Se realiza Test unitarios.
- se compila.
- Se construye la imagen del aplicativo.
- La imagen se almacena en el repositorio de contenedores Docker hub
- Finalmente, se realiza el despliegue en el servicio correspondiente.

   <img width="485" height="478" alt="image" src="https://github.com/user-attachments/assets/2a00fe6d-f1c2-4e75-8ff0-34818dcf7c36" />

  <img width="941" height="273" alt="image" src="https://github.com/user-attachments/assets/85b0bf0d-9543-404a-bb68-52605ae2c1e8" />



