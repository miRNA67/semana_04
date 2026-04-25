# Semana 04: Basecalling de los datos de secuenciación - Visualización de la calidad y limpieza de los archivos FASTQ

## Logro de la sesión: 

Al finalizar la sesión, el estudiante realiza el basecalling de los archivos POD5 y la limpieza de los archivos FASTQ con diferentes herramientas bioinformáticas.

## Estructura de la práctica:

1. Acceso al servidor de cómputo
2.	Análisis de calidad de archivos FASTQ de Illumina
3.	Limpieza de los archivos FASTQ de Illumina
4.	Basecalling de los archivos POD5 de Nanopore
5.	Análisis de calidad de archivos FASTQ de Nanopore
6.	Limpieza de los archivos FASTQ de Nanopore
7.	Análisis de calidad y limpieza de los datos de secuenciación Nanopore generados en el curso

## Programas requeridos:

### Programas de acceso al servidor:

PuTTY v0.79 https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html
   - **Descripción:** PuTTY es un cliente SSH, Telnet y Rlogin gratuito y de código abierto para Windows y sistemas Unix. Se utiliza principalmente para establecer conexiones seguras de línea de comandos a servidores remotos.

WinSCP v6.1 https://winscp.net/eng/download.php
   - **Descripción:** WinSCP es un cliente SFTP, FTP, WebDAV, Amazon S3 y SCP gratuito y de código abierto para Windows. Permite la transferencia segura de archivos entre un ordenador local y servidores remotos mediante una interfaz gráfica de usuario. 

### Programas bioinformáticos:

Dorado v0.9.1 https://github.com/nanoporetech/dorado
   - **Descripción:** Dorado es una herramienta de Oxford Nanopore Technologies, sucesora de Guppy, para la llamada de bases (basecalling) de las señales eléctricas generadas por sus secuenciadores de ADN. Al igual que Guppy, también incluye funcionalidades para el multiplexado y el filtrado de reads, pero con mejoras en rendimiento y precisión.
   - 
FastQC v0.12.1 http://www.bioinformatics.babraham.ac.uk/projects/fastqc/
   - **Descripción:** FastQC es una herramienta de control de calidad para datos de secuenciación de alto rendimiento. Proporciona un informe detallado que ayuda a identificar posibles problemas en los datos brutos antes del análisis posterior.

Minimap2 v2.28 https://github.com/lh3/minimap2
   - **Descripción:** Minimap2 es un alineador de secuencias versátil y de alta velocidad diseñado para lecturas largas (Nanopore y PacBio).
     
MultiQC v1.28.0 https://multiqc.info
   - **Descripción:** MultiQC es una herramienta que agrega informes de control de calidad de múltiples herramientas de análisis bioinformático en un único informe HTML interactivo. Es compatible con una amplia gama de herramientas, incluyendo FastQC, NanoPlot, PycoQC y Trim Galore!, facilitando la revisión y comparación de los resultados de control de calidad de múltiples muestras.
   - 
Nanofilt v2.8.0 https://github.com/wdecoster/nanofilt
   - **Descripción:** NanoFilt es una herramienta para filtrar datos de secuenciación de Nanopore basándose en la calidad y la longitud de los reads. Permite seleccionar reads de alta calidad para análisis posteriores.

NanoPlot v1.41.6 https://github.com/wdecoster/NanoPlot
   - **Descripción:** NanoPlot es una herramienta para la visualización de datos de secuenciación de Nanopore. Genera varios tipos de gráficos para evaluar la calidad y las características de los reads, como la distribución de longitudes y la calidad a lo largo de los reads.

PycoQC v2.5.2 https://github.com/a-slide/pycoQC
   - **Descripción:** PycoQC es una herramienta para el control de calidad de datos de secuenciación de Oxford Nanopore, similar a FastQC pero diseñada específicamente para este tipo de datos. Genera informes interactivos en HTML con diversas métricas de calidad.

Porechop v0.2.4 https://github.com/rrwick/Porechop
   - **Descripción:** Porechop es una herramienta para identificar y recortar adaptadores de horquilla (hairpin adapters) que a veces se forman durante la secuenciación de ADN largo con tecnología de Oxford Nanopore. También puede detectar y dividir reads concatenados (chimeric reads).

