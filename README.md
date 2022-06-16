# Estadia2
CURSO TÉCNICAS  Y METODOLOGIAS EN GENÉTICA


## Semana 1, comando basicos y como hacer un repositorio
Esta semana fue realizada guiandome con el tutorial https://docs.github.com/es/get-started/quickstart/hello-world y siguiendo las unidades desde https://github.com/u-genoma/wksp2019.


### Unidad 1, Línea de comando
Mediante la utilización de Ubuntu se probaron comandos descritos en la "Unidad 1" del repositorio BioinfinvRepro año 2018. Comandos tales como:
- `pwd`   para poder conocer la ruta del directorio en el que actualmente estamos
- `ls`    para poder conocer los archivos y carpetas que estan dentro de un directorio
- `mkdir` para crear una carpeta
- `mv RUTA/NOMBRE_ARCHIVO RUTA_DESTINO` para mover un archivo desde una ruta a otra destino
- `cd`    para poder entrar a una carpeta
- `cd ..` para poder volver a la carpeta anterior
- `echo`  para podes imprimir en pantalla un mensaje
- `cp`    para copiar archivos
- `less`  para ver archivos de manera compaginada
- `more`  para mostrar una parte de los archivos
- `cat` para ver el archivo completo sin compaginar o concatenar 2 archivos distintos en un tercero
- `wget PAGINA_WEB` para descargar algun archivo desde un link de descarga
- `unzip NOMBRE_ARCHIVO` para descomprimir un archivo
- `tar -xvf NOMBRE_ARCHIVO` para descomprimir archivos .tar (-x), que nos muestre que hace (v) y reciba un archivo de entrada (f)
- `scp SERVIDOR:/RUTA_ABSOLUTA/ARCHIVO_DESCARGAR ./` para descargar un archivo desde un servidor a nuestra carpeta actual

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

*ejercicio 1*
```{bash}
$ grep -oE "\Physalis philadelphica" tomatesverdes.fasta 
Physalis philadelphica
Physalis philadelphica
Physalis philadelphica
Physalis philadelphica
Physalis philadelphica
```


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

En los loop *for* tambien se pueden utilizar archivos, como por ejemplo *.fasta*:
`for i in *.fasta; do
echo debemos buscar una secuencia en el archivo $i;done`
```{bash}
$ for i in *.fasta;do echo "Ejemplo de archivo fasta es $i";done
Ejemplo de archivo fasta es jitomate.fasta
Ejemplo de archivo fasta es tomatesverdes.fasta
```
Tambien se pueden utilizar listas asociadas previamente a una variable con la salvedad que debe hacerse alucion a esta anotando `${lista[@]}`, por ejemplo:
```{bash}
$ lista=(Unidad1 "Unidad2" Unid3)
$ for i in ${lista[@]}; do
> echo La mejor manera de escribir la unidad es $i; done
La mejor manera de escribir la unidad es Unidad1
La mejor manera de escribir la unidad es Unidad2
La mejor manera de escribir la unidad es Unid3
```
Las listas puede ser resultado de un comando como `grep` u otro similar. Aunque es bueno que la salidad de este comando sea guardado como un nuevo archivo, por ejemplo: `$ grep -oE "\w+_[0-9]*" nuevos_final.fam > muestras.txt` para luego realizar el loop con este archivo: `$ for i in $(cat muestras.txt); do echo Hacer algo con la muestra $i; done`.


