## Semana 2, R

Siguiendo con la leccion de R/RStudio.

Para poder cargar archivos existen varias maneras, por ejemplo *read.delim* permite archivos de filas y columnas. Esto incluye datos geneticos que una vez abiertos pueden ser utilizados para graficar y analizarlo.

Existen varios paquetes con funciones especializadas para graficar datos geneticos, paquetes tales como *ggplot2*, *ggbio*, *ape*, entre otras. En este caso se utilizó una funcion que viene en el paquete base para las más simples y luego algunos paquetes para graficos mas complejos.

En primer lugar dentro de esta funcion *Graphics* se vio graficos clasicos como graficos de puntos o `plot`, de barras o `barplot`, de caja y bigotes o `boxplot`, histogramas o `hist`, de torta o `pie`, entre otros.

#### Gráfico de puntos:

```{r}
plot(x=cars$speed, y=cars$dist, xlab="Velocidad", ylab="Distancia", cex=0.5, pch=19, main = "Ejemplo gráfico PLOT")
```
Donde *cars* corresponde a una base de datos que viene con R, *xlab* e *ylab* son comandos para colocarles titulos a los ejes x e y, respectivamente. El comando *cex* se utiliza para determinar el tamaño del icono que marca los datos donde 1 es el tamaño estandar, *pch* es un comando para elegir el tipo de icono que marca los datos (en este caso circulos macizos) y *main* para colocar un titulo al grafico.