TrimGalore v0.6.10 https://github.com/FelixKrueger/TrimGalore
   - **Descripción:** Trim Galore! es un wrapper alrededor de Cutadapt y FastQC para realizar el recorte de adaptadores y el control de calidad en datos de secuenciación de alto rendimiento. Automatiza el proceso de recorte y genera informes de calidad.

Trimmomatic v0.39 http://www.usadellab.org/cms/?page=trimmomatic
   - **Descripción:** Trimmomatic es una herramienta flexible y rápida para realizar el recorte de adaptadores y el filtrado de calidad en datos de secuenciación de Illumina. Permite eliminar secuencias de adaptadores, bases de baja calidad y reads demasiado cortos.

YACRD v0.6.2 https://github.com/natir/yacrd
   - **Descripción:** YACRD (Yet Another Chimeric Read Detector) es una herramienta especializada en la detección de lecturas quiméricas y regiones sin cobertura en datos de secuenciación de lecturas largas. Permite "limpiar" (scrubb) o dividir las lecturas donde se detectan uniones accidentales, mejorando significativamente la contigüidad y precisión de los ensamblajes genómicos posteriores.

## Metodología:

## 1.	Acceso al servidor de cómputo:

### Abrir el programa PuTTY, colocar el hostname ( 10.142.250.66 ) y port ( 22 ), y dar clic en Open:

<img width="500" alt="image" src="https://github.com/user-attachments/assets/92f89dbb-1a21-411d-adb5-38fe486a5567" />



### En la terminal abierta, escribir su usuario y contraseña correspondiente para tener acceso al servidor de cómputo Tensor:
 
<img width="700" alt="image" src="https://github.com/user-attachments/assets/4d246e93-c59c-4749-a2dd-03db25c53654" />



### Abrir el programa WinSCP, colocar el hostname ( 10.142.250.66 ) y port ( 22 ), escribir su usuario y contraseña correspondiente para tener acceso al servidor de cómputo Tensor, y hacer clic en Login:

<img width="500" alt="image" src="https://github.com/user-attachments/assets/ef4dc253-ce4a-417d-b761-39692d2a011a" />

<img width="500" alt="image" src="https://github.com/user-attachments/assets/577debca-6085-47c5-9bbd-73688bfa8bb0" />


## 2. Análisis de calidad de archivos FASTQ de Illumina

```bash
cd

mkdir genomics

cd genomics

mkdir quality

cd quality

mkdir illumina

cd illumina

conda activate quality

fastqc -t 2 /data/2025_1/database/illumina/CAT_R1.fastq.gz -o .
```

> **Comentario:** 
> - `-t 2`: Esta opción especifica el número de hilos (threads) que FastQC debe utilizar. Al usar múltiples hilos, el programa puede procesar los datos más rápidamente. En este caso, se están usando 2 hilos.
> - `/data/2024_2/genome/illumina/CAT_R1.fastq.gz`: Esta parte del comando indica la ubicación del archivo que FastQC debe analizar.
> - `-o .`: Esta opción define el directorio de salida. El punto "." representa el directorio actual. Esto significa que los informes HTML generados por FastQC se guardarán en el mismo directorio donde se ejecuta el comando.

```bash
Repetir lo mismo para la biblioteca CAT_R2.fastq.gz
```

```bash
multiqc -o raw_illumina .
```
> **Comentario:**
> - `-o raw_illumina`: Esta opción especifica el directorio de salida donde se guardará el informe HTML generado por MultiQC.
> - `.`: Representa el directorio actual. Esto le dice a MultiQC que busque archivos de resultados (los que ha generado FastQC por ejemplo) dentro del directorio en el que estás ejecutando el comando. MultiQC buscará automáticamente archivos de salida de las herramientas de control de calidad compatibles que se encuentren en el directorio actual y sus subdirectorios.

## 3.	Limpieza de los archivos FASTQ de Illumina

### Limpieza con trim galore

```bash
cd ~/genomics

mkdir trimming

cd trimming

mkdir illumina

cd illumina

mkdir trim_galore

cd trim_galore

trim_galore --quality 30 --length 50 --phred33 --cores 2 --fastqc --paired /data/2025_1/database/illumina/CAT_R1.fastq.gz /data/2025_1/database/illumina/CAT_R2.fastq.gz
```

