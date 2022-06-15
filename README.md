## Semana 3

### Repositorio de imagenes

Debido al gran interes por mantener imagenes de alta calidad, ya sea para compartir con familiares, amigos o para empresas, es que han surgido los alojamientos de imagenes en linea. En estos una persona sube una imagen la cual queda "alojada" y se le asigna un link de acceso que puede ser compartido con otra(s) persona(s). Se diferencia de los sitios web para compartir fotos como Instagram, Facebook, Flick, entre otros; en que los alojamientos de imagenes te permite compartir una imagen e incluirla directamente en otras plataformas e incluso todo tipo de imagenes como fotografias, ilustraciones, avatares sin perder la calidad original.

En el servicio de alojamiento de imagenes, las imagenes se alojan en una nube y no en un servidor lo cual le otorga mayor escalabilidad, confiabilidad y flexibilidad para alojar cada vez más imagenes. Además de presentar otros beneficios como ahorrar espacio de almacenamiento en su propio dispositivo, velocidad de carga constante, funciones para compartir facilmente cada imagen, funciones de colaboración, incluso algunos alojamientos ofrecen analisis estadisticos sobre fallidos de carga, visualizaciones, etc.

Para generar este github elegi el sistema de alojamiento *PostImage* creado en 2004, principalemente porque es muy sensillo de usar, es gratis, aguanta imagenes de hasta 8MB y no es requisito generar una cuenta para poder subir las imagenes, tiene la capacidad de crear una galeria con las imagenes favoritas y es famoso por permitir modificar las fotos para compartirlas.

La pagina web principal es https://postimages.org/ y en ella simplemente se carga la imagen y se obtiene de retorno distintos link según la plataforma donde se quisiera compartir la imagen, tales como:
* Link
* Direct link
* Markdown
* Markdown para github
* Thumbnail for forums
* Miniatura para webs
* Hotlink for forums
* Enlace directo para webs





### Unidad 3 Genomica de poblaciones

