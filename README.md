# Especificación de requerimientos de software
## Para el sistema RAPPITAM
Version 1.0  

Preparado por Alessandro, Sebastian Gonzales and Andrés Cruz  

42-Rapitam

6 Diciembre 2019





# Tabla de contenidos

1. [Introducción](#introducción)
2. [Descripción general](#descripción-general)
3. [Requerimientos de interfaz externa](#requerimientos-de-interfaz-externa)
4. [Características del sistema](#características-del-sistema)
5. [Requerimientos no funcionales](#requerimientos-no-funcionales)
6. [Plan de calidad](#plan-de-calidad)
7. [Otros requerimientos](#otros-requerimientos)

## 1.Introducción
### 1.1 Proposito

### 1.2 Convenciones del documento

En este documento utilizaremos una escala del 1 al 5 para definir el tamaño de un feature.


### 1.3 Audiencia objetivo

Este documento tiene como público objetivo a ingenieros de software. En este sentido es importante que el documento logre claridad y completez en la definicíon de las especificaciones del sistema.


### 1.4 Scope del producto

El sistema debe ser desplegado para toda la comunidad estudiantil del itam. Conforme a esto, debe poder atender las peticiones de alta y baja de materias así como las listas de espera. Además, debe permitir la visualización de los cursos para lograr los objetivos anteriores.



## 2 Descripción general

### 2.1	Perspectiva del producto

RAPPITAM es una app que permite a los alumnos y personal de ITAM pedir comida a las instalaciones de Río Hondo.

### 2.2 Funciones del producto

A continuación se presenta una breve descripción de las funcionalidades generales del producto.

- Registro de usuarios
El usuario es capaz de registrarse en el sistema para iniciar a administrar sus materias.
- Login de usuarios
El usuario es capaz de ingresar al sistema con correo y contraseña porsteriormente a su registro.
- Alta de materias
El usuario debe de ser capaz de dar de alta sus materias.
- Actualización de materias
El usuario debe de ser capaz de actualizar sus materias.
- Eliminación de materias
El usuario debe de ser capaz de dar de baja sus materias.
- Configuración de perfil
El usuario debe de ser capaz de modificar la información básica de su perfil

### 2.3 Usuarios y características

A continuación se presenta una breve descripción de los usuarios que van a interactuar con el producto

- Estudiantes de nuevo ingreso
Nuevos estudiantes en el ITAM, están por cursar su primer semestre en el ITAM y su horario es establecido por control escolar.
- Estudiantes por egresar
Estudiantes que no son de primer ingreso, y siguen avanzando en su carrera en el ITAM

### 2.4 Ambiente operativo

Para el proyecto vamos a utilizar una intancia T2 Micro de AWS. Las instancias T2 son tipos de instancias de Amazon EC2 diseñadas para disminuir radicalmente los costos de las aplicaciones que se benefician de la capacidad para ampliarse para alcanzar el rendimiento pleno de los núcleos cuando resulta necesario. Las instancias T2 se pueden usar en la capa gratuita de AWS, que incluye 750 horas de instancias t2.micro de Linux y Windows al mes durante un año para clientes nuevos de AWS.

El sistema operativo a utilizar es Linux.

### 2.5 Restricción de diseño e implementación
### 2.6 Arquitectura

Para poder definir la arquitectura de RAPPITAM es importante que recapitulemos algunos de las restricciones a las que estará sujeta la aplicación. 

En primer lugar, el desarrollo de RAPPITAM se lleva a cabo por un equipo pequeño de ingenieros que deberan tener la capacidad de  trabajar tanto en el back como en el front. Buscamos priorizar la simplicidad de la arquitectura para asegurar que los ingenieros puedan trabajar en distintas partes del código con facilidad. Por las mismas razones, es impotante que la arquitectura se componga de un sólo stack tecnologico.

En segundo lugar, el primer mercado objetivo de la aplicación son los estudiantes del ITAM, que cuenta con una matricula de 5,500 estudiantes en el presente. Aunque exista la posibilidad futura de expandirse a otras escuelas, el scope de este proyecto debe enfocarse a satisfacer la carga actual únicamente. Es importante que el desarrollo se lleve a cabo de forma ágil, pues no se descarta que sea necesario iterar la funcionalidad actual y una solución "over-engineered" puede entorpecer la velocidad del desarrollo.

Tomando encuenta los dos puntos anteriores, consideramos que una arquitectura monolítica es la mejor opción para este proyectos por las siguientes razones. Primero, la simplicidad de esta arquitectura permitirá que los ingenieros entiendan como funciona el sistema en conjunto y les permitirá ser útiles en distintos módulos de la aplicación. En segundo lugar, un monolíto asegurará que la tecnología utilizada es uniforme y que, una vez que los ingenieros se adecuen a la tecnología elegida, no habrá curvas de aprendizaje que tomar en cuenta al transitar el código. Por último, la arquitectura monolítica será capaz de atender la carga de alumnos del itam con el conocimiento de que la matricula se mantiene constante año con año y con la posibilidad de replicar el backend con tecnología de contenedores si es que fuera necesario.


### 2.7 Suposiciones y dependencias

## Requerimientos de interfaz externa
## 4 Características del sistema

### 4.1 Registrarse en el sistema

#### 4.1.1 Descripción y prioridad

En la parte superior de la pantalla hay botones para cambiar entre las pantallas de autentificaión y registro.
El usuario ingresa un e-mail, contraseña y la confirmación de contraseña, es validado y manda un mensaje de error, o un mensaje de éxito y procede al Marketplace.
Hay un botón con la opción de iniciar sesión con Facebook.
Hay un botón con la opción de iniciar sesión con Google.

Prioridad: 3

#### 4.1.2 Secuencias de estímulo y respuesta

El botón "SIGN UP" está deshabilitado.
Al hacer click en el boton "SIGN IN" se redirigirá a la página de autentificación.
En la pantalla hay 3 cajas de texto donde el usuario ingresará su e-mail, una contraseña y la confirmación de su contraseña, al hacer click en el botón de "Registrarme" el sistema valida la informacíon ingresada y de ser correcta manda un mensaje de éxito y redirige a la página de el Marketplace, de lo contrario muestra un mensaje de error de autentificación.
Al hacer click en "Log in con Facebook" se iniciará la sesión con Facebook y pasará a la página de marketplace.
Al hacer click en "Log in con Google" se iniciará la sesión con Google y pasará a la página de marketplace.

#### 4.1.3 Requerimientos funcionales

##### Requerimiento 1

Al hacer click en el botón "Registrarme" el sistema valida que los campos no estén vacíos, de ser así desplegará un mensaje pidiendo que se proporcione la información reqerida.

##### Requerimiento 2

Si los campos no están vaciós, el sistema valida que el e-mail no exista en la base de datos, si existe despliega un mensaje de error; de otro modo verifica que ambas contraseñas sean iguales, si no lo son despliega un mensaje de error, en caso conrario guarda la nueva cuenta en la base de datos y redirige al usuario a la página de Marketplace.

##### Requerimiento 3

Al hacer click en el botón "Log in con Facebook" el sistema se conecta con la API de la aplicación de Facebook para iniciar sesión a travez de ella y proceder a la página de Marketplace.

##### Requerimiento 4

Al hacer click en el botón "Log in con Google" el sistema se conecta con la API de Google para iniciar sesión a travez de ella y proceder a la página de Marketplace.

##### Requerimiento 5

Al hacer click en el botón "SIGN IN" el sistema pasará a la pantalla de autentificación.


### 4.2 Módulo de autentificación

#### 4.2.1 Descripción y prioridad

En la parte superior de la pantalla hay botones para cambiar entre las pantallas de autentificaión y registro.
El usuario ingresa su e-mail y contraseña, es validado y manda un mensaje de error o procede al Marketplace.
Hay un botón con la opción de iniciar sesión con Facebook.
Hay un botón con la opción de iniciar sesión con Google.
Hay un botón para reestablcer la contraseña.

Prioridad: 2

#### 4.2.2 Secuencias de estímulo y respuesta

Al hacer click en el boton "SIGN UP" se redirigirá a la página de registro.
El botón "SIGN IN" está deshabilitado.
En la pantalla hay 2 cajas de texto donde el usuario ingresará su e-mail y contraseña, al hacer click en el botón de "Continue" el sistema valida la informacíon ingresada y de ser correcta redirige a la página de el Marketplace, de lo contrario muestra un mensaje de error de autentificación.
Al hacer click en "Log in con Facebook" se iniciará la sesión con Facebook y pasará a la página de marketplace.
Al hacer click en "Log in con Google" se iniciará la sesión con Google y pasará a la página de marketplace.
Al hacer click en el botón "Recuperar contraseña" se redirigirá a la página de reestablecer contraseña.

#### 4.2.3 Requerimientos funcionales

##### Requerimiento 1

Al hacer click en el botón "Continuar" el sistema valida que los campos de e-mail y contraseña no estén vacíos, de ser así desplegará un mensaje pidiendo que se proporcione la información reqerida.

##### Requerimiento 2

Si los campos no están vaciós, el sistema valida la información con la base de datos, si la validación falla despliega un mensaje de error, de otro modo guarda la sesión y redirige al usuario a la página de Marketplace.

##### Requerimiento 3

Al hacer click en el botón "Log in con Facebook" el sistema se conecta con la API de la aplicación de Facebook para iniciar sesión a travez de ella y proceder a la página de Marketplace.

##### Requerimiento 4

Al hacer click en el botón "Log in con Google" el sistema se conecta con la API de Google para iniciar sesión a travez de ella y proceder a la página de Marketplace.

##### Requerimiento 5

Al hacer click en el botón "Recuperar" el sistema redirigirá al usuario a la página de reestablecimiento de contraseñas.

##### Requerimiento 6

Al hacer click en el botón "SIGN UP" el sistema pasará a la pantalla de registro.

### 4.3 Marketplace

#### 4.3.1 Descripción y prioridad

En esta pantalla se muestra una lista con todos los restaurantes y tiendas cercanas al ITAM, mostrando su nombre y rating.
Hay una barra de búsqueda
En la parte inferior de la pantalla se hay una barra en la que se despliega enl Monto Actual y un botón para pasar al pedido.

Prioridad: 3

#### 4.3.2 Secuencias de estímulo y respuesta

Al hacer click en el botón de búsqueda se despliegan en la lista los restaurantes que coincidadn con la búsqueda en su nombre o algún producto que vendan.
Al arrastrar la lista hacia arriba o abajo se deslizará mosrtrando más opciones.
Al hacer click en un Restaurante se abrirá la Vista del restaurante correspondinte.
Al hacer clck en el botón "Continuar" se pasará a la pantalla de Pedido.

#### 4.3.3 Requerimientos funcionales

##### Requerimiento 1

Un scroll panel en el que se muestren los comercios disponibles con una imagen, nombre y calificación.

##### Requerimiento 2

Una caja te texto para búsqueda y un botón que al ser pesionado envía un querry a la base de datos y despliega los restaurantes resultantes en el panel, o un mensaje indicando que la búsqueda no obtuvo resultados.

##### Requerimiento 3

Una barra en el fondo en la que se ve el Monto Actual.

##### Requerimiento 4

Un botón "Continuar" junto al monto que al ser presionado muestra la pantalla de pedido.

### 4.4 Vista de restaurante

#### 4.4.1 Descripción y prioridad

En esta pantalla se muestra una lista con todos los artículos disponibles en el comercio respectivo, mostrando su nombre, precio, una pequeña descripción y un botón para agregar uno al pedido.
Hay un botón para volver al Marketplace.
En la parte inferior de la pantalla se hay una barra en la que se despliega en el Monto Actual y un botón para pasar al pedido.

Prioridad: 4

#### 4.4.2 Secuencias de estímulo y respuesta

Al hacer click en el botón de agrgar en un artículo se agrega uno del mismo al Pedido, incrementando el Monto Actual.
Al arrastrar la lista hacia arriba o abajo se deslizará mosrtrando más opciones.
Al hacer click en el botón de regresar, se pasará a la pantalla del Msrketplace.
Al hacer clck en el botón "Continuar" se pasará a la pantalla de Pedido.

#### 4.4.3 Requerimientos funcionales

##### Requerimiento 1

Un scroll panel en el que se muestren los artículos disponibles con una imagen, nombre, precio, pequeña descripción y un botón "+".

##### Requerimiento 2

Al hacer click en un Artículo éste se agrega al Pedido, y su precio se suma al Monto Actual.

##### Requerimiento 3

Una barra en el fondo en la que se ve el Monto Actual.

##### Requerimiento 4

Un botón "Continuar" junto al monto que al ser presionado muestra la pantalla de pedido.

##### Requerimiento 5

Al hacer click en el botón Regresar se pasará a la pantalla de Marketplace.

### 4.5 Hacer Pedido

#### 4.5.1 Descripción y prioridad

En esta pantalla se muestra una lista con todos los artículos en el Pedido, mostrando su nombre, cantidad, precio y un botón para eliminar; y el total.
Hay un botón para volver al Marketplace.
Una lista con las tarjetas guardadas para elegir con cual se realizará el pago.
Un botón para agregar tarjeta.
Un botón "Ordenar" para comfirmar la compra, que mostrará un mensaje de éxito si se realiza el pago, o uno de error.

Prioridad: 1

#### 4.5.2 Secuencias de estímulo y respuesta

Al hacer click en el botón de Ordenar, se realizará la transacción; de ser exitosa se le indicará al usuario y se iniciará el Pedido; de lo contrario se desplegará un mensaje de erro y pasará a la pantalla de Markentplace. 
Al hacer click en el botón de regresar, se pasará a la pantalla del Msrketplace.
Al hacer click en el botón de eliminar en un artículo se elimina del Pedido, y actualiza el Monto Actual.

#### 4.5.3 Requerimientos funcionales

##### Requerimiento 1

Una lista en la que se muestren los artículos con nombre, precio, cantidad y un botón "-"; y el total del Monto Actual.

##### Requerimiento 2

Al hacer click en eliminar un Artículo éste se elimina del Pedido, y su precio se resta del Monto Actual.

##### Requerimiento 3

Un botón Ordenar que se conecta con el servicio de pago con la transacción, si es exitosa lo reporta al usuario y activa el Pedido, si no muesrta un mensaje de error y pasa a la pantalla de Marketplace.

##### Requerimiento 4

Al hacer click en el botón Regresar se pasará a la pantalla de Marketplace.

### 4.6 Hacer Pedido

#### 4.6.1 Descripción y prioridad

#### 4.6.2 Secuencias de estímulo y respuesta

#### 4.6.3 Requerimientos funcionales

##### Requerimiento 1

##### Requerimiento 2

##### Requerimiento 3

## 5.Requerimientos no funcionales
### 5.1 Requerimientos de rendimiento
El sistema debe ser capaz de atender las peticiones de los alumnas en su máxima carga. En los 3 días que los alumnos se inscriben, el sistema debe tener poca latencia y disponibilidad del 100%;
### 5.2 Requerimientos de seguridad

La cuenta de cada alumno solo debe poder ser accedida por el mismo. Es muy importante asegurar el proceso de autenticación puesto que fallar en este aspecto puede tener consecuencias negativas para el alumno. Así mismo, ningun alumno debe poder acceder información que no le corresponda


### 5.3 Reglas del negocio
Cada alumno puede visualizar todos los cursos, pero no le debe ser posible dar de alta materias que no pertenezcan a su plan de estudios o que se den en un horario que choque con una materia previamente seleccionada. Así mismo, cada alumno tiene un límite de materias que puede inscribir definido por su carga académica.

#6.Plan de calidad

##6.1 CI/CD

El temrmino CI/CD es un acrónimo para "Continous Integration / Continous Delivery", define la implementación de un pipeline de desarrollo para poder mantener la integridad del producto al añadir nuevas funcionalidades o corregir bugs identificados dentro de la misma.

A coontinuación vemos un ejemplo de un pipeline implemetado con tecnologías líderes en el mercado:

<center><img src="https://image.slidesharecdn.com/cicdwithjenkinsanddocker1-160815013911/95/cicd-with-jenkins-and-docker-devops-meetup-day-thailand-7-638.jpg?cb=1471229320"></center>
##6.2 Monitoreo de la plataforma
##6.3 Administración de tickets

## Otros requerimientos