> **Comentario:**
> - `--quality 30`: Esta opción especifica el umbral de calidad para el recorte de bases. Las bases con una calidad inferior a 30 (en escala Phred33) serán recortadas del final de las lecturas.
> - `--length 50`: Esta opción establece la longitud mínima de las lecturas después del recorte. Las lecturas que sean más cortas que 50 bases serán descartadas.
> - `--phred33`: Esta opción indica que los datos de calidad de las bases están en la escala Phred33, que es la escala más común utilizada en la secuenciación Illumina.
> - `--cores 2`: Esta opción especifica el número de núcleos de procesamiento que Trim Galore! debe utilizar. En este caso, se están utilizando 2 núcleos para acelerar el procesamiento.
> - `--fastqc`: Esta opción le indica a Trim Galore! que ejecute FastQC automáticamente después del recorte para generar informes de control de calidad de los datos recortados.
> - `-paired`: Esta opción indica que los datos son pareados (paired-end), lo que significa que las lecturas vienen en pares (R1 y R2).
> - `/data/2025_1/database/illumina/CAT_R1.fastq.gz`: Esta es la ruta del archivo FASTQ comprimido que contiene las lecturas R1 (la primera lectura del par).
> - `/data/2025_1/database/illumina/CAT_R2.fastq.gz`: Esta es la ruta del archivo FASTQ comprimido que contiene las lecturas R2 (la segunda lectura del par).

```bash
multiqc -o trimming_trim_galore .
```

### Limpieza con trimmomatic

```bash
cd ~/genomics/trimming/illumina

mkdir trimmomatic

cd trimmomatic
```

> **Comentario:** Crear el archivo NexteraPE.fa

```bash
nano NexteraPE.fa

>PrefixNX/1
AGATGTGTATAAGAGACAG
>PrefixNX/2
AGATGTGTATAAGAGACAG
>Trans1
TCGTCGGCAGCGTCAGATGTGTATAAGAGACAG
>Trans1_rc
CTGTCTCTTATACACATCTGACGCTGCCGACGA
>Trans2
GTCTCGTGGGCTCGGAGATGTGTATAAGAGACAG
>Trans2_rc
CTGTCTCTTATACACATCTCCGAGCCCACGAGAC
```

```bash
trimmomatic PE /data/2025_1/database/illumina/CAT_R1.fastq.gz /data/2025_1/database/illumina/CAT_R2.fastq.gz CAT_R1.trim.fastq.gz CAT_R1.unpaired.fastq.gz CAT_R2.trim.fastq.gz CAT_R2.unpaired.fastq.gz ILLUMINACLIP:NexteraPE.fa:2:30:10 SLIDINGWINDOW:4:30 MINLEN:50 -threads 2
```

> **Comentario:**
> - `PE`: Indica que los datos son pareados (paired-end).
> - `/data/2025_1/database/illumina/CAT_R1.fastq.gz`: Esta es la ruta del archivo FASTQ comprimido que contiene las lecturas R1 (la primera lectura del par).
> - `/data/2025_1/database/illumina/CAT_R2.fastq.gz`: Esta es la ruta del archivo FASTQ comprimido que contiene las lecturas R2 (la segunda lectura del par).
> - `T4_R1.trim.fastq.gz`: Archivo de salida para las lecturas R1 recortadas y emparejadas.
> - `T4_R1.unpaired.fastq.gz`: Archivo de salida para las lecturas R1 que quedaron sin par después del recorte.
> - `T4_R2.trim.fastq.gz`: Archivo de salida para las lecturas R2 recortadas y emparejadas.
> - `T4_R2.unpaired.fastq.gz`: Archivo de salida para las lecturas R2 que quedaron sin par después del recorte.
> - `ILLUMINACLIP:NexteraPE.fa:2:30:10`: Son los parámetros para el recorte de adaptadores (mismatch allowance:palindrom match threshold:simple match threshold).
> - `SLIDINGWINDOW:4:30`: Indica que se va a utilizar una ventana deslizante de 4 bases y que la calidad promedio mínima dentro de la ventana debe ser 30.
> - `MINLEN:50`: Esta opción establece la longitud mínima de las lecturas después del recorte. Las lecturas que sean más cortas que 50 bases serán descartadas.

```bash
fastqc -t 2 *.trim.fastq.gz -o .

multiqc -o trimming_trimmomatic .
```

## 4. Basecalling de los archivos POD5 de Nanopore

#### Basecalling

