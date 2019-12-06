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

En este documento utilizaremos una escala del 1 al 5 para definir la prioridad de una característica, siendo 1 la mayor prioridad y 5 la menor.


### 1.3 Audiencia objetivo

Este documento tiene como público objetivo a ingenieros de software. En este sentido es importante que el documento logre claridad y completez en la definicíon de las especificaciones del sistema.


### 1.4 Scope del producto

El sistema debe ser desplegado para toda la comunidad estudiantil del itam. Conforme a esto, debe poder atender los pedidos de los usuarios. Además, debe permitir la visualización de los artículos para lograr los objetivos anteriores.

## 2 Descripción general

### 2.1	Perspectiva del producto

RAPPITAM es una app que permite a los alumnos y personal de ITAM pedir comida a las instalaciones de Río Hondo.

### 2.2 Funciones del producto

A continuación se presenta una breve descripción de las funcionalidades generales del producto.

- Registro de usuarios
El usuario es capaz de registrarse en el sistema para iniciar a hacer pedidos.
- Login de usuarios
El usuario es capaz de ingresar al sistema con correo y contraseña porsteriormente a su registro.
- Visualización de Comercios
El usuario debe de ser capaz de ver los comercios disponibles.
- Visualización de oferta de productos en los locales.
El usuario debe de ser capaz de visualizar sus opciones para saber que pedir.
- Crear un pedido
El usuario debe de crear un pedido de lo que desea de cada local.
-Realizar un pago
El usuario debe ser capaz de pagar pera que se le entregue el pedido.
- Configuración de perfil
El usuario debe de ser capaz de modificar la información básica de su perfil

### 2.3 Usuarios y características

A continuación se presenta una breve descripción de los usuarios que van a interactuar con el producto

- Estudiantes del ITAM
Los estudiantes en el ITAM que no pueden salir de clases y su horario es establecido por control escolar, que pueden necesitar pedir algo de comer entregado a su clase.

### 2.4 Ambiente operativo

Para el proyecto vamos a utilizar una intancia T2 Micro de AWS. Las instancias T2 son tipos de instancias de Amazon EC2 diseñadas para disminuir radicalmente los costos de las aplicaciones que se benefician de la capacidad para ampliarse para alcanzar el rendimiento pleno de los núcleos cuando resulta necesario. Las instancias T2 se pueden usar en la capa gratuita de AWS, que incluye 750 horas de instancias t2.micro de Linux y Windows al mes durante un año para clientes nuevos de AWS.

El sistema operativo a utilizar es Linux.

### 2.6 Arquitectura

Para poder definir la arquitectura de RAPPITAM es importante que recapitulemos algunos de las restricciones a las que estará sujeta la aplicación. 

En primer lugar, el desarrollo de RAPPITAM se lleva a cabo por un equipo pequeño de ingenieros que deberan tener la capacidad de  trabajar tanto en el back como en el front. Buscamos priorizar la simplicidad de la arquitectura para asegurar que los ingenieros puedan trabajar en distintas partes del código con facilidad. Por las mismas razones, es impotante que la arquitectura se componga de un sólo stack tecnologico.

En segundo lugar, el primer mercado objetivo de la aplicación son los estudiantes del ITAM, que cuenta con una matricula de 5,500 estudiantes en el presente. Aunque exista la posibilidad futura de expandirse a otras escuelas, el scope de este proyecto debe enfocarse a satisfacer la carga actual únicamente. Es importante que el desarrollo se lleve a cabo de forma ágil, pues no se descarta que sea necesario iterar la funcionalidad actual y una solución "over-engineered" puede entorpecer la velocidad del desarrollo.

Tomando encuenta los dos puntos anteriores, consideramos que una arquitectura monolítica es la mejor opción para este proyectos por las siguientes razones. Primero, la simplicidad de esta arquitectura permitirá que los ingenieros entiendan como funciona el sistema en conjunto y les permitirá ser útiles en distintos módulos de la aplicación. En segundo lugar, un monolíto asegurará que la tecnología utilizada es uniforme y que, una vez que los ingenieros se adecuen a la tecnología elegida, no habrá curvas de aprendizaje que tomar en cuenta al transitar el código. Por último, la arquitectura monolítica será capaz de atender la carga de alumnos del itam con el conocimiento de que la matricula se mantiene constante año con año y con la posibilidad de replicar el backend con tecnología de contenedores si es que fuera necesario.

<img src="https://i.ibb.co/JzcTJpm/Web-App-Reference-Architecture-2.png">

### 2.7 Suposiciones y dependencias

