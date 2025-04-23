# Semana 04: Basecalling de los datos de secuenciación - Visualización de la calidad y limpieza de los archivos FASTQ

## Logro de la sesión: 

Al finalizar la sesión, el estudiante realiza el basecalling de los archivos FAST5 y la limpieza de los archivos FASTQ con diferentes herramientas bioinformáticas.

## Estructura de la práctica:

1.  Acceso al servidor de cómputo
2.	Análisis de calidad de archivos FASTQ de Illumina
3.	Limpieza de los archivos FASTQ de Illumina
4.	Basecalling de los archivos POD5 y FAST5
5.	Análisis de calidad de archivos FASTQ de Nanopore
6.	Limpieza de los archivos FASTQ de Nanopore

## Programas requeridos:

### Programas de acceso al servidor:

PuTTY v0.79 https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html
   - **Descripción:** PuTTY es un cliente SSH, Telnet y Rlogin gratuito y de código abierto para Windows y sistemas Unix. Se utiliza principalmente para establecer conexiones seguras de línea de comandos a servidores remotos.

WinSCP v6.1 https://winscp.net/eng/download.php
   - **Descripción:** WinSCP es un cliente SFTP, FTP, WebDAV, Amazon S3 y SCP gratuito y de código abierto para Windows. Permite la transferencia segura de archivos entre un ordenador local y servidores remotos mediante una interfaz gráfica de usuario. 

### Programas bioinformáticos:

FastQC v0.12.1 http://www.bioinformatics.babraham.ac.uk/projects/fastqc/
   - **Descripción:** FastQC es una herramienta de control de calidad para datos de secuenciación de alto rendimiento. Proporciona un informe detallado que ayuda a identificar posibles problemas en los datos brutos antes del análisis posterior.

Guppy v6.5.7 https://community.nanoporetech.com/downloads/
   - **Descripción:** Guppy es un software desarrollado por Oxford Nanopore Technologies para la llamada de bases (basecalling) de las señales eléctricas generadas por sus secuenciadores de ADN. También incluye funcionalidades para el multiplexado y el filtrado de reads.

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

## Metodología:

## 1.	Acceso al servidor de cómputo (20 minutos):

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

## 4. Basecalling de datos de secuenciación Nanopore

### Basecalling de FAST5

```bash
cd ~/genomics

mkdir basecalling

cd basecalling

guppy_basecaller -i /home/ins_user/genomics/raw_data/fast5 -s fast5 -c dna_r10.4_e8.1_fast.cfg
```

> **Comentario:** 
> - `-i /home/ins_user/genomics/raw_data/fast5`: Esta opción especifica el directorio de entrada donde se encuentran los archivos de datos de secuenciación crudos (en formato FAST5). Guppy leerá todos los archivos FAST5 dentro de este directorio.
> - `-s fast5`: Esta opción especifica el directorio de salida donde se escribirán los datos convertidos. La bandera -s significa "ruta de guardado" (save path). Guppy creará un nuevo directorio llamado "fast5" dentro del directorio de trabajo actual y almacenará los archivos de salida allí.
> - `-c dna_r10.4_e8.1_fast.cfg`: Esta opción especifica el archivo de configuración que se utilizará para el "basecalling". El archivo dna_r10.4_e8.1_fast.cfg contiene ajustes optimizados para la celda de flujo R10.4 y el modelo de "basecalling" "fast" (rápido). Este modelo prioriza la velocidad sobre la máxima precisión.

### Basecalling de POD5

#### Obtención de archivos POD5
```bash
cd ~/genomics/basecalling

mkdir pod5

cd pod5

conda deactivate

pod5 convert fast5 /home/ins_user/genomics/raw_data/fast5/*.fast5 --output converted.pod5
```

> **Comentario:** Esta línea de código utiliza `pod5` para convertir todos los archivos FAST5 en el directorio `fast5` a un único archivo POD5 llamado `converted.pod5`

#### Basecalling y desmultiplexación

```bash
dorado basecaller fast --kit-name SQK-NBD114-24 --min-qscore 8 --barcode-both-ends converted.pod5 > calls.bam
```

> **Comentario:** 
> - `basecaller fast`: Esto invoca el programa Dorado en modo "basecaller" (llamador de bases) y utiliza el modo "fast" (rápido). El modo rápido prioriza la velocidad sobre la precisión.
> - `--kit-name SQK-NBD114-24`: Especifica el nombre del kit de secuenciación utilizado.
> - `--min-qscore 8`: Establece un umbral de calidad mínimo de 8 para las lecturas.
> - `--barcode-both-ends`: Indica que los códigos de barras están presentes en ambos extremos de las lecturas.
> - `> calls.bam`: Redirige la salida a un archivo BAM llamado `calls.bam`.

```bash
dorado demux --kit-name SQK-NBD114-24 --output-dir barcodes --emit-summary calls.bam
```