[![Rplot.jpg](https://i.postimg.cc/CMZ3ZWHk/Rplot.jpg)](https://postimg.cc/SjhT31Px)

#### Gráfico de barra:
```{r}
barplot(reads$nreads, col=rainbow(6), xlab="Sample", ylab="Reads", main = "Ejemplo barplot")
```
[![barplot.jpg](https://i.postimg.cc/sXg8XYcQ/barplot.jpg)](https://postimg.cc/HJF3v7Fd)



Un paquete mas especializado para los gráficos es *ggplot2* el cual se caracteriza por ir agregando linea a linea caracteristicas adicionales al gráfico.

#### Por ejemplo en el siguiente codigo para un grafico de puntos:
```{r}
ggplot(data=iris, aes(x=Sepal.Length, y= Sepal.Width)) + 
  ggtitle("Ejemplo ggplot2") +
  xlab("Largo sepalo") + ylab("Ancho sepalo") + 
  theme(plot.title = element_text(color="red", size=14, face="bold.italic")) +
  geom_point(aes(colour = Species,size = Petal.Width, shape= Species)) +
  scale_size_area('Ancho petalo', max_size = 4)
```
Donde:

+ ggplot es el comando basico el cual usa como base de datos *iris* 
+ Como eje X se ocupa la columna *Sepal.length* y como eje Y la columna *Sepal.Width"
+ El simbolo *+* se utiliza para ir agregando más caracteristicas al gráfico
+ con el comando *ggtitle* podemos agregar un titulo al gráfico y con *theme(plot.title...* cambiarle caracteristicas como el color, tamaño, tipo de letra, etc
+ De manera similar *xlab* e *ylab* son para agregarle titulos a los ejes
+ Con el comando *geom_point* se determina que sea un grafico de puntos donde el color de los grupos esta dado por *colour* y el tipo de marcador por *shape* y en este caso ambos son atraves de la columna *Species*, ademas de que el tamaño de los puntos esta determinado por el ancho de los petalos en el comando *size*
+ Para poder cambiar el titulo y los tamaños de los puntos de la leyenda es que se usa *scale_size_area*

[![Ejemplo-ggplot2.jpg](https://i.postimg.cc/G2sF0scD/Ejemplo-ggplot2.jpg)](https://postimg.cc/1nsnwXVR)

Tambien se pueden separar las especies una en un grafico separado cada uno, usando el codigo:
```{r}
ggplot(data=iris, aes(x=Sepal.Length, y= Sepal.Width)) + 
  ggtitle("Ejemplo ggplot2 separados") +
  xlab("Largo sepalo") + ylab("Ancho sepalo") + 
  theme(plot.title = element_text(color="red", size=14, face="bold.italic")) +
  geom_point(aes(colour = Species,size = Petal.Width, shape= Species)) +
  scale_size_area('Ancho petalo', max_size = 4)+
  facet_grid(Species ~ .)
```

Donde al agregar el comando *facet_grid* estoy seleccionando en base a que parametro separadar las grillas, en este caso según las especies.

[![Ejemplo-ggplot2-separado.jpg](https://i.postimg.cc/kG654xVJ/Ejemplo-ggplot2-separado.jpg)](https://postimg.cc/D4hhp4dH)

Tambien se pueden agregar modelos matematicos, como una linea de tendencia para cada especie de la siguiente manera:
```{r}
ggplot(data=iris, aes(x=Sepal.Length, y= Sepal.Width)) + 
  ggtitle("Ejemplo ggplot2 separados") +
  xlab("Largo sepalo") + ylab("Ancho sepalo") + 
  theme(plot.title = element_text(color="red", size=14, face="bold.italic")) +
  geom_point(aes(colour = Species,size = Petal.Width, shape= Species)) +
  scale_size_area('Ancho petalo', max_size = 4)+
  facet_grid(Species ~ .)+
  geom_smooth(method="lm")
```
Donde el comando *geom_smooth* en el metodo "lm" corresponde a un modelo lineal.

[![Ejemplo-ggplot2-separados-con-modelo-lineal.jpg](https://i.postimg.cc/N0sm0zQQ/Ejemplo-ggplot2-separados-con-modelo-lineal.jpg)](https://postimg.cc/jD1LgvW1)


#### Ahora el mismo paquete pero para graficos de barra:
```{r}
# Cambiar orden de levels segun la columna sample"
reads$sample<-factor(reads$sample, levels = reads$sample[order(1:length(reads$sample))])
p <- ggplot(data=reads, aes(x=sample, y=nreads, fill=Library)) + 
  geom_bar(stat="identity") +  
  theme(axis.text.x = element_text(angle = 45, hjust = 1, size=6))+
  ggtitle("Ejemplo barplot ggplot2") +
  xlab("Muestras") + ylab("Número lecturas") + 
  theme(plot.title = element_text(color="red", size=14, face="bold.italic")) 
p
```
Donde se grafican los datos *reads*, pero en primer lugar lo que se hace es ordenar el orden de las barras segun la columna de muestras en el orden en que se presentan en la columna, ya que por defecto las grafica por orden alfabetico. Para esto se utiliza la linea `reads$sample<-factor(reads$sample, levels = reads$sample[order(1:length(reads$sample))])`. El comando para que el tipo de grafico sea de barra es `geom_bar(stat="identity")`, el resto de los comandos son los mismos utilizados para el grafico de puntos antes mencionados. El gráfico resultante es:

[![ejemplo-barplot-ggplot2.jpg](https://i.postimg.cc/ZRqvfwxK/ejemplo-barplot-ggplot2.jpg)](https://postimg.cc/wtSBMcrS)

#### *ggplot2* tambien tiene una version para graficos de bigotes y caja:

```{r}
p <- ggplot(data=reads, aes(x=Library, y=nreads, fill=Library)) + 
  geom_boxplot()+  
  ggtitle("Ejemplo boxplot ggplot2") +
  xlab("Libreria") + ylab("Número lecturas") + 
  theme(plot.title = element_text(color="red", size=14, face="bold.italic")) 
p
```
Donde el comando `geom_boxplot` es quien determina que se trate de un grafico de cajas, el resto de los comandos son los mismos usados para barplot y ggplot.

[![ejemplo-boxplot-ggplot2.jpg](https://i.postimg.cc/fRh01G4B/ejemplo-boxplot-ggplot2.jpg)](https://postimg.cc/ykvdZr8Z)

Un punto importante en cualquier tipo de grafico que utiliza colores es que sean colores que puedan ser diferenciados por todos los usuarios, es decir que sean amigable con las personas que presentan distinto tipo de daltonismo. En la pagina web https://venngage.com/blog/color-blind-friendly-palette/ se puede encontrar informacion interesante de los distintos tipos de daltonismo y que paleta de colores son adecuadas para cada uno.

Para cambiar los colores en ggplot2 se utiliza el comando `scale_fill_manual(values=XXXXXXX)` donde en XXXXXXX se ingresan los colores manualmente (uno a uno) o el nombre de una paleta de colores definida.
```{r}
p <- ggplot(data=reads, aes(x=Library, y=nreads, fill=Library)) + 
  geom_boxplot()+  
  ggtitle("Ejemplo boxplot ggplot2 color-blind-friendly") +
  xlab("Libreria") + ylab("Número lecturas") + 
  theme(plot.title = element_text(color="red", size=14, face="bold.italic")) 
p + scale_fill_manual(values=cbPalette)
# p + scale_fill_manual(values=c("red", "blue", "green")) #ejemplo de ingreso manual, color a color
```

[![Ejemplo-boxplot-ggplot2-color-blind-friendly.jpg](https://i.postimg.cc/QxWT4ptg/Ejemplo-boxplot-ggplot2-color-blind-friendly.jpg)](https://postimg.cc/SJkRjYcj)

Hasta el momento solo se ha visto un grafico a la vez, pero tambien se pueden hacer imagenes con varios graficos a la vez. Para esto se utilizó el paquere *Rmisc*, en el cual se puede determinar la cantidad de graficos y columnas de como ordenarlos.

```{r}
s1 <- ggplot(data=reads, aes(x=sample, y=nreads, fill=Library)) + 
  ggtitle("Ejemplo ggplot2") +
  xlab("Muestra") + ylab("Número lecturas") + 
  theme(plot.title = element_text(color="red", size=14, face="bold.italic")) +
  geom_point(aes(colour = Library)) +
  theme(axis.text.x = element_text(angle = 45, hjust = 1, size=6))
  

s2 <- ggplot(data=reads, aes(x=sample, y=nreads, fill=Library)) + 
  geom_bar(stat="identity") +  
  theme(axis.text.x = element_text(angle = 45, hjust = 1, size=6))+
  ggtitle("Ejemplo barplot ggplot2") +
  xlab("Muestras") + ylab("Número lecturas") + 
  theme(plot.title = element_text(color="red", size=14, face="bold.italic"))

s3 <- ggplot(data=reads, aes(x=Library, y=nreads, fill=Library)) + 
  geom_boxplot()+  
  ggtitle("Ejemplo boxplot ggplot2") +
  xlab("Libreria") + ylab("Número lecturas") + 
  theme(plot.title = element_text(color="red", size=14, face="bold.italic")) 

s4 <- ggplot(data=reads, aes(x=Library, y=nreads, fill=Library)) + geom_boxplot()+  
  ggtitle("Ejemplo color-blind-friendly") +
  xlab("Libreria") + ylab("Número lecturas") + 
  theme(plot.title = element_text(color="red", size=14, face="bold.italic")) + 
  scale_fill_manual(values=cbPalette)

multiplot(s1, s2, s3, s4, cols=2)
```

[![ejemplo-multiplot.jpg](https://i.postimg.cc/pXWq7W4X/ejemplo-multiplot.jpg)](https://postimg.cc/BtzTP0Jd)


#### Grafico Arboles filogeneticos
Para realizar arboles filogeneticos se utiliza el paquete *ape* y el paquete *phytools*. Para este ejemplo se utilizo el paquere *rotl* el cual permite descargar la secuencia y generar un arbol con el genoma completo de un organismo. 
```{r}
library("rotl")
taxa <- tnrs_match_names(names = c("Felis silvestris", "Felis chaus", "Felis margarita", 
                                   "Felis nigripes", "Otocolobus manul", "Lynx canadensis", "Lynx lynx",
                                   "Lynx pardinus", "Lynx rufus", "Caracal caracal", "Caracal aurata", 
                                   "Leptailurus serval", "Pardofelis marmorata", "Pardofelis badia", 
                                   "Pardofelis temminckii", "Prionailurus bengalensis", "Prionailurus rubiginosa", 
                                   "Prionailurus viverrinus", "Leopardus colocolo", 
                                   "Leopardus pardalis", "Leopardus wiedii", "Leopardus tigrinus", 
                                   "Leopardus geoffroyi", "Leopardus guigna", "Leopardus jacobita", 
                                   "Puma yagouaroundi", "Puma concolor", "Panthera uncial", 
                                   "Panthera tigris", "Panthera pardus", "Panthera onca", "Panthera leo", 
                                   "Acinonyx jubatus"))

tree <- tol_induced_subtree(ott_ids = taxa[["ott_id"]])
plot(tree, cex=0.8)
title("Familia felidae (paquete rotl)")
```

[![arbol-filogenetico-rotl.jpg](https://i.postimg.cc/g0tCcMXQ/arbol-filogenetico-rotl.jpg)](https://postimg.cc/wtJf0QkQ)





## Unidad 2 

### Markdown

El principal problema que se tiene hoy en día en la ciencia en general es la reproducibilidad de los resultados y la bioinformatica no se salva de este conflicto. Por este motivo nacen los repositorios, para poder contener gran cantidad de datos generados, pero solo tener los datos no es suficiente para lograr la tan anhelada reproducibilidad de los resultados. Se hace indispensable el poder seguir los mismos pasos, la misma depuracion de datos brutos, los mismos parametros de analisis, etc. Todo esto debe estar especificado en un script lo más claro posible y seguir el mismo orden en que fue realizado la primera vez para reproducirlo e incluso mejorarlo.

Una manera de escribir estos script es en *Markdown*, el cual es un formato ampliamente utilizado en Github, Stackoverflow y otras plataformas gracias a su sencillez al tratarse de un archivo de texto plano pero con caracteristicas que permiten ser empleado, por ejemplo, para ser transformado rapidamente a HTML. Dentro de las ventajas la utilizacion de Markdown esta la aplicación universal, ya que la sintaxis es reconocida en todos los sistemas operativos, repositorios y reconocida rapidamente; ademas, las herramientas basadas en Markdown son gratis.

##### La sintaxis basica de Markdown es:

- Encabezados: los titulos se anotan con *#* donde la cantidad de # va a determinar el tamaño.
# H1 Un solo gato
## H2 Dos gatos
### H3 Tres gatos
#### H4 Cuatro gatos
##### H5 Cinco gatos
###### H6 Seis gatos



- Enfasis: para destacar palabras por sobre otras.
    * Para colocar palabras en cursiva se puede usar asteriscos o guion bajo `*palabras entre asteriscos*` *cursiva* o  `_palabras entre guiones bajos_` _cursiva_.
    * Para colocar palabras en negrita se usan los mismos asteriscos o guion bajo pero dobles `**palabras entre asteriscos**` **negrita** o  `__palabras entre guiones bajos__` __negrita__.
     * Estas dos maneras se pueden mezclar usando una combinacion entre simples y dobles o usando triple asterisco `**dobles y _simples_**` **negritas y _cursivas_** o `***triple asterisco***` ***negrita y cursiva***.
     * Tambien se pueden tachar palabras usando virgulas simples `~entre virgulas simples~` ~tachada~.



- Se pueden listar de distintas maneras:
    * Haciendo un listado de numeros:
```{bash}
1. Primero
2. Segundo
```
1. Primero
2. Segundo

    * Usando asteriscos:
```{bash}
* Primero
* Segundo
```
* Primero
* Segundo

    * Usando lineas:
```{bash}
- Primero
- Segundo
```
- Primero
- Segundo

    * Usando simbolo más:
```{bash}
+ Primero
+ Segundo
```
+ Primero
+ Segundo

    * Usando tabulaciones se puede hacer sub-indices:
```{bash}
+ Primero (sin tab)
  + Segundo (1 tab)
    + Tercero (2 tab)
      + Cuarto (3 tab)
```
+ Primero
  + Segundo
    + Tercero
      + Cuarto

- Se pueden insertar links: para esto simplemente se coloca la pagina web o puede colocarse un titulo y luego la pagina web.
```{bash}
Solo pagina web: https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet
[Operaciones basicas de Markdown](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet)
```
Solo pagina web: https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet

[Operaciones basicas de Markdown](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet)


- Se pueden insertar imagenes: para esto simplemente se coloca la pagina web o puede colocarse un titulo y luego la pagina web o hacer referencia a la pagina web.
```{bash}
Ginkgo biloga
![GB.png](https://i.postimg.cc/bNJnJk94/GB.png)

Ginkgo biloga
![GB.png][direccion]

[direccion]: https://i.postimg.cc/bNJnJk94/GB.png
```
Ginkgo biloga
![GB.png](https://i.postimg.cc/bNJnJk94/GB.png)

Ginkgo biloga
![GB.png][direccion]

[direccion]: https://i.postimg.cc/bNJnJk94/GB.png

#### RMarkdown

R viene su version de Marckdown llamada *R Marckdown*, esta puede ser utilizada directamente desde RStudio abriendo un archivo .Rmd el cual permite escribir toda la información necesaria (en mi caso hice una replica de esta unidad pero en RMarckdown). La estructura basica de todo Rmarkdown consta de una *cabecera* en la cual se coloca información basica como el titulo del archivo, el autor, la fecha, el idioma y el tipo de salida (que pueden ser varios formatos distintos, entre ellos pdf, Word, HTML, R Notebooks, etc.). La cabecera es continuada con el cuerpo del archivo en el cual va todo el texto plano en codigo Markdown y ademas, los codigos R de interes con sus resultados. En esta parte, del codigo R, hay varias formas de presentar los resultados:

- En primer lugar que se muestre el codigo y el resultado completo al colocar simplemente el chunks sin opciones, ejemplo:
`   ```{r}   codigo  ```   ` 
- En segundo lugar que se muestre solo el resultado y no el codigo. Esto le logra colocando
`   ```{r echo=FALSE}   codigo  ```   `
- En tercer lugar y por el contrario al anterior, si se quiere solo mostrar el codigo y no el resultado se debe colocar la opción:
`   ```{r eval=FALSE}   codigo  ```   `
- En cuarto lugar si se desera mostrar el codigo y el resultado, pero sin los "warning" que pudiese arrojar esta a opcion:
`   ```{r warning=FALSE}   codigo  ```   `

Para generar el archivo de salida o renderizar el documento se realiza desde el boton *Knit* y seleccionar la opcion de salidad como se muestra en la imagen en el circulo rojo:

[![Imagen1.png](https://i.postimg.cc/43KSSbHr/Imagen1.png)](https://postimg.cc/4KgPKc55)

#### De script a R Markdown

Se puede pasar desde un script de R a un reporte a pesar de no estar en formato markdown, esto se logra haciendo click en *Compile report* como se muestra en la siguiente imagen señalado con una flecha roja.

[![Imagen2.png](https://i.postimg.cc/fyBbrh6W/Imagen2.png)](https://postimg.cc/bSS8Z4y4)

Cabe destacar que el archivo generado consta de todos los comandos corridos y los resultados obtenidos (analisis, tablas, graficos, imagenes generadas, etc.), pero de una manera no muy amigable a una persona no familiarizada con el script original.



### Jupyter notebooks y JupyterLab

Los notebook de jupyter son como tener varias celdas para ser corridas independientemente, cada celda puede tener texto tipo Markdown, puede tener codigos de R, de Python, entre otros. La ventaja de estos notebook es principalmente que al ser celdas separadas se pueden probar partes de codigo de manera individual antes de ser corrido completamente. Un ejemplo de esto es el siguiente donde se observa la primera celda con escritura del tipo Markdown seguida de una segunda celda con codigo Python que puede ser corrida independiente de la primera celda.

[![Imagen3.png](https://i.postimg.cc/ZnkLYnxR/Imagen3.png)](https://postimg.cc/qhLKjkYV)

Estos notebook pueden ser exportados en distintos formatos y ser compartidos con colaboradores.



### Docker

Docker es una herramienta diseñada para alcanzar la reproducibilidad maxima en el analisis de datos, ya que no solo basta con especificar los codigos, el orden en que estos son realizados, tambien es de vital importancia las versiones de los software a utilizar, los parametros de programación, los datos de partida. Bueno Docker lo que hace es generar una especie de *contenedor* en el cual puede incluirse todo lo necesario para realizar un analisis.

Ademas de la clara ventaja de lograr una completa reproducibilidad, Docker permite tener distintas versiones de software en contenedores distintos, incluso versiones que podrían ser incompatibles entre ellas.

Se habla de *contenedor* a una unidad estandarizada de los componentes basicos de linux, en este contenedor se instalan *imagenes* de los software a utilizar donde incluye todo los elementos necesarios para que el software se eyecute, incluido librerias, herramientas del sistema, código fuente. Son estas imagenes las que pueden ser compartidas con otro usuario para reproducir nuestros mismos resultados. 

Docker tiene un listado de imagenes disponibles las cuales uno puede buscar directamente en la pagina https://hub.docker.com/ y descargarlas utilizando el comando `docker pull NOMBRE_IMAGEN` o simplemente desde nuestra terminal colocar `docker run NOMBRE_IMAGEN` y si no la tenemos automaticamente se descarga y luego se corre. 

Algunos comandos basicos de Docker son:

`docker pull NOMBRE_IMAGEN` es para poder descargar una imagen
`docker run NOMBRE_IMAGEN` para poder correr una imagen
`docker images` nos muestra las imagenes que se han descargado en la maquina, nos muestra el TAG (version descargada) y el ID de la imagen
`docker ps` nos muestra todas las imagenes que se encuentran corriendo
`docker ps -a` nos muestra las ultimas imagenes que se han corrido
`docker start CONTENEDOR_ID` volver a correr un contenedor que ya estaba corriendo y que por algun motivo se detuvo
`docker logs CONTENEDOR_ID` para ver las salidas del contenedor
`docker exec` ejecuta un comando en una imagen que ya esta corriendo
`docker exec -it CONTENEDOR_ID sh` vuelve el contenedor una shell donde uno puede ahora aplicar comandos unix
`docker stop CONTENEDOR_ID` para detener el contenedor 
`docker run -d NOMBRE_IMAGEN` para correr una imagen en background
`docker rm CONTENEDOR_ID` para borrar un contenedor ya corrido
`docker rm -f NOMBRE_IMAGEN` para borrar una imagen descargada