```bash
cd ~/genomics/basecalling

mkdir pod5_db_sup

cd pod5_db_sup

dorado basecaller sup --kit-name SQK-NBD114-24 --min-qscore 10 --device 'cuda:0' --barcode-both-ends --models-directory 
/data/software/dorado-0.9.1-linux-x64/models /data/2025_1/database/nanopore/pod5/barcode15.pod5 > b15_calls.bam
```

> **Comentario:** 

> - `sup`: Esta opción indica que se debe utilizar el modelo de basecalling de "super precisión" (super accuracy). Estos modelos están entrenados para ofrecer una mayor exactitud en la llamada de bases.
> - `--kit-name SQK-NBD114-24`: Este parámetro especifica el nombre del kit de secuenciación utilizado. En este caso, es el kit SQK-NBD114-24. Esta información puede ayudar a Dorado a seleccionar los modelos de basecalling más apropiados.
> - `--min-qscore 10`: Esta opción establece un umbral de calidad mínima para las bases llamadas. Solo las bases con una puntuación de calidad (Q-score) igual o superior a 10 se incluirán en la salida. El Q-score es una medida de la probabilidad de que una base llamada sea incorrecta. Un Q-score de 10 significa una probabilidad de error de 1 en 10.
> - `--device 'cuda:0'`: Esto indica que Dorado debe utilizar la primera GPU habilitada para CUDA (índice 0) disponible en tu sistema para acelerar el proceso de basecalling. El uso de la GPU puede reducir significativamente el tiempo de procesamiento.
> - `--barcode-both-ends`: Esta opción le dice a Dorado que intente identificar códigos de barras (barcodes) en ambos extremos de las lecturas de secuencia. Esto es útil si tu protocolo de secuenciación incluyó el uso de códigos de barras en ambos extremos para multiplexar muestras.
> - `--models-directory /data/software/dorado-0.9.1-linux-x64/models`: Este parámetro especifica la ruta al directorio donde Dorado puede encontrar los modelos de basecalling pre-entrenados. Es importante que la ruta sea correcta para que Dorado pueda cargar los modelos necesarios.
> - `/data/2025_1/database/nanopore/pod5/barcode15.pod5`: Esta es la ruta al archivo de entrada POD5 que contiene los datos de señal sin procesar para una muestra con el código de barras (barcode) número 15. Dorado realizará el basecalling de los datos contenidos en este archivo.
> - `> b15_calls.bam`: Esto redirige la salida estándar (stdout) del comando Dorado al archivo llamado b15_calls.bam. En este caso, Dorado generará las secuencias base-llamadas y la información de alineamiento (si se realiza) en formato BAM (Binary Alignment Map), que es un formato común para almacenar datos de secuenciación alineados o sin alinear.

#### Conversión de bam a fastq

```bash
for file in *.bam; do prefix="${file%.bam}"; samtools sort -n "$file" -o "${prefix}_sorted.bam"; done

for file in *_sorted.bam; do prefix="${file%.bam}"; bedtools bamtofastq -i "${prefix}.bam" -fq "${prefix}.fastq"; done

seqkit stats -a -j 4 *_sorted.fastq > stats_sorted_fastq.txt
```

> **Comentario:** 
> - `samtools sort -n`: Ordena los archivos BAM por nombre de lectura.
> - `bedtools bamtofastq`: Convierte los archivos BAM ordenados a formato FASTQ.
> - `seqkit stats`: Calcula las estadísticas de archivos FASTQ que han sido previamente ordenados (-a: todas las estadísticas y -j: número de hilos).

```bash
cat stats_sorted_fastq.txt

file                    format  type  num_seqs    sum_len  min_len  avg_len  max_len   Q1   Q2       Q3  sum_gap    N50  N50_num  Q20(%)  Q30(%)  AvgQual  GC(%)  sum_n
b15_calls_sorted.fastq  FASTQ   DNA      8,056  9,351,266       26  1,160.8   26,983  555  814  1,298.5        0  1,423      721   89.24   80.11    19.24   45.7      0
```

```bash
mv b15_calls_sorted.fastq b15.fastq
```

