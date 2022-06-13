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

**Plink**, el cual es un programa que trabaja con conjuntos de datos que comprenden cientos de miles de marcadores para muchos individuos a la vez de modo que pueden manipularse y analizarse rapidamente con unos pocos comandos. 
Este programa genera un archivos que pueden estar en formato normal: en los cuales encontramos archivos .ped que contiene los SNPs y otro .map que contiene la posiciòn. Tambien puede generar archivos en formato binario en los cuales encontramos archivos .bed que contiene toda la informacion anterior, genera tambien archicos .bim que contiene las bases originales y .fam contiene los datos de las muestras (nombre de las muestras y pedigree).
El archivo .raw es donde Plink exporta los resultados para que sean leibles por otros programas.
Para utilizar Plink basta con tener instalado Plink y los archivos 














```{bash}
```
















cd Escritorio/SONIA/estadia2/wksp2019/Unidad1/Bash_git/Prac_bash
