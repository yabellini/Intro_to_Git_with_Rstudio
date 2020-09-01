---
date: "2020-05-17"
draft: false
type: page
linktitle: Version Control. Primeros pasos de Git con R
summary: En este post introducimos los primeros pasos para usar Git con RStudio
title: Primeros pasos de Git con R
authors: 
    - admin
    - Marysol Gatti
type: post
weight: 1
tags: 
  - R-Ladies
  - Git
  - RStudio
---

Este post corresponde al meetup realizado en conjunto por los capítulos de R-Ladies Santa Rosa, R-Ladies General Pico y R-Ladies Buenos Aires realizado el 18 de Mayo sobre realizar primeros pasos en Git utilizando R.

El material presentado en este post tiene como fuente el libro [Happy Git and GitHub for the useR](https://happygitwithr.com/index.html) de [Jennifer Bryan](https://github.com/jennybc/happy-git-with-r)

## ¿Quién sos vos?

Cada lección debe ser pensada, organizada y generada para una audiencia en particular, esta es la persona en la que pensamos cuando preparamos este taller:

>*Romina* trabaja ordenando y analizando datos utilizando R para una variedad de clientes.  
Utiliza proyectos en RStudio para ordenar su trabajo.
Comparte sus avances y resultados utilizando herramientas en la nube (como dropbox y google drive).  
Compartir de esta manera le ha traído varios dolores de cabeza
Sabe que Git puede ayudarla con estos problemas pero no le queda claro como.
Tiene usuario en GitHub pero nunca usó.  
Quiere entender como funciona y como usarlo con R y RStudio para poder incorporarlo a sus proyectos.


## ¿Qué vamos a ver?

Este mapa conceptual presenta el contenido de este taller

   {{< figure src="/img/git_concept_map.png" alt="Mapa conceptual: El mapa conceptual presenta los conceptos que serán cubiertos durante el meetup.  Estos conceptos se presentan en cajas o círculos como sustantivos y las relaciones entre ellos por medio de flechas con verbos.  En nuestro caso el mapa conceptual se presenta el funcionamiento de Git: en tu computadora tienes RStudio IDE y un proyecto de RStudio, con un directorio de trabajo, que será el repositorio local de Git, al que podremos hacer Add de archivos a la Staging area, desde la cual podremos hacer Commit al repositorio local. Desde este repositorio local podemos hacer Push y Pull hacia el repositorio remoto que puede estar en GitHub.  Esta misma configuración está en la máquina de todos los colaboradores.">}}


## A usar Git desde RStudio

### Primera situación: Nuevo proyecto, GitHub primero

#### Paso 1: Hacer un repositorio en GitHub

Estos pasos se deben realizar sólo una vez por cada proyecto nuevo:

 * Ir a https://github.com y asegúrate de haber iniciado sesión.

 * Hacé clic en el botón verde "Nuevo repositorio" o, si estás en tu página de perfil, hacé clic en "Repositorios", luego haga clic en el botón verde "Nuevo".  complear con los siguientes datos:

  - Nombre del repositorio: MiRepo (o el nombre que quieras, pero que sea signficativo del proyecto que vas a realizar, que te ayude a recordar de que se trataba cuando lo veas en un tiempo)
    
  - Público
    
  - *SÍ* inicializa este repositorio con un archivo _README_

* Hacé clic en el botón verde grande "Crear repositorio".

Copia la URL HTTPS para clonar el repositorio mediante el botón verde "Clonar o descargar" (o copia la URL SSH si elegiste utilizar claves SSH).


#### Paso 2: Nuevo proyecto RStudio a través de git clone

* En RStudio, generar un nuevo proyecto:

   _File > New Project > Version Control > Git_ .En la "URL del repositorio", pegue la URL de su nuevo repositorio de GitHub. Será algo como esto https://github.com/nombreusuario/MiRepo.git.  Seleccionar _Open in new session_ y hacé clic en _Create Project_. Esto debería descargar el archivo README.md  que creamos en GitHub en el paso anterior. (pasos 1 a 5 de la siguiente figura). 
   
   {{< figure src="/img/git_githubfirst_new_project.png" alt="Pasos para crear un proyecto con control de versiones desde RStudio si ya existe el repositorio en GitHub">}}
    
  Cuando hacemos click en _Create Project_ se crea un nuevo directorio (carpeta), que cumplirá todas estas funciones:
  
  - un directorio o "carpeta" en su computadora
    
  - un repositorio de Git, vinculado a un repositorio de GitHub remoto
    
  - un proyecto de RStudio
 
El proyecto ya está listo para ser usando con control de versiones. 

En ausencia de otras restricciones, se sugiere que todos tus proyectos de R tengan exactamente esta configuración.

Hay una gran ventaja en el flujo de trabajo “GitHub primero, luego RStudio”: el repositorio de GitHub se agrega como remoto para tu repositorio local y tu _master local_ está ahora mirando los cambios de la _master en GitHub_. Este es un punto muy técnico pero importante sobre Git. La parte práctica es que ahora está configurado para hacer `pull` y `push`, sin necesidad de la linea de comandos.


### Segunda situación: Proyecto existente, GitHub primero

Si ya estás trabajando en R y no has utilizado Git esta debe ser tu situación: asumimos aquí que tienes tu proyecto R existente aislado en un directorio en tu computadora.  Para poder utilizar control de versiones vamos a repetir los pasos 1 y 2 explicados en la situación anterior.

#### Paso 3: Traer tu proyecto existente al proyecto con control de versiones

Usando tu método favorito para mover o copiar archivos, copia los archivos que constituyen tu proyecto existente en el directorio de este nuevo proyecto.

En RStudio, consulta el panel Git y el navegador de archivos: 

  * ¿Estás viendo todos los archivos? Deberían estar aquí si la copia/movida de archivos fue exitosa.
  * ¿Aparecen en el panel de Git con signos de interrogación? Deberían aparecer como nuevos archivos sin seguimiento.
  
Si las respuestas a estas preguntas es si, el proyecto local ya está con control de versiones y está asociado al repositorio remoto.  Hay u cuarto paso que permitirá actualizar ambos repositorios con todos los archivos del proyecto.

#### Paso 4: Stage y commit

Tenés que hacer _commit_ de tus archivos en este repositorio. ¿Cómo?

1. Hacé clic en la pestaña _Git_ en el panel superior derecho
2. Marca la casilla _Staged_ para todos los archivos que queres hacer _commit_.  Por defecto: ponerlo en _staged_ y reconsiderar cuando esto irá a GitHub.  Se puede mantener sin problemas uno o una serie de archivos localmente, sin hacer _commit_ al repositorio de Git y sin enviarlo a GitHub . Si no lo pasamos a _staged_ entonces no se tendrá en cuenta al momento de hacer los _commits_. Si se trata de una situación a largo plazo, o bien es un archivo que nunca será parte del respositorio, entonces hay que agregarlo en .gitignore. (Por jemplo: archivos de datos o archivos temporales)
3. Hacé clic en _Commit_
4. Escribe un mensaje en _Commit message_, como por jemplo: "Commit inicial del proyecto".
5. Hacé clic en _Commit_


## Usando el control de versiones

Ya vimos como funcionan algunos de las acciones de Git en el paso 4 de la segunda situación.  Ahora vamos a repasar todo el proceso desde el inicio.

### Realizar cambios locales, guardar, confirmar

Deberías hacer esto cada vez que termines una parte valiosa del trabajo, probablemente muchas veces al día.  No deberían ser espacios mayores a una hora.

Desde RStudio, vamos a modificar el archivo README.md, por ejemplo, agregando la línea "Esta es una línea desde RStudio". Guarda tus cambios.

Ahora vamos a confirmar estos cambios en el repositorio local. ¿Cómo?

  1. Hacé clic en la pestaña _Git_ en el panel superior derecho.
  2. Marca la casilla _Staged_ para los archivos que querramos gurdar (sean nuevos o modificados).
  3. Hacé clic en _Commit_.
  
   {{< figure src="/img/git_git_staged.png" alt="Agregar (add) un archivo a la Staged area y luego iniciar un Commit desde RStudio">}}
  
  
  4. Aparece una ventana emergente.  Escribe un mensaje en _Commit message_, como "Commit desde RStudio" y hacé clic en _Commit_.

{{< figure src="/img/git_commit_rstudio.png" alt="Realizar un Commit desde RStudio">}}

### Actualice (push) sus cambios locales a GitHub

Deberías hacer esto varias veces al día, pero menos veces que las que hacés _commit_.  En este momento tienes trabajo nuevo en tu repositorio local, pero los cambios aún no están en el repositorio remoto.

Ahora vamos a actualizar esos cambios del repositorio local al remoto. ¿Cómo?

  1.  Primero hacemos _Pull_ desde GitHub. Esto puede parecer contradictorio pero si realizaste cambios en el repositorio remoto desde la interfaz web o desde otra máquina o (un día) un colaborador ha realizado cambios, será mucho mas sencillo (y serás mucho más feliz) si traes esos cambios a tu repositorio local antes de enviar los tuyos haciendo _push_.  
  Para hacer _Pull_ presionamos la flecha azul en la pestaña Git en RStudio.  Lo más probable es que recibas un mensaje de que está todo actualizado (_Already up-to-date_).
  
  2. Hacé clic en el botón verde _Push_ para enviar tus cambios locales a GitHub. Puede ser que solicite el usuario y contraseña de github. Debería ver algún mensaje similar a la siguiente figura.
  
  {{< figure src="/img/git_push_rstudio.png" alt="Realizar un Push desde RStudio">}}
  

### Confirmando que el cambio local se actualizó en el repositorio remoto de GitHub
  
Para confirmar que el cambio que realizamos en RStudio se ecnuentra reflejado en el repositorio remoto, vamos a regresar al navegador a la página del repositorio en GitHub.  Si actualizamos, se debería ver la nueva linea de texto "Esta es una linea desde RStudio" en el archivo README.

Si haces clic en _commits_, debería ver un _commit_ con el mensaje "Commit from RStudio".  

### Hacer un cambio en GitHub

1. Hacé clic en README.md en el listado de archivos en GitHub.

2. En la esquina superior derecha, hacé clic en el lápiz para editar el archivo.

3. Agrega una línea de texto a este archivo, como por ejemplo: "Línea agregada desde GitHub".

4. Edita el mensaje de commit en _Commit changes_ o acepta el valor predeterminado.

5. Hacé clic en el gran botón verde _Commit changes_.

### Pull desde GitHub

1. De vuelta en RStudio localmente ...

2. Revisa tu archivo README.md, *NO* debe tener la línea "Línea agregada desde GitHub". Debería estar igual a como lo dejaste. Verificalo.

3. Hacé clic en el botón azul _Pull_.

4. Revisa README.md nuevamente. Ahora debería ver la nueva línea allí.

Y eso es todo...solamente se debe repetir este patrón. Siempre intenta tener los dos repositorios: local y remoto, sincronizados. Recuerda que es recomendable siempre hacer un _Pull_ antes de intentar hacer _Push_ con nuestros cambios.

## ¿Cómo seguimos?

Primero te dejamos [aqui acceso a la presentación del meetup](https://docs.google.com/presentation/d/1rDWruJpZPHVSCeypC_sgNYaArTzxvmFbRxum-lCuSmA/edit?usp=sharing) donde hay más datos de como utilizar Git desde la consula.  Estos son solos los primeros pasos y hay mucho mas para conocer sobre el funcionamiento del control de versiones.

Recomendamos leer el libro [Happy Git and GitHub for the useR](https://happygitwithr.com/index.html) de [Jennifer Bryan](https://github.com/jennybc/happy-git-with-r) en el que se basa gran parte de este tutorial.

Y por supuesto prestar atención a los nuevos meetups de R-Ladies!

