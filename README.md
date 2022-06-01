# Estadia2
CURSO TÉCNICAS  Y METODOLOGIAS EN GENÉTICA


## Semana 1, comando basicos y como hacer un repositorio
Guiandome con el tutorial https://docs.github.com/es/get-started/quickstart/hello-world y siguiendo las unidades desde https://github.com/u-genoma/wksp2019.


### Unidad 1, Línea de comando
Mediante la utilización de Ubuntu se probaron comandos descritos en la "Unidad 1" del repositorio BioinfinvRepro año 2018. Comandos tales como:
- `pwd`   para poder conocer la ruta del directorio en el que actualmente estamos
- `ls`    para poder conocer los archivos y carpetas que estan dentro de un directorio
- `mkdir` para crear una carpeta
- `cd`    para poder entrar a una carpeta
- `cd ..` para poder volver a la carpeta anterior
- `echo`  para podes imprimir en pantalla un mensaje
- `cp`    para copiar archivos
- `less`  para ver archivos de manera compaginada
- `more`  para mostrar una parte de los archivos
- `cat` para ver el archivo completo sin compaginar o concatenar 2 archivos distintos en un tercero

Una vez dominado estos comandos basicos se procedio a clonar el repositorio del curso Workshop 2019 usando el comando `$ git clone https://github.com/u-genoma/wksp2019.git`, como resultado se obtuvo:
```{bash}
Clonando en 'wksp2019'...
warning: redirigiendo a https://github.com/u-genoma/wksp2019.git/
remote: Enumerating objects: 270, done.
remote: Total 270 (delta 0), reused 0 (delta 0), pack-reused 270
Recibiendo objetos: 100% (270/270), 7.77 MiB | 13.53 MiB/s, listo.
Resolviendo deltas: 100% (102/102), listo.
```

Dentro de la carpeta creada wksp2019 y para saber el estatus del repositorio se utilizo el comando `$ git status`, obteniendo como resultado:
```{bash}
En la rama master
Tu rama está actualizada con 'origin/master'.

nada para hacer commit, el árbol de trabajo está limpio
```

Para agregar un archivo que no se encontraba en el repositorio se utilizo `$ touch ejemplo.txt` , seguido de `$ git status` para comprobar el estado de este, obteniendo:

```{bash}
En la rama master
Tu rama está actualizada con 'origin/master'.

Archivos sin seguimiento:
  (usa "git add <archivo>..." para incluirlo a lo que se será confirmado)
	ejemplo.txt

no hay nada agregado al commit pero hay archivos sin seguimiento presentes (usa "git add" para hacerles seguimiento)
```

Posteriomente se agrego add como `$ git add ejemplo.txt` y se volvio a comprobar con `$ git status`, obteniendo el nuevo estatus del archivo nuevo agregado:

```{bash}
En la rama master
Tu rama está actualizada con 'origin/master'.

Cambios a ser confirmados:
  (usa "git restore --staged <archivo>..." para sacar del área de stage)
	nuevo archivo:  ejemplo.txt
```

Se trato se agregar los cambios al branch usando el comando `git commit -m "agregar archivo ejemplo"`, pero se obtuvo el siguiente mensaje de error:


```{bash}
*** Por favor cuéntame quien eres.

Corre

  git config --global user.email "you@example.com"
  git config --global user.name "Tu Nombre"

para configurar la identidad por defecto de tu cuenta.
Omite --global para configurar tu identidad solo en este repositorio.

fatal: no es posible auto-detectar la dirección de correo (se obtuvo 'dinka@dinka-System-Product-Name.(none)')
```

Como no se pudo unir los cambios al branch que se esta utilizando se siguio trabajando con los siguientes comandos `echo "Hola Mundo" > ejemplo.txt`, seguido de revisar el archivo ejemplo con `cat ejemplo.txt` donde se obtuvo como salida:
```{bash}
Hola Mundo
```

Al probar `$ git status` se obtuvo nuevamente:
```{bash}
En la rama master
Tu rama está actualizada con 'origin/master'.

Cambios a ser confirmados:
  (usa "git restore --staged <archivo>..." para sacar del área de stage)
	nuevo archivo:  ejemplo.txt

Cambios no rastreados para el commit:
  (usa "git add <archivo>..." para actualizar lo que será confirmado)
  (usa "git restore <archivo>..." para descartar los cambios en el directorio de trabajo)
	modificado:     ejemplo.txt
```

Mensaje que cambio al aplicar el comando `$ git add ejemplo.txt`, seguido de `$ git status` :
```{bash}
En la rama master
Tu rama está actualizada con 'origin/master'.

Cambios a ser confirmados:
  (usa "git restore --staged <archivo>..." para sacar del área de stage)
	nuevo archivo:  ejemplo.txt
```

El comando *git diff* no genero cambios, ni arrojo ningun resultado en pantalla, probablemente debido a que el archivo "ejemplo.txt" no se encuentra unido al branch.

