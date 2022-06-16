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
Luego se hace el mismo ejercicio, pero con un umbral de corte del 2%.

6. Posteriormente a la depuracion de datos perdidos lo que se realiza es la verificación del sexo de cada muestra. Para esto se utiliza el ultimo archivo creado y el comando `plink --bfile chilean_all48_hg19_5 --check-sex` el cual entrega como resultado  un archivo que es utilizado para graficar el resultado mediante un script de R y el comando `Rscript --no-save $T/gender_check.R`. Obteniendo los graficos:
[![Men-check.png](https://i.postimg.cc/BnLtSzqS/Men-check.png)](https://postimg.cc/3kh39n4V)
[![Women-check.png](https://i.postimg.cc/MTVqgkb4/Women-check.png)](https://postimg.cc/ZBbGyMQF)
En el cual se observa en los ejes X el parametro F, el cual hace referencia a la consaguineidad del cromosoma X. Como los hombres solo poseen un cromosoma X se espera una consanguineidad muy alta (>0.8 segun los filtros de plink) y para las mujeres al tener 2 cromosomas X se espera una consanguineidad baja (<0.2 segun los filtros de plink). Por lo tanto, se observan discrepancias en los sexos, ya que hay 1 hombre con F menor a 0.8 y 1 mujer con F>0.5. 

7. Para eliminar estos individuos con discrepancia de sexo se utilizan 2 comandos, en primer lugar el comando `grep "PROBLEM" plink.sexcheck | awk '{print$1,$2}'> sex_discrepancy.txt` el cual me extrae desde el archivo *plink.sexcheck* las lineas que presenten la palabra *PROBLEM*, de estas lineas se va a quedar con las columnas 1 y 2 y el resultado de esto lo va a guardar en un archivo de texto plano llamado *sex_discrepancy*. Posteriormente utiliza el comando `plink --bfile chilean_all48_hg19_5 --remove sex_discrepancy.txt --make-bed --out chilean_all48_hg19_6` para generar un nuevo archivo (llamado *out chilean_all48_hg19_6*) en el cual, utilizando como base el archivo depurado en el paso 5., se remuevan los individuos que poseen las discrepancias de sexo.

8. El paso siguiente es quedarse con las variantes correspondientes a los cromosomas autosomicos, es decir del 1 al 22. Para esto se usan los comandos `awk '{ if ($1 >= 1 && $1 <= 22) print $2 }' chilean_all48_hg19_6.bim > snp_1_22.txt` el cual usando como entrada el archivo *chilean_all48_hg19_6.bim* hace una lista de los SNP (columna 2 del archivo) que cumplan con la condicion de tener valores entre 1 y 22 de la columna 1, el resultado de esto lo escribe en un archivo de texto plano llamado *snp_1_22.txt*
Luego utiliza el comando `plink --bfile chilean_all48_hg19_6 --extract snp_1_22.txt --make-bed --out chilean_all48_hg19_7` que hace que usando el listado de SNPs extraiga todas esas filas desde el archivo base *chilean_all48_hg19_6* y generar un nuevo archivo llamado *chilean_all48_hg19_7*

9. Utilizando solo las variantes de los cromosomas autosomicos se calcula las frecuencias alelicas para cada SNP utilizando el comando `plink --bfile chilean_all48_hg19_7 --freq --out MAF_check` que la salida es utilizada para realizar un grafico de distribución para las frecuencias del alelo menor (MAF) mediante otro script de R con el comando `Rscript --no-save $T/MAF_check.R` 

10. Con los calculos realizados de frecuencias alelicas se puede ahora descartar las variantes que son monomorficas, ya que al no tener variabilidad tampoco nos entregan información relevante para evaluar la ansestría. Con este fin se utiliza el comando `plink --bfile chilean_all48_hg19_7 --maf 0.011 --make-bed --out chilean_all48_hg19_8` con el cual tendremos como salida el archivo *chilean_all48_hg19_8*.

11. El siguiente filtro a ocupar correponde al filtro de Equilibrio de Hardy-Weinberg (HWE), ya que las variantes que presenten una desviación muy grande de la esperada podrían ser variantes que presenten algun tipo de error. Se utiliza el comando `plink --bfile chilean_all48_hg19_8 --hardy` el cual hace un calculo del valor esperado, el valor obtenido y una pueba estadistica que nos entrega un p-value. En base a estos p-value se realiza un comando `awk '{ if ($9 <0.000001) print $0 }' plink.hwe > plinkzoomhwe.hwe` seguido por `Rscript --no-save $T/hwe.R` que nos permite visualizar en un histograma los valores del Equilibrio de Hardy-Weinberg y otro donde muestra cuantos se desvian de este. Graficos:
[![histhwe.png](https://i.postimg.cc/zX77T0RY/histhwe.png)](https://postimg.cc/nCsqJKk3)
[![histhwe-below-theshold.png](https://i.postimg.cc/htGrsT9z/histhwe-below-theshold.png)](https://postimg.cc/bsKkNGVp)
En los graficos se observa que un numero alto de variantes que presentan un p-value cercano a cero, por lo tanto se filtran las variantes que tengan un p mayor 0.000001 con el comando `plink --bfile chilean_all48_hg19_8 --hwe 1e-6 --hwe-all --make-bed --out chilean_all48_hg19_9` obteniendo un archivo *chilean_all48_hg19_9* que solo contiene las variantes con p>1E-6.

12. Los parentezcos desconocidos en el calculo de ancestría puede generar un error al sobreestimar la presencia de un cromosoma y de todos los SNP dentro de él, por lo tanto es indispensable descartar las muestras que esten altamente emparentadas con otras. 
Para hacer este filtro en primer lugar, se requiere que los SNP sean independientes y no presenten ligamiento. Entonces el primer comando en utilizar `plink --bfile chilean_all48_hg19_9 --exclude $T/inversion.txt --range --indep-pairwise 50 5 0.2 --out indepSNP` nos entrega una lista de SNP que son independientes entre sí y que tienen un r2 menor a 0.2 con respecto a los otros SNPs. 
A continuación se utiliza esta salidad en el comando `plink --bfile chilean_all48_hg19_9 --extract indepSNP.prune.in --genome --min 0.2 --out pihat_min0.2` para realizar el analisis de parentezco donde se seleccionan los pihat>=0.2, es decir, que los genomas no compartan mas del 20% de identidad entre dos muestras.
Como resultado de esto se obtiene una tabla donde se observan comparaciones de pares de individuos donde el pi_hat calculado es mayor a 0.2 y mediante la utilización de R se pueden obtener los graficos de pi_hat y más interesantemente un resumen de que muestra es la que más se repite con el comando `rel <- read.table("pihat_min0.2.genome", header=T)` obteniendo como resultado que la muestra ARI001 genera los mayores parentezcos. 
Entonces se opta por eliminar esta muestra con el comando `subset(rel, !IID1 %in% "ARI001" & !IID2 %in% "ARI001")` y se vuelve a realizar el analisis, arroyando ahora como posible muestras problema las ARI018 y ARI021. Por lo tanto, seleccionando estas 3 muestras del dataset .fam con el comando `awk '$2=="ARI001" || $2=="ARI021" || $2=="ARI018"' chilean_all48_hg19_9.fam > to_romeve_by_relatedness.txt` genero un archivo que puede ser utilizado para eliminar estas muestras desde el dataset depurado *chilean_all48_hg19_9* con el comando `plink -bfile chilean_all48_hg19_9 -remove to_romeve_by_relatedness.txt -make-bed --out chilean_all48_hg19_10`.

13. Posterior al filtrado de muestras emparentadas lo que continua es integrar nuestros datos a la base de datos de 1000 genomas, para esto en primer lugar se eliminan las variantes duplicadas en el set de datos de ChileGenomico con 1000G. Esto se logra con los comandos `plink --bfile chilean_all48_hg19_10 --list-duplicate-vars suppress-first` y `plink --bfile chilean_all48_hg19_10 --exclude plink.dupvar --make-bed --out chilean_all48_hg19_11`.
Luego se extraen las variantes presentes en ChileGenomico por un lado y de 1000G por otro lado, para esto se utilizan los comandos `cut -f 2 chilean_all48_hg19_11.bim | sort -u > chilean_all48_hg19_11.snps` y `cut -f 2 $G/1kG_MDS5.bim | sort -u  > 1kG_MDS5.snps` donde se utilizado el comando *sort* para poder tenerlos por orden.
A continuación se buscan los SNP en comun entre las dos listas usando el comando `comm -12 chilean_all48_hg19_11.snps 1kG_MDS5.snps > common_snps.txt` con el cual se generará un archivo de texto plano con el listado de SNPs compartidos. Con esta lista de SNPs compartidos ahora se extrae la información de los SNP desde 1000G con el comando `plink --bfile $G/1kG_MDS5 --extract common_snps.txt --recode --make-bed --out 1kG_MDS6` y se realiza lo mismo para nuestro dataset de ChileGenomico con `plink --bfile chilean_all48_hg19_11 --extract common_snps.txt --make-bed --out chilean_all48_hg19_12`.

14. Con los 2 archivos de SNPs comunes par ChileGenomico y 1000G, el siquiente paso es homologar las versiones del genoma, ya que ChileGenomico es la version hg19 y para 1000G no estamos seguro. Para realizar la homologación de los SNPs de 1000G en las coordenadas de hg19 se usa el comando `awk '{print $2, $4}' chilean_all48_hg19_12.bim> buildhapmap.txt` que genera un archivo de texto plano con el ID de cada SNP y la posición fisica de cada uno. Se realiza a continuación el comando `plink --bfile 1kG_MDS6 --update-map buildhapmap.txt --make-bed --out 1kG_MDS7` con el que finalmente tendremos ambos dataset con las mismas coordenadas.

15. Se debe considerar antes de fusionar los dos dataset que: i) ambos se encuentren en el mismo genoma de referencia, ii) que en ambos casos la hebra sentido sea la misma y iii) una ultima depuración para asegurarse que los SNPs no difieran entre ellos.
i) Similar a los realizado en el punto anterior con los archivos .bim es que ahora se realiza en ChileGenomico usando como referencia 1000G y el comando `awk '{print $2, $5}' 1kG_MDS7.bim> 1kG_ref-list.txt` seguido de `plink --bfile chilean_all48_hg19_12 --reference-allele 1kG_ref-list.txt --make-bed --out chilean_all48_hg19_13`; para verificar que todo ocurrio correctamente se corre el comando `grep "Impossible" chilean_all48_hg19_13.log | wc -l` el cual arroja que hubieron 0 errores.
ii) Para resolver los potenciales problemas de hebra en sentido y antisentido es que se utilizan los comandos `awk '{print $2, $5, $6}' 1kG_MDS7.bim> 1kG_MDS7_tmp` y `awk '{print $2, $5, $6}' chilean_all48_hg19_13.bim > chilean_all48_hg19_13_tmp` los cuales generan nuevos archivos solo con las filas con los nombres de los SNP y los alelos 1 y 2, tanto para ChileGenomico como para 1000G. Al utilizar el comando `sort 1kG_MDS7_tmp chilean_all48_hg19_13_tmp | uniq -u > all_differences.txt` se genera un archivo de texto plano que contenga las filas unidas que sean producto de la union ordenada de ambos archivos, es decir, un listado de los SNP que presenten diferencias en el orden de los alelos. Finalmente cuenta las lineas en este archivo mediante el comando `wc -l all_differences.txt` obteniendo 0, osea que no hay discrepancias en la direccion de las hebras.
En el caso que el archivo hubiera mostrado discrepancias se deberian realizar los siguientes comandos `awk '{print $ 1}' all_differences.txt | sort -u > flip_list.txt` , `plink --bfile chilean_all48_hg19_13 -flip flip_list.txt --reference-allele 1kG_ref-list.txt --make-bed --out chilean_all48_hg19_14` lo cual genera un dataset con la lista de alelos volteadas para ChileGenomico. Posterior a esto deberia verificarse si siguen existiendo diferencias con los comandos `awk '{print $2, $5, $6}' chilean_all48_hg19_14.bim > chilean_all48_hg19_14_tmp`, `sort 1kG_MDS7_tmp chilean_all48_hg19_14_tmp | uniq -u> uncorresponding_SNPs.txt` y `wc -l uncorresponding_SNPs.txt` que nos arroja una cuenta de 0 lineas.
iii) Para asegurarse que ningun SNP presente problemas se utiliza el comando `awk '{print $ 1}' uncorresponding_SNPs.txt | sort -u > SNPs_for_exlusion.txt` el cual nos dara un listado ordenado de SNP que presentaron problemas. Se utiliza este listado para eliminar estos SNP desde los dataset de 1000G con `plink --bfile 1kG_MDS7 --exclude SNPs_for_exlusion.txt --make-bed --out 1kG_MDS8` y desde ChileGenomico con `plink --bfile chilean_all48_hg19_14 --exclude SNPs_for_exlusion.txt --make-bed --out chilean_all48_hg19_15`.

16. Ahora que no hay discrepancias se pueden unir los dos dataset mediante el comando `plink --bfile 1kG_MDS8 --bmerge chilean_all48_hg19_15.bed chilean_all48_hg19_15.bim chilean_all48_hg19_15.fam --allow-no-sex --make-bed --out MDS_merge` el cual genera el archivo de salida con los datos unidos *MDS_merge.bed*

17. El analisis de estructura poblacional requiere de un analisis MDS, el cual a su vez asume que los SNP no presentan ligación por lo que se utiliza el archivo de texto plano que listaba los SNP independientes y el comando `plink --bfile MDS_merge --extract indepSNP.prune.in --genome --out MDS_merge2` que a su vez analiza nuevamente los parentezcos al haber agregado mas muestras (las de 1000G) y a continuación el comando `plink --bfile MDS_merge --read-genome MDS_merge2.genome --cluster --mds-plot 10 --out MDS_merge3` el cual busca los agrupamientos de parentezcos y luego realiza la prueba MDS de los 10 primeros componentes principales y que todo lo guarde como un archivo *MDS_merge3*. 

18. El paso siguiente es generar un archivo con la información de las poblaciones usando el comando `wget ftp://ftp.1000genomes.ebi.ac.uk/vol1/ftp/release/20100804/20100804.ALL.panel` que obtiene desde internet el archivo descargable de la pagina web ingresada en el comando.
Con todos estos datos de poblaciones se hacen subset de datos poblacionares por etnia con los comandos:
```{bash}
awk '{print$1,$1,$2}' 20100804.ALL.panel > ethnicity_1kG.txt
sed 's/JPT/ASN/g' ethnicity_1kG.txt>ethnicity_1kG2.txt
sed 's/ASW/AFR/g' ethnicity_1kG2.txt>ethnicity_1kG3.txt
sed 's/CEU/EUR/g' ethnicity_1kG3.txt>ethnicity_1kG4.txt
sed 's/CHB/ASN/g' ethnicity_1kG4.txt>ethnicity_1kG5.txt
sed 's/CHD/ASN/g' ethnicity_1kG5.txt>ethnicity_1kG6.txt
sed 's/YRI/AFR/g' ethnicity_1kG6.txt>ethnicity_1kG7.txt
sed 's/LWK/AFR/g' ethnicity_1kG7.txt>ethnicity_1kG8.txt
sed 's/TSI/EUR/g' ethnicity_1kG8.txt>ethnicity_1kG9.txt
sed 's/MXL/AMR/g' ethnicity_1kG9.txt>ethnicity_1kG10.txt
sed 's/GBR/EUR/g' ethnicity_1kG10.txt>ethnicity_1kG11.txt
sed 's/FIN/EUR/g' ethnicity_1kG11.txt>ethnicity_1kG12.txt
sed 's/CHS/ASN/g' ethnicity_1kG12.txt>ethnicity_1kG13.txt
sed 's/PUR/AMR/g' ethnicity_1kG13.txt>ethnicity_1kG14.txt
```
Y luego se crea las etnias MAP (mapuche) y AYM (aimara) con los datos de ChileGenomico y el comando `awk '{if($1~/CDSJ/) pop="MAP"}{if($1~/ARI/) pop="AYM"} {print $1, $2, pop}' chilean_all48_hg19_14.fam > ethnicityfile_CLG.txt` el cual se concatena a las demas etnias con el comando `cat ethnicity_1kG14.txt ethnicityfile_CLG.txt | sed -e '1i \ FID IID ethnicity'> ethnicityfile.txt`

19. Todos estos subset poblacionales se pueden graficar con `Rscript $W/MDS_merged.R` que nos entrega el grafico:
[![MDS.png](https://i.postimg.cc/cLmnf0Mh/MDS.png)](https://postimg.cc/755hkvRJ)
Donde al graficar los 2 primeros componentes principales del MDS podemos ver una clara separación de la etnia africana, la asiatica y la europea, pero por otro lado, no hay una completa separación de las etnias americanas, aymaras y mapuches.

20. Finalmente la ancestría se calcula utilizando el programa *Admixture* el cual asume independencia de los SNP y se utiliza la lista de SNP independientes generada con antelación y el comando `plink --bfile MDS_merge --extract indepSNP.prune.in --make-bed --out MDS_merge_r2_lt_0.2`. Con este resultado podemos realizar el analisis con el comando `admixture -j4 --cv MDS_merge_r2_lt_0.2.bed 3 > MDS_merge_r2_lt_0.2.K3.log` que el comando *cv* que nos entrega el calculo de cross validation para un K o numero poblacional de 3. Se repite el mismo comando pero ahora para K= 4, 5 y 6 usando el comando `for k in $(seq 4 6)\
  do\
    admixture -j44 --cv MDS_merge_r2_lt_0.2.bed $k > MDS_merge_r2_lt_0.2.K$k.log	\	
  done`

21. Para poder visualizar los resultados se utiliza el programa R, pero primero se determina el orden en que va a graficar las etnias, para esto es el comando
```{r}
popinfo <- read.table("ethnicityfile.txt", as.is=T, header=T)
popinfo_ls <- split(popinfo, popinfo[,3])
names(popinfo_ls)
[1] "AFR" "AMR" "ASN" "AYM" "EUR" "MAP"
popinfo_sorted <- do.call(rbind, popinfo_ls[c("AFR", "EUR", "ASN", "AMR", "AYM", "MAP")])
write.table(popinfo_sorted, "popinfo_sorted.txt", sep="\t", row.names=F)
q()
```
Seguido del comando `Rscript $W/admixture_plot.R popinfo_sorted.txt MDS_merge_r2_lt_0.2.fam` que nos entrega el grafico:
[![admixture.png](https://i.postimg.cc/3wh0yjr0/admixture.png)](https://postimg.cc/jD8Sm77R)
Y si analizamos el menor valor cv para cada K obtenemos que el numero poblacional que mejor representa nuestra ancestría es 4 y su grafico ampliado es:
[![admi-final.png](https://i.postimg.cc/TwThtTBk/admi-final.png)](https://postimg.cc/QBnXtZ85)
En este grafico se observa que las poblaciones aymara y mapuche tienen un gran porcentaje de su genoma compartido con la poblacion amerindia, menor porcentaje europeo, poco porcentaje africano y casi nada de porcentaje asiatico.