> **Comentario:** 
> - `demux`: Invoca la función de desmultiplexación de la herramienta Dorado.
> - `--kit-name SQK-NBD114-24`: Indica el kit de secuenciación que se usó. Dorado necesita esta información para saber qué códigos de barras buscar y cómo interpretarlos.
> - `--output-dir barcodes`: Especifica que los archivos de salida se guarden en un directorio llamado "barcodes". Dentro de este directorio, se creará un archivo BAM para cada código de barras, conteniendo las lecturas correspondientes.
> - `--emit-summary`: Indica que se genere un archivo de resumen que contenga información sobre la clasificación de las lecturas por código de barras.
> - `calls.bam`: Es el archivo de entrada, que en este caso es el archivo BAM generado por el comando dorado basecaller que vimos anteriormente.

```bash
cd barcodes
```

> **Comentario:** 
> - `--kit-name SQK-16S024`: Especifica el nombre del kit de secuenciación utilizado.
> - `--min-qscore 8`: Establece un umbral de calidad mínimo de 8 para las lecturas.
> - `--barcode-both-ends`: Indica que los códigos de barras están presentes en ambos extremos de las lecturas.
> - `> calls.bam`: Redirige la salida a un archivo BAM llamado `calls.bam`.
> - `--output-dir barcodes`: Especifica el directorio de salida para los archivos demultiplexados.
> - `--emit-summary`: Genera un resumen de la ejecución de secuenciación.

```
cat barcoding_summary.txt | head

filename	read_id	barcode
converted.pod5	79575555-aded-46c6-9f18-e9556fbd576d	SQK-NBD114-24_barcode15
converted.pod5	00870608-57ee-497a-a738-b31d4876c161	unclassified
converted.pod5	0054a804-cf1f-4218-9877-f490288b5675	unclassified
converted.pod5	0046d92e-d735-4f25-9fb3-6b80ef88a3fd	unclassified
converted.pod5	032006e4-6d5a-4e8e-a1f7-e6f695d732ad	unclassified
converted.pod5	03d484a9-6644-4856-bf4e-ddf071e2a52e	unclassified
converted.pod5	013562b4-3582-4bf5-852d-11297ed2b35f	unclassified
converted.pod5	037de90d-c40a-4ae4-8b7b-887350c6c219	unclassified
converted.pod5	043aa25b-75b0-4363-ab12-3c3fe75dcf89	unclassified
```

#### Resumen de la secuenciación 

```bash
for file in *.bam; do prefix="${file%.bam}"; dorado summary "$file" > "${prefix}_summary.tsv"; done
```

> **Comentario:** Genera un resumen para cada archivo BAM en el directorio y lo guarda en un archivo TSV.

```
cat bcf4b7732185c1a3353d1b4fe80266cd3ac60162_SQK-NBD114-24_barcode13_summary.tsv | head

filename	read_id	run_id	channel	mux	start_time	duration	template_start	template_duration	sequence_length_template	mean_qscore_template	barcode
converted.pod5	05886056-e7c4-4c7f-9f61-a1f025b940a4	bcf4b7732185c1a3353d1b4fe80266cd3ac60162	31	1	9069.31	1.7564	9069.31	1.7564	678	10.5307	SQK-NBD114-24_barcode13
converted.pod5	a87c7559-6f22-463c-b288-a281fa7b0b41	bcf4b7732185c1a3353d1b4fe80266cd3ac60162	66	1	9083.14	0.9576	9083.14	0.9576	219	11.1093	SQK-NBD114-24_barcode13
converted.pod5	44432ea9-99d6-4f46-aba7-82a288b6c9ff	bcf4b7732185c1a3353d1b4fe80266cd3ac60162	132	3	8941.51	1.6908	8941.51	1.6908	621	9.64351	SQK-NBD114-24_barcode13
converted.pod5	af970a9d-239a-4623-80a3-7e26485f66ae	bcf4b7732185c1a3353d1b4fe80266cd3ac60162	328	3	9135.62	3.1966	9135.62	3.1966	1267	12.403	SQK-NBD114-24_barcode13
converted.pod5	9a105f99-ef53-43bb-9e26-321139cd8bad	bcf4b7732185c1a3353d1b4fe80266cd3ac60162	434	4	9016.32	1.05	9016.32	1.05	219	8.39137	SQK-NBD114-24_barcode13
```

#### Conversión de bam a fastq

```bash
conda activate quality

for file in *.bam; do prefix="${file%.bam}"; samtools sort -n "$file" -o "${prefix}_sorted.bam"; done

for file in *_sorted.bam; do prefix="${file%.bam}"; bedtools bamtofastq -i "${prefix}.bam" -fq "${prefix}.fastq"; done

seqkit stats -a -j 4 *_sorted.fastq > stats_sorted_fastq.txt
```

> **Comentario:** 
> - `samtools sort -n`: Ordena los archivos BAM por nombre de lectura.
> - `bedtools bamtofastq`: Convierte los archivos BAM ordenados a formato FASTQ.
> - `seqkit stats`: Calcula las estadísticas de archivos FASTQ que han sido previamente ordenados.