Para la comprension de esta unidad se recurrieron a las clases de [Bioinf CL-MX 2020](https://www.youtube.com/watch?v=Gdxwh2oSkOY&ab_channel=Bioinform%C3%A1ticaCL-MX)

La genetica de poblaciones busca describir la variacion y distribucion alelica de una población en particular, dada por individuos de una misma especie que comparten tiempo y lugar. En este practico se busca analizar los genomas obtenidos de ChileGenomico y HapMap.

Para realizar esto se usaran programas como:

**PLINK**, el cual es un programa que trabaja con conjuntos de datos que comprenden cientos de miles de marcadores para muchos individuos a la vez de modo que pueden manipularse y analizarse rapidamente con unos pocos comandos. 
Este programa genera un archivos que pueden estar en formato normal: en los cuales encontramos archivos .ped que contiene los SNPs y otro .map que contiene la posiciòn. Tambien puede generar archivos en formato binario en los cuales encontramos archivos .bed que contiene toda la informacion anterior, genera tambien archicos .bim que contiene las bases originales y .fam contiene los datos de las muestras (nombre de las muestras y pedigree).
El archivo .raw es donde Plink exporta los resultados para que sean leibles por otros programas.
Para utilizar Plink basta con tener instalado Plink, los archivos geneticos y los comandos necesarios para generar los archivos de salida .bed, .bim y .fam.
plink tiene una amplia variedad de opciones para poder filtrar los datos por ejemplo: segun posicion cromosomal, por muestra, segun el MAF, segun el equiliquio de Hardy-Weinberg, segun datos faltantes, etc. Se pueden revisar mas filtros en la pagina web [Filtros plink](https://www.cog-genomics.org/plink/1.9/filter)
Ademas de entregar varios tipos de reportes tales como: archivos .ped que contienen los resumenes de los filtros realizados, .frq que contiene todas las frecuencias alelicas, .hwe que contiene los calculos de Hardy-Weinberg para cada locus. Se pueden revisar mas formatos y analisis en [Estadistica Básica plink](https://www.cog-genomics.org/plink/1.9/basic_stats).
Otro fuerte motivo para usar plink en nuestros analisis es que el output entregado esta en un formato que puede ser reconocido como input para otro programa.


**R** es uno de los programas que acepta como entradas algunas de las salidad de plink. Gracias a que posee distintos paquetes dedicados a genetica es que R ha ganado gran versatilidad en el analisis y visualización de datos genomicos. Entre estos paquetes encontramos *adegenet*, *ape* y una amplia variedad más, que puede ser revisado con detención en la pagina de CRAN para [Statistical Genetics](https://cran.microsoft.com/snapshot/2017-08-01/web/views/Genetics.html) o en Bioconductor [Bioconductor Software Packages](https://bioconductor.org/packages/release/bioc/). 
Siempre debe considerarse que no todos los paquetes funcionan para todos los tipos de datos, por ejemplo *dartr* que esta especializado en el analisis de SNP [dartr](https://pubmed.ncbi.nlm.nih.gov/29266847/) o *rrBLUP* para analisis de GWAS [rrBLUP](https://cran.r-project.org/web/packages/rrBLUP/rrBLUP.pdf).


**Admixture** es un programa que recibe archivos obtenidos desde plink, en especifico archivos .ped. Este programa se utilizar para inferir ancestría mediante los datos de pedigree que se tienen de las muestras de SNP. El calculo de ancestría, es decir, que porcentaje del genoma corresponde a cada población genética a evaluar, puede ser realizado para distintas cantidades de poblaciones o K. El programa permite realizar el calculo para cada K que se desee evaluar y ademas hace un calculo de cross validation (cv) que nos permite elegir el mejor numero de K (menor valor de cv) osea con el menor error. 


El tutorial propiamente tal consiste en:

1. Hacer ingreso al servidor del proyecto genoma atraves del comando `$ ssh bioinfo1@genoma.med.uchile.cl` y una contraseña dispuesta para el.

2. Generar variables transitorias o de ambiente que permitiran de manera más fácil hacer alusion a una información. En este caso serían variables que representan rutas y se tratan de los comandos:
`export T=/shared/bioinfo1/GWA_tutorial/1_QC_GWAS` ,  `export P=/shared/bioinfo1/GWA_tutorial/2_Population_stratification/` , `export C=/shared/bioinfo1/ChileGenomico` y `export G=~/1000G` .

3. Analizar la calidad de los datos, para esto usa comandos de plink como `missing` el cual entrega un reporte de datos perdidos ya sea de muestras o de variantes. Con estos resultados de datos perdidos se puede analizar si una muestra tiene un porcentaje muy alto de datos perdidos y quizas sería mejor no considerarla o si un SNP en particular no es correctamente leido en todas las muestras y es mejor descartarlo para el analisis. Para esto se utiliza el comando `plink --bfile $C/chilean_all48_hg19 --missing`

4. Con el fin de poder visualizar de manera más rapida y sencilla estos datos perdidos es que se utiliza R, en particular se realiza un histograma con los datos obtenidos del comando anterior. El comando para la grafica es `Rscript --no-save $T/hist_miss.R` donde hist_miss es un script previamente formulado en formato R. Como resultado de este script se obtienen 2 graficos:
[![histimiss.png](https://i.postimg.cc/R0n5qdB7/histimiss.png)](https://postimg.cc/4KZFSzny)
En este grafico observamos que la mayoria de las muestras tiene valores muy bajos de datos perdidos, mientras que en el siguiente grafico podemos ver que algunos SNPs en particular no se encuentran en todas las muestras.
[![histlmiss.png](https://i.postimg.cc/hvmfrTTT/histlmiss.png)](https://postimg.cc/9wWmX4xQ)

5. Al visualizar estos graficos podemos determinar un rango de corte para descargar muestras o SNP sin perder un gran numero. Para la eliminación de estos se utilizan los siguientes comandos:
` plink --bfile $C/chilean_all48_hg19 --geno 0.2 --make-bed --out chilean_all48_hg19_2` para eliminar las variantes del archivo *chilean_all48_hg19* que tengan una perdida mayor al 20% y haga un nuevo archivo depurado con nombre *chilean_all48_hg19_2*.
`plink --bfile chilean_all48_hg19_2 --mind 0.2 --make-bed --out chilean_all48_hg19_3` para eliminar en el archivo generado con el comando anteior las muestras que tengan una perdidad mayor al 20% y las guarde en un archivo llamado *chilean_all48_hg19_3*.

6. 











```{bash}
```
















cd Escritorio/SONIA/estadia2/wksp2019/Unidad1/Bash_git/Prac_bash
