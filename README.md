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








```{bash}
```

