### Scrips
Es un texto plano en el cual esta ordenado de manera secuencial y clara las instrucciones necesarias para llevar a cabo un analisis más complejo. Es útil para poder recordar que función cumple cada linea del codigo, es facil de compartir y utilizar posteriormente para repetir el analisis o variar algunos elementos.
Un buen script posee los codigos o instrucciones para la computadora debe ejecutar en el orden en que deben ser ejecutados y a la vez, comentarios (que comienzan por el simbolo *#*) para que las personas pueden entender de manera rapida y sencilla la funcion del script completo o de alguna linea en particular.

Para iniciar un scrip se hace con un edito de texto, se eligio *nano*, `nano script_prueba.sh`. Una vez abierto el script se escriben las instrucciones, en este caso las mismas entregadas por el workshop:
```{bash}
#!/bin/bash
# -*- ENCODING: UTF-8 -*-

## Este script baja 3 secuencias de Chiropterotriton de NCBI
# Crear directorio para guardar datos
mkdir Chiropt

# Bajar datos de NCBI
curl -s "https://eutils.ncbi.nlm.nih.gov/entrez/eutils/efetch.fcgi?db=nucleotide&rettype=fasta&id=937202862,937202860,937202858" > Chiropt/ranas.fasta

# Revisar qué secuencias se bajaron
grep ">" Chiropt/ranas.fasta

echo "listo" 
```

Una vez listo el script se debe correr, para esto debemos estar en la carpeta donde esta el script y correr el comando `bash`
```{bash}
$ bash script_prueba.sh 
>KT820711.1 Chiropterotriton sp. SMR-2015b voucher MVZ:Herp:269665 cytochrome b (cytb) gene, partial cds; mitochondrial
>KT820710.1 Chiropterotriton sp. SMR-2015a voucher IBH:28182 cytochrome b (cytb) gene, partial cds; mitochondrial
>KT820709.1 Chiropterotriton sp. SMR-2015a voucher IBH:28178 cytochrome b (cytb) gene, partial cds; mitochondrial
Listo
```


## R

Los script de R pueden correrse sin necesidad de abrir R propiamente tal, usando el comando `Rscript` seguido del archivo .R, el resultado de este script aparecerá en pantalla.
Si uso el comando `R CMD BATCH` tambien corro el archivo .R, pero ahora el resultado del script se guarda en un archivo .Rout el cual contiene la informacion basica de R, el contenido del script y el resultado, continuado de datos del procesamiento del script como el tiempo. Ejemplo:
```{bash}
$ R CMD BATCH holascript.R
$ cat holascript.Rout 

R version 4.1.2 (2021-11-01) -- "Bird Hippie"
Copyright (C) 2021 The R Foundation for Statistical Computing
Platform: x86_64-pc-linux-gnu (64-bit)

R es un software libre y viene sin GARANTIA ALGUNA.
Usted puede redistribuirlo bajo ciertas circunstancias.
Escriba 'license()' o 'licence()' para detalles de distribucion.

R es un proyecto colaborativo con muchos contribuyentes.
Escriba 'contributors()' para obtener más información y
'citation()' para saber cómo citar R o paquetes de R en publicaciones.

Escriba 'demo()' para demostraciones, 'help()' para el sistema on-line de ayuda,
o 'help.start()' para abrir el sistema de ayuda HTML con su navegador.
Escriba 'q()' para salir de R.

> x<-10
> y<-6
> cat("¡Hola mundo!", x, "+", y, "es igual a", x+y)
¡Hola mundo! 10 + 6 es igual a 16> write(x, file="aquiestax.txt")
> 
> proc.time()
   user  system elapsed 
  0.092   0.009   0.082 
```

Otra manera de poder utilizar R y que es más amigable con el usuario es atraves de RStudio.

Una de las razones que hace a R una herramienta tan poderosa es que al ser de codigo abierto esta constantemente agregando nuevos paquetes con funciones nuevas y depuradas que son agregadas por todo tipo de profesionales. El principal repositorio para estos paquetes es *CRAN*, pero a nivel de analisis genomico el mas potente es *Bioconductor*. 
Para el uso de paquetes lo primero que debe hacerse es la instalacion mediante el comando `install.packages("nombre del paquete")` y para activarlo simplemente el comando `library("nombre del paquete")`.



```{bash}
```
















cd Escritorio/SONIA/estadia2/wksp2019/Unidad1/Bash_git/Prac_bash