Ahora se probo el eliminar un elemento, para esto se genero un nuevo archivo con el nombre "ejemplo2.txt" y fue agregado con *git add*, para ser eliminado se utilizo el comando `$ git rm -f ejemplo2.txt`, debido a que el comando `$git rm ejemplo2.txt` arrojaba el siguiente error:
```{bash}
error: el siguiente archivo tiene cambios en stage en el índice:
    ejemplo2.txt
(usa --cached para conservar el archivo, o -f para forzar su eliminación)
```
Debido a que me encuentro trabajando en mi repositorio, los comandos *push* y *fetch* no se probaron. 

A continuación se configuro el git local a la cuenta Github usando los comandos `$ git config --global user.email soniavidal@uchile.cl` y `$ git config user.name SonissimaV`, el correcto ingreso se verifico con el comando `$ git config user.email` el cual dio como resultado:
```{bash}
soniavidal@uchile.cl
```

Siguiendo con los ejercicios del workshop, se generan los archivos `ejemplo_final.bed` y `ejemplo_final.fam` usando el comando 
```{bash}
$ touch ejemplo_final.bed
$ touch ejemplo_final.fam
```

Para saber cuantos archivos hay con la misma terminación, ejemplo *.bed*; se utiliza el comodín `*` tambien llamado wildcard, el cual reemplaza a los caracteres (cualquier caracter y cualquier cantidad de caracteres). Un ejemplo de su uso es `$ ls *final*` donde el comodin abarca todos los caracteres anteriores y posteriores a la palabra *final*, la salida fue:
```{bash}
ejemplo_final.bed  nuevos_final.bed  nuevos_final.fam
ejemplo_final.fam  nuevos_final.bim  nuevos_final.log
```
Otros comodines, pero mas limitados son *?* el cual solo es capaz de reemplazar un caracter y *[]* el cual permite agrupar los caracteres a reemplazar; ejemplos de usos de estos comodines son:
```{bash}
$ ls nuevos_final.???
nuevos_final.bed  nuevos_final.bim  nuevos_final.fam  nuevos_final.log
$ ls [a-z]*.bim
nuevos_final.bim
```

La busqueda de patrones es algo muy utilizado en genética, ya que permite encontrar de manera rápida patrones determinados, cuantificarlos e incluso reemplazarlos. En el ejemplo del workshop se busco y reemplazo el nombre cientifico de una especie de tomates por la palabra *jitomate* en el archivo *jitomate.fasta* usando el comando `sed 's/Solanum lycopersicum/jitomate/' jitomate.fasta` el resultado de este comando fue el reemplazo de una parte del encabezado de 3 secuencias.
El comando *awk* tiene variadas funciones, por ejemplo, puede contar la cantidad de lineas de un fichero (jitomate.fasta) escribiendo `$ awk 'END {print NR}' jitomate.fasta` que nos arroja un numero entero de 42.
Se prueba el comando *grep* usando `grep lycopersicum jitomate.fasta`, obteniendo:
```{bash}
>gi|315140847|gb|HQ593449.1| Solanum lycopersicum voucher AP471 maturase K (matK) gene, partial cds; chloroplast
>gi|385137316|gb|JQ412261.1| Solanum lycopersicum voucher BS0156 maturase K (matK) gene, partial cds; chloroplast
>gi|315259972|gb|HQ619840.1| Solanum lycopersicum isolate LegMedMO_116 maturase K (matK) gene, partial cds; chloroplast
```
Ademas de esto tiene muchas más opciones, por ejemplo usando *-c* permite contar las lineas donde aparecen un caracter de interes; *-l* entrega todos los nombres de archivos en los cuales se encuentra la expresion de interes, al agregar *-i* se hace insensible la busqueda a mayusculas o minusculas; *-w* termine buscar palabras enteras con lo que busco y no partes de palabras.

Se realizaron los ejercicios 1 y 2:
*ejercicio 1*
```{bash}
$ grep -oE "\Physalis philadelphica" tomatesverdes.fasta 
Physalis philadelphica
Physalis philadelphica
Physalis philadelphica
Physalis philadelphica
Physalis philadelphica
```

*ejercicio 2*
Pendiente!


### Loops
Los loops son funciones que se repiten una serie de comandos cuando se cumplan las condiciones, en el caso de bash tienen una estructura basica de:
*for* i *in* lista de palabras, caracteres no separados por comas *; do*
*comando* (ejemplo echo) *;done*

Un ejemplo:
```{bash}
$ for unidades in "Unidad 1" "Unidad 2" "Unidad 3"; do
> echo la $unidades es la más entrenida de todas; done
la Unidad 1 es la más entrenida de todas
la Unidad 2 es la más entrenida de todas
la Unidad 3 es la más entrenida de todas
```
Preguntas:
¿Cuándo debo usar comillas en la lista de elementos?
R: Se usan comillas cuando el elemento de la lista tiene espacios entremedio
¿Qué hace ;?
R: El punto y coma ; señaliza el termino de la condición.
Pregunta ¿De qué manera sencilla borrarías muchos directorios a la vez?
R: `rm -r dire*`

Para crear una variable que quiera ser introducida en un loop del tipo *for*, es importante que entre el nombre de la variable y la variable vaya el signo "=" sin empacios; ejemplo: `curso=Tecnicas`








```{bash}
```
```{bash}
```
```{bash}
```
```{bash}
```
```{bash}
```
```{bash}
```
