Se asume que la base de datos existe y se puede manejar.
Se trabaja considerando que las conexiones a las APIs de Facebook, Google y el servicio de pago están implementadas

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
Un botón Cuenta, que envía a la pantalla de Configuración de Cuenta.

Prioridad: 3

#### 4.3.2 Secuencias de estímulo y respuesta

Al hacer click en el botón de búsqueda se despliegan en la lista los restaurantes que coincidadn con la búsqueda en su nombre o algún producto que vendan.
Al arrastrar la lista hacia arriba o abajo se deslizará mosrtrando más opciones.
Al hacer click en un Restaurante se abrirá la Vista del restaurante correspondinte.
Al hacer clck en el botón "Continuar" se pasará a la pantalla de Pedido.
Al hacer clck en el botón "Cuenta" se pasará a la pantalla de Configuración de cuenta.

#### 4.3.3 Requerimientos funcionales

##### Requerimiento 1

Un scroll panel en el que se muestren los comercios disponibles con una imagen, nombre y calificación.

##### Requerimiento 2

Una caja te texto para búsqueda y un botón que al ser pesionado envía un querry a la base de datos y despliega los restaurantes resultantes en el panel, o un mensaje indicando que la búsqueda no obtuvo resultados.

##### Requerimiento 3

Una barra en el fondo en la que se ve el Monto Actual.

##### Requerimiento 4

Un botón "Continuar" junto al monto que al ser presionado muestra la pantalla de pedido.

##### Requerimiento 5

Al presionar el botón Cuenta, se cambiará a la pantalla Configuración de Cuenta.

### 4.4 Vista de restaurante

#### 4.4.1 Descripción y prioridad

En esta pantalla se muestra una lista con todos los artículos disponibles en el comercio respectivo, mostrando su nombre, precio, una pequeña descripción y un botón para agregar uno al pedido.
Hay un botón para volver al Marketplace.
En la parte inferior de la pantalla se hay una barra en la que se despliega en el Monto Actual y un botón para pasar al pedido.
Un botón Cuenta, que envía a la pantalla de Configuración de Cuenta.

Prioridad: 4

#### 4.4.2 Secuencias de estímulo y respuesta

Al hacer click en el botón de agrgar en un artículo se agrega uno del mismo al Pedido, incrementando el Monto Actual.
Al arrastrar la lista hacia arriba o abajo se deslizará mosrtrando más opciones.
Al hacer click en el botón de regresar, se pasará a la pantalla del Msrketplace.
Al hacer clck en el botón "Continuar" se pasará a la pantalla de Pedido.
Al hacer clck en el botón "Cuenta" se pasará a la pantalla de Configuración de cuenta.

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

##### Requerimiento 6

Al presionar el botón Cuenta, se cambiará a la pantalla Configuración de Cuenta.

### 4.5 Hacer Pedido

#### 4.5.1 Descripción y prioridad

En esta pantalla se muestra una lista con todos los artículos en el Pedido, mostrando su nombre, cantidad, precio y un botón para eliminar; y el total.
Hay un botón para volver al Marketplace.
Una lista con las tarjetas guardadas para elegir con cual se realizará el pago, por default la última que se usó.
Un botón para agregar tarjeta.
Un botón "Ordenar" para comfirmar la compra, que mostrará un mensaje de éxito si se realiza el pago, o uno de error.
Un botón Cuenta, que envía a la pantalla de Configuración de Cuenta.

Prioridad: 1

#### 4.5.2 Secuencias de estímulo y respuesta

Al hacer click en el botón de Ordenar, se realizará la transacción; de ser exitosa se le indicará al usuario y se iniciará el Pedido; de lo contrario se desplegará un mensaje de erro y pasará a la pantalla de Markentplace. 
Al hacer click en el botón de regresar, se pasará a la pantalla del Msrketplace.
Al hacer click en el botón de eliminar en un artículo se elimina del Pedido, y actualiza el Monto Actual.
Al hacer click en el botón de Agregar tejreta, se pasará a la pantalla de Métodos de Pago.
Al hacer clck en el botón "Cuenta" se pasará a la pantalla de Configuración de cuenta.

#### 4.5.3 Requerimientos funcionales

##### Requerimiento 1

Una lista en la que se muestren los artículos con nombre, precio, cantidad y un botón "-"; y el total del Monto Actual.

##### Requerimiento 2

Al hacer click en eliminar un Artículo éste se elimina del Pedido, y su precio se resta del Monto Actual.

##### Requerimiento 3

Al hacer click en el botón Ordenar, si no hay una tarjeta seleccionada, se pasará a la pantalla Métodos de Pago.

##### Requerimiento 4

