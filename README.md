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





### Unidad 2, Markdown

El principal problema que se tiene hoy en día en la ciencia en general es la reproducibilidad de los resultados y la bioinformatica no se salva de este conflicto. Por este motivo nacen los repositorios, para poder contener gran cantidad de datos generados, pero solo tener los datos no es suficiente para lograr la tan anhelada reproducibilidad de los resultados. Se hace indispensable el poder seguir los mismos pasos, la misma depuracion de datos brutos, los mismos parametros de analisis, etc. Todo esto debe estar especificado en un script lo más claro posible y seguir el mismo orden en que fue realizado la primera vez para reproducirlo e incluso mejorarlo.

Una manera de escribir estos script es en *Markdown*, el cual es un formato ampliamente utilizado en Github, Stackoverflow y otras plataformas gracias a su sencillez al tratarse de un archivo de texto plano pero con caracteristicas que permiten ser empleado, por ejemplo, para ser transformado rapidamente a HTML. Dentro de las ventajas la utilizacion de Markdown esta la aplicación universal, ya que la sintaxis es reconocida en todos los sistemas operativos, repositorios y reconocida rapidamente; ademas, las herramientas basadas en Markdown son gratis.

La sintaxis basica de Markdown es:

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
     * Estas dos maneras se pueden mezclar usando una combinacion entre simples y dobles `**dobles y _simples_**` **negritas y _cursivas_**.
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

    * Usando espacios o puntos se puede hacer sub-indices:
```{bash}
+ Primero (sin tab)
  + Segundo (1 tab)
    + Tercero (2 tab)
      + Cuarto (3 tab)
        + Quinto (4 tab)
          + Sexto (5 tab)
            + Septimo (6 tab)
```
+ Primero
  + Segundo
    + Tercero
      + Cuarto
        + Quinto (4 tab)
          + Sexto (5 tab)
            + Septimo (6 tab)




















```{bash}
```
















cd Escritorio/SONIA/estadia2/wksp2019/Unidad1/Bash_git/Prac_bash
