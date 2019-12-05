# RAPPITAM
RAPPITAM es una app que permite a los alumnos y personal de ITAM pedir comida a las instalaciones de Río Hondo.

## Arquitectura

Para poder definir la arquitectura de RAPPITAM es importante que recapitulemos algunos de las restricciones a las que estará sujeta la aplicación. 

En primer lugar, el desarrollo de RAPPITAM se lleva a cabo por un equipo pequeño de ingenieros que deberan tener la capacidad de  trabajar tanto en el back como en el front. Buscamos priorizar la simplicidad de la arquitectura para asegurar que los ingenieros puedan trabajar en distintas partes del código con facilidad. Por las mismas razones, es impotante que la arquitectura se componga de un sólo stack tecnologico.

En segundo lugar, el primer mercado objetivo de la aplicación son los estudiantes del ITAM, que cuenta con una matricula de 5,500 estudiantes en el presente. Aunque exista la posibilidad futura de expandirse a otras escuelas, el scope de este proyecto debe enfocarse a satisfacer la carga actual únicamente. Es importante que el desarrollo se lleve a cabo de forma ágil, pues no se descarta que sea necesario iterar la funcionalidad actual y una solución "over-engineered" puede entorpecer la velocidad del desarrollo.

Tomando encuenta los dos puntos anteriores, consideramos que una arquitectura monolítica es la mejor opción para este proyectos por las siguientes razones. Primero, la simplicidad de esta arquitectura permitirá que los ingenieros entiendan como funciona el sistema en conjunto y les permitirá ser útiles en distintos módulos de la aplicación. En segundo lugar, un monolíto asegurará que la tecnología utilizada es uniforme y que, una vez que los ingenieros se adecuen a la tecnología elegida, no habrá curvas de aprendizaje que tomar en cuenta al transitar el código. Por último, la arquitectura monolítica será capaz de atender la carga de alumnos del itam con el conocimiento de que la matricula se mantiene constante año con año y con la posibilidad de replicar el backend con tecnología de contenedores si es que fuera necesario.