```bash
head b15.fastq

@0a3b5933-6ecd-4ab8-b6fe-323eeee7a012
TAAGGTTAAAACGAGTCTCTTGGGACCCATAGACAGCACCTCAAGAGCCGTGTCTCCTGTCCTTAGTGTAATCAAGCTTTTGTTTATACTTGTCAATCAGCCGCTCGTTTTCTTTGAAAATTCTGGCGGTATGAGGGCTGACCTGGTAACTTGCGATACTTGTCATTGAACGTTTTTTAAACATTTTGAACAGTTTCGCTTCTTGTTTCCGGCTGCCCCGTTTTGAAATGCCTGCTCCATTTAACCGTCACCTTCCTCTTCTATTGGCAGCATTAAATCATAAATGCTCGTTAGCGATGTGAAAAGCAAATAATCGAATTCCGTCAACAGGTTTTCCGACGTGAGTTTGATCACGTAATGGCGGTTCTGGACTGTAAACGGAATAAGCACAAGCCTGCCTTTTTGATCATAGTAGACGTCTTTACGGTTAAGACGGGACTGAACGTCTGCCGCATCAGGCATATGCTCCGTCAAGCGGTCCTTATCCAATTGTGCGGAATAGTCAAGGAAGCCGTGACATTCATTTTTTCGGCATAAGCGGCCAGCAGTCTGCT
+
EFDCDDFCEGFFGGKHJJPSE6666SLNSSSSJGGSRMPMJSSSSSSSSSSSSRSPSSNSLOKIIISSSRLS:4322/..:8=@CDSOSSSNSQSSSQSSMQNSSOSSSSSSNMRBSSSSSSOSNSSQSSNSNSSSSSSLSSQMKLISSSSSSSNQSSSLIQSSSSSSSSSQSSSSSSSSSSNSSSS////*,,,.B>>>=66:33K@22CBGSSSE@2+SSKSLNSSSSSSSMIINCBA@BSSSSSSSSSNQSSSSOSSSSRSSSMJSSSLSSMSSSSSSSSSSSSSSSSSPSSSSSSSLSSSSSSLOSSNSSSSSSSSOSSSSSKHSSSSSSSSSSLIOSSSMNSSMSSSSSSSMSSPSSSSSSOSSSSSSOSSSSSPSSSSLMOSDBBBBGDBBB@==QNPSSSSSSSSSSSSSSSSLSSSSNSSSSSSSSOSISJGNQSSJJLSOMLLJKKKOSSSSSSSQSSNSJQQKJEEFSSSSQPJJKKFHGFAA>=<?=?@3222***=BFGJKSSMMJHSLKE==GCBBCEHHISQKFEBA?==<<;643130)
@0a3d8a47-5c4d-4d13-913c-3b6f598d1449
TAAGGTTAAAACGAGTCTCTTGGGACCCATAGACAGCACCTTTTTTGTTTCATCGGAGCGCCGTTAGATTGGTTTTTATTTTTTCTGCTGCTCATTACGGGGCTTGCCAAAAAAATAAAGCATTGGCTGGAAGCAGCGGTGCGCTTTCGGGTGCTGCAAATCGTAAGCTTCGTATTTGTGATTTCACTCATCATTACGGTGGCTTCGCTTCGCTTGAGTGGATCGGATATCGGGTTTCGCTTGCGTATCATATTTCGACGCAGACAACAGCAAGCTGGATAAGAGACCATGTCATTGATTTCTGGATCAGCTTTCCGCTGTTTGCCGTGTGTGTGCTTGTGTTTTACTGGCTGATCACAAAGCATACAAAAAAATGGTGGTTTTACGCTTGGTGTAC
+
7OLSSMJJEEDE;:99>ED>AAABDISSJKIHFHMMNJIF@=666HG0+*):::;<CJJKLJOPIDDDDI>;:;;???@CIKSSSSSBC:=BB@@BDIIKSSOLNP:77788SSSSOSRNNKHGHHPMONKCARSMMSOOJKNA><<45555OONSSLNKLPOMORSQSSLCAD>@?)B@??@:*****))))))(()))43,,,++043-+,.33===,,+++?BBBPMJJSKSSSCA<3>AAAABHJ7656:=10000?CA@@@@KKLMPLSSSMIKGHECEGKKSHHID=<<::>>>IGGEEISJJJIJMSKMFFHHJJJNSSNMOSOSPSOQPSSSSSPMKSSSRSSSRPMSKK@@@@@RSNJ<4<5333634489::8988----,++++(&
@0a3f050d-7fd8-4d74-a730-655bedec67ec
AGGGCTTATTACTGATAAAAAAAGCAAAACGATTTATAAAATTGAGTCAAAACGGTCTTTGCAGCCGGGCATATACGCATTCAAGGTTTACAGACCTCTGAAGGGTACCCGGCCGACGAAGAAAAATTTGAGTGGTCAAAACCGATGAAACTCGTCAAATGCCGGGAACAGGCGACCGTTTCGAATATAAAACGGAGAAAGAGCCGGCTGAGCCGGTAAAAGAAAGCGGGGAAGAACATGAAAAAAACGCTGAAACTGATGAGTAATATTTTGTATGCCAGTCATCTTCAGCTTGATTATTGTGCTGGCGTTAACGGTGATTCAGACCCGGGCTTCCGGGGGTGAGCCGGCCATTTTCGGCTATACA
```