```bash
cat barcoding_summary.txt | head

file                                                                           format  type  num_seqs    sum_len  min_len  avg_len  max_len     Q1     Q2     Q3  sum_gap    N50  N50_num  Q20(%)  Q30(%)  AvgQual  GC(%)  sum_n
bcf4b7732185c1a3353d1b4fe80266cd3ac60162_SQK-NBD114-24_barcode13_sorted.fastq  FASTQ   DNA         10      6,008      219    600.8    1,267    219    621    678        0    678        2   45.21   17.71    11.17  35.92      0
bcf4b7732185c1a3353d1b4fe80266cd3ac60162_SQK-NBD114-24_barcode14_sorted.fastq  FASTQ   DNA      5,854  6,073,564       16  1,037.5   20,665    445    700  1,179        0  1,405      481   47.28    18.5    11.38  45.46      0
bcf4b7732185c1a3353d1b4fe80266cd3ac60162_SQK-NBD114-24_barcode15_sorted.fastq  FASTQ   DNA          2      2,900    1,450    1,450    1,450  1,450  1,450  1,450        0  1,450        1   51.93   23.24    12.08     52      0
bcf4b7732185c1a3353d1b4fe80266cd3ac60162_unclassified_sorted.fastq             FASTQ   DNA      2,156  2,567,210       28  1,190.7   26,377    585    859  1,351        0  1,439      223   47.34    18.8    11.34  45.45      0
```

## 5. Análisis de calidad del secuenciamiento Nanopore 

### Concatenado de los archivos FASTQ

```bash
cd ~/genomics/raw_data

mkdir nanopore

cd nanopore

cat /home/ins_user/genomics/basecalling/fast5/pass/*.fastq > b01_fast.fastq
```

### Visualización de la calidad

```bash
cd ~/genomics/quality

mkdir nanopore

cd nanopore

NanoPlot -t 2 --fastq /home/ins_user/genomics/raw_data/nanopore/b01_fast.fastq -p b01_fast_raw_ -o b01_fast_raw --maxlength 100000
```

> **Comentario:** 
> - `--fastq /home/ins_user/genomics/raw_data/nanopore/b01_fast.fastq`: Indica la ruta del archivo FASTQ que contiene las lecturas de secuenciación de ONT que se van a analizar.
> - `-p b01_fast_raw_`: Define el prefijo que se usará para los nombres de los archivos de salida. En este caso, todos los gráficos generados comenzarán con "b01_fast_raw_".
> - `-o b01_fast_raw`: Especifica el directorio de salida donde se guardarán los gráficos. Si el directorio no existe, NanoPlot lo creará.
> - `--maxlength 100000`: Establece la longitud máxima que se mostrará en los gráficos. Las lecturas que superen esta longitud serán truncadas en las visualizaciones. Esto ayuda a enfocar el análisis en la mayoría de las lecturas y evita que las lecturas extremadamente largas distorsionen la visualización.

### Eliminación de adaptadores

```bash
cd ~/genomics/trimming/

mkdir nanopore

cd nanopore

mkdir porechop

cd porechop

porechop -t 2 -i /home/ins_user/genomics/raw_data/nanopore/b01_fast.fastq -o b01_fast_porechop.fastq.gz
```

> **Comentario:** 
> - `-i /home/ins_user/genomics/raw_data/nanopore/b01_fast.fastq`: Esta opción indica la ruta del archivo FASTQ de entrada. Este es el archivo que contiene las lecturas de secuenciación de ONT que se van a procesar.
> - `-o b01_fast_porechop.fastq.gz`: Esta opción especifica el nombre del archivo FASTQ de salida comprimido con gzip. Este archivo contendrá las lecturas después de que Porechop haya recortado los adaptadores y separado las lecturas concatenadas.

### Eliminación de lecturas de baja calidad

```bash
cd ~/genomics/trimming/nanopore

mkdir nanofilt

cd nanofilt

gunzip -c /home/ins_user/genomics/trimming/nanopore/porechop/b01_fast_porechop.fastq.gz | NanoFilt -q 9 --length 1000 | gzip > b01_fast_nanofilt.fastq.gz
```

> **Comentario:** 
> - `gunzip -c /home/ins_user/genomics/trimming/nanopore/porechop/b01_fast_porechop.fastq.gz`: Descomprime el archivo "b01_fast_porechop.fastq.gz".
> - `NanoFilt -q 9 --length 1000`: Filtra las lecturas descomprimidas utilizando NanoFilt, manteniendo solo aquellas que tengan un puntaje de calidad mínimo de 9 y una longitud mínima de 1000 bases.
> - `gzip > b01_fast_nanofilt.fastq.gz`: Comprime las lecturas filtradas y las guarda en un nuevo archivo llamado "b01_fast_nanofilt.fastq.gz".
> - `|`: Este símbolo es una "tubería" (pipe) que conecta la salida de un comando a la entrada de otro. 

```bash
cd ~/genomics/quality/nanopore

NanoPlot -t 2 --fastq /home/ins_user/genomics/trimming/nanopore/nanofilt/b01_fast_nanofilt.fastq.gz -p b00_fast_filt_ -o b01_fast_filt --maxlength 100000
```