Un botón Ordenar que, si hay una tarjeta seleccionada, se conecta con el servicio de pago con la transacción, si es exitosa lo reporta al usuario y activa el Pedido, si no muesrta un mensaje de error y pasa a la pantalla de Marketplace.

##### Requerimiento 5

Al hacer click en el botón Regresar se pasará a la pantalla de Marketplace.

##### Requerimiento 6

Al presionar el botón Cuenta, se cambiará a la pantalla Configuración de Cuenta.

### 4.6 Métodos de pago

#### 4.6.1 Descripción y prioridad

Una lista con las tarjetas aceptadas.
Cuatro cajas de texto, para el número de tarjeta, nombre, fecha de vencimiento y ccv.
Un botón Agregar tarjeta, que agregará la tarjeta a la cuenta del usuario, y lo redirigirá a la pantalla de MArketplace.
Un botón de regresar, que envía a la pantalla de Msrketplace.

Prioridad: 5

#### 4.6.2 Secuencias de estímulo y respuesta

Al hacer click en Agregar tarjeta se valida la tarjeta, se guarda y se pasa a la pantalla de Mrketplace si la validacion es exitosa, si no se muestra un error al usuario.
Al hacer click en el botón de regresar, se pasará a la pantalla del Msrketplace.

#### 4.6.3 Requerimientos funcionales

##### Requerimiento 1

Al hacer click en el botón Agregar tarjeta se valida que los campos no estén vacíos y de ser así desplegará un mesaje pidiendo que se completen los datos.

##### Requerimiento 2

Al hacer click en el botón Agregar tarjeta se conecta con el servicio de pago y valida los datos, de haber un error lo indicará al usuario, de lo contrario gusrdará la tarjeta en la cuanta y pasará a la pantalla de Marketplace.

##### Requerimiento 3

Al hacer click en el botón Regresar se pasará a la pantalla de Marketplace.

### 4.7 Configuración de cuenta

#### 4.7.1 Descripción y prioridad

En esta pantalla se muestra la información de la cuenta del usuario.
Hay un botón de volver que envía a la pantalla de Marketplace.
Hay un botón Eliminar cuenta, para borrar la cuenta de la base de datos.
Hay un botón Reestablecer contraseña, que dirige a la pantalla de recuperación de contraseña.

Prioridad: 5

#### 4.7.2 Secuencias de estímulo y respuesta

Al hacer click en Eliminar cuenta aparece un pop-up con una caja de texto para la contraseña y el botón Confirmar Baja
Al hacer click en Confirmar Baja, si la contraseña ingresada es correcta, se eliminará la cuenta.
Al hacer click en el botón de regresar, se pasará a la pantalla del Msrketplace.
Al hacer click en el botón de reestablecer contraseña, se pasará a la pantalla de recuperación de contraseña.

#### 4.7.3 Requerimientos funcionales

##### Requerimiento 1

Un panel con la información de la cuenta: correo, número de pedidos, tarjetas asociadas.

##### Requerimiento 2

Un botón Eliminar cuenta que al ser presionado muestra un pop-up con una caja de texto para la contraseña y el botón Confirmar baja.

##### Requerimiento 3

Al hacer click en el botón Confirmar baja valida que la contraseña ingresada sea la correcta, de ser así se eliminará la informacion de la cuenta de la base de datos y se mostrará la pantalla de Registro.

##### Requerimiento 4

Al hacer click en el botón Regresar se pasará a la pantalla de Marketplace.

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
Hagamos un análisis a profundidad de cada uno de los pasos de este pipeline de desarrollo:

- *Commit/build*

En este paso algún developer hace commit y push de sus cambios en código, asumiendo que el equipo tiene una metodología de administración de las tasks por hacer y cada cuando hacer push. El sistema automaticamente registra el commit y recibe la información para ver que la solución continúe íntegra. 

- *Testing*

Para mantener una solución íntegra el sistema corre las pruebas asociadas a los archivos de testing que se hayan definido para ver que ninguno de los cambios rompa algún assert o funcionalidad que se espera se mantenga. Esto permite que automaticamente se evite integrar los cambios antes de que rompa algo de la solución. En caso de que las pruebas sean cumplidas pasa al siguiente eslabón en la cadena.

- *Staging*

Una vez que los cambios aprueban los tests definidos entra en un ambiente de staging donde tenemos una versión del producto muy similar a la que el consumido final podrá acceder. Se hace una revisión manual por parte de alguno de los integrantes del equipo para validar que los cambios cumplen con las expectativas deseadas o los cambio deseados. Si es que 

- *Deploy*

Una vez que haya sido aprobada pasa a producción para que los nuevos cambios puedan ser utilizados por parte de los clientes.
## Otros requerimientos