```bash
gzip b15.fastq
```

## 5. Análisis de calidad de archivos FASTQ de Nanopore

### Visualización de la calidad

```bash
cd ~/genomics/quality

mkdir nanopore

cd nanopore

NanoPlot -t 2 --fastq ~/genomics/basecalling/pod5_db_sup/b15.fastq.gz -p b15_sup_raw_ -o b15_sup_raw --maxlength 1000000 --only-report

cat b15_sup_raw/b15_sup_raw_NanoStats.txt

General summary:         
Mean read length:              1,160.8
Mean read quality:                18.9
Median read length:              814.0
Median read quality:              20.3
Number of reads:               8,056.0
Read length N50:               1,423.0
STDEV read length:             1,257.0
Total bases:               9,351,266.0
Number, percentage and megabases of reads above quality cutoffs
>Q10:   8054 (100.0%) 9.4Mb
>Q15:   7484 (92.9%) 8.9Mb
>Q20:   4292 (53.3%) 5.4Mb
>Q25:   1024 (12.7%) 1.0Mb
>Q30:   162 (2.0%) 0.1Mb
Top 5 highest mean basecall quality scores and their read lengths
1:      43.1 (332)
2:      43.1 (332)
3:      41.9 (351)
4:      41.9 (351)
5:      41.3 (371)
Top 5 longest reads and their mean basecall quality score
1:      26983 (18.4)
2:      26983 (18.4)
3:      20990 (26.5)
4:      20990 (26.5)
5:      14663 (23.3)
```

> **Comentario:** 
> - `--fastq /home/ins_user/genomics/raw_data/nanopore/b01_fast.fastq`: Indica la ruta del archivo FASTQ que contiene las lecturas de secuenciación de ONT que se van a analizar.
> - `-p b15_sup_raw_`: Define el prefijo que se usará para los nombres de los archivos de salida. En este caso, todos los gráficos generados comenzarán con "b15_sup_raw_".
> - `-o b15_sup_raw`: Especifica el directorio de salida donde se guardarán los gráficos. Si el directorio no existe, NanoPlot lo creará.
> - `--maxlength 1000000`: Establece la longitud máxima que se mostrará en los gráficos. Las lecturas que superen esta longitud serán truncadas en las visualizaciones. Esto ayuda a enfocar el análisis en la mayoría de las lecturas y evita que las lecturas extremadamente largas distorsionen la visualización.

## 6.	Limpieza de los archivos FASTQ de Nanopore

### Eliminación de adaptadores

```bash
cd ~/genomics/trimming/

mkdir nanopore

cd nanopore

porechop -t 10 -i ~/genomics/basecalling/pod5_db_sup/b15.fastq.gz -o b15_sup_porechop.fastq.gz > b15_porechop.log 2> b15_porechop.err
```

> **Comentario:** 
> - `-i ~/genomics/basecalling/pod5_db_sup/b15.fastq.gz`: Esta opción indica la ruta del archivo FASTQ de entrada. Este es el archivo que contiene las lecturas de secuenciación de ONT que se van a procesar.
> - `-o b15_sup_porechop.fastq.gz`: Esta opción especifica el nombre del archivo FASTQ de salida comprimido con gzip. Este archivo contendrá las lecturas después de que Porechop haya recortado los adaptadores y separado las lecturas concatenadas.

### Eliminación de quimeras

