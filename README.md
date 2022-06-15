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
1. Hacer ingreso al servidor del proyecto genoma atraves del comando `shh`
2. Generar variables transitorias o de ambiente que permitiran de manera más fácil hacer alusion a una información. En este caso serían variables que representan rutas.
3. Analizar la calidad de los datos, para esto usa comandos de plink como `missing` el cual entrega un reporte de datos perdidos ya sea de muestras o de variantes. Con estos resultados de datos perdidos se puede analizar si una muestra tiene un porcentaje muy alto de datos perdidos y quizas sería mejor no considerarla o si un SNP en particular no es correctamente leido en todas las muestras y es mejor descartarlo para el analisis.















```{bash}
```
















cd Escritorio/SONIA/estadia2/wksp2019/Unidad1/Bash_git/Prac_bash