```bash
cd ~/genomics/trimming/nanopore

minimap2 -x ava-ont -g 500 -t 10 b15_sup_porechop.fastq.gz b15_sup_porechop.fastq.gz > b15_overlap.paf

yacrd -i b15_overlap.paf -o b15_report.yacrd -c 4 -n 0.4 scrubb -i b15_sup_porechop.fastq.gz -o b15_yacrd.fastq.gz
```

> **Comentario:** 
> - `minimap2 -x ava-ont`: Utiliza el algoritmo Minimap2 con el preajuste (preset) para solapamientos de lecturas largas de Nanopore.
> - `-g 500`: Establece la distancia máxima para el llenado de brechas (gaps) entre semillas en 500 bases. Es una configuración recomendada para mejorar la sensibilidad en datos R10.
> - `-t 10`: Indica que el servidor utilizará 10 hilos (CPUs) para procesar el alineamiento de forma paralela y rápida.
> - `b15_sup_porechop.fastq.gz b15_sup_porechop.fastq.gz`: ERealiza un mapeo de tipo "all-vs-all", comparando cada lectura contra todas las demás de la misma muestra para encontrar solapamientos consistentes.
> - `> b15_overlap.paf`: Redirige los resultados al archivo "b15_overlap.paf" en formato PAF (Pairwise Alignment Format).
> - `yacrd -i b15_overlap.paf`: Carga el archivo de solapamientos generado anteriormente como entrada para el detector de quimeras.
> - `-o b15_report.yacrd`: Crea un archivo de reporte con la clasificación de cada lectura (Chimeric, NotCovered o NotBad).
> - `-c 4`: Define el umbral de cobertura mínima. Las regiones con menos de 4 lecturas de soporte se consideran potencialmente "malas" o quiméricas.
> - `-n 0.4`: Exige que al menos el 40% de la lectura esté cubierta por otros solapamientos; de lo contrario, se marca como no cubierta.
> - `scrubb`: Modo de operación que limpia la secuencia. En lugar de borrar la lectura completa si es quimérica, yacrd la corta en los puntos de unión falsos y conserva las partes reales.
> - `-i b15_sup_porechop.fastq.gz`: Indica el archivo FASTQ original que contiene las secuencias físicas que serán procesadas y cortadas.
> - `-o b15_yacrd.fastq.gz`: Genera el archivo final limpio y comprimido, listo para ser utilizado en el ensamblaje de genomas.

### Eliminación de lecturas considerando su calidad y longitud

```bash
gunzip -c ~/genomics/trimming/nanopore/b15_yacrd.fastq.gz | NanoFilt -q 10 --length 1000 | gzip > b15_sup_nanofilt.fastq.gz
```

> **Comentario:** 
> - `gunzip -c ~/genomics/trimming/nanopore/b15_yacrd.fastq.gz`: Descomprime el archivo "b15_yacrd.fastq.gz".
> - `NanoFilt -q 10 --length 1000`: Filtra las lecturas descomprimidas utilizando NanoFilt, manteniendo solo aquellas que tengan un puntaje de calidad mínimo de 10 y una longitud mínima de 1000 bases.
> - `gzip > b15_sup_nanofilt.fastq.gz`: Comprime las lecturas filtradas y las guarda en un nuevo archivo llamado "b15_sup_nanofilt.fastq.gz".
> - `|`: Este símbolo es una "tubería" (pipe) que conecta la salida de un comando a la entrada de otro.

```bash
seqkit rename -n b15_sup_nanofilt.fastq.gz -o b15_rename.fastq.gz

seqkit stats -a -j 10 *.fastq.gz > b15_stats_fastq.txt
```

## 7.	Análisis de calidad y limpieza de los datos de secuenciación Nanopore generados en el curso

> - `Realizar todo el proceso de visualización de calidad y limpieza del FASTQ de su respectivo barcode.`
> - `Localización de los archivos FASTQ:`

```bash
tree /data/2026_1/genomics/
```

> - `Mantener la siguiente estructura de carpetas:`

```bash
~/genomics/
├── basecalling/          # Archivos BAM y FASTQ iniciales (Dorado)
│   └── pod5_db_sup/      
├── quality/              # Informes de FastQC, NanoPlot y PycoQC
│   ├── illumina/
│   └── nanopore/
└── trimming/             # Archivos procesados y limpios
    ├── illumina/
    └── nanopore/         # Resultados de Porechop, YACRD y NanoFilt`
```

> **Bitácora bioinformática:** 
> - `Sorpresa!`
