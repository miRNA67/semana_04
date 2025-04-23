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

guppy_basecaller -i /data/2025_1/database/nanopore/fast5 -s fast5_db_sup -c dna_r10.4_e8.1_sup.cfg -x 'cuda:0'
```

> **Comentario:** 
> - `-i /data/2025_1/database/nanopore/fast5`: Esta opción especifica el directorio de entrada donde se encuentran los archivos de datos de secuenciación crudos (en formato FAST5). Guppy leerá todos los archivos FAST5 dentro de este directorio.
> - `-s fast5_db_sup`: Esto define el directorio de salida donde se guardarán los datos después del basecalling. En este caso, se creará un directorio llamado fast5_db_sup en tu directorio de trabajo actual para almacenar los archivos de salida (típicamente archivos FASTQ).
> - `-c dna_r10.4_e8.1_fast.cfg`: Esta opción especifica el archivo de configuración que se utilizará para el "basecalling". El archivo dna_r10.4_e8.1_sup.cfg contiene ajustes optimizados para la celda de flujo R10.4 y el modelo de "basecalling" "sup" . Este modelo es conocido por su mayor exactitud en la identificación de las bases.
> - `-x 'cuda:0'`: Esta opción habilita la aceleración por GPU para el proceso de basecalling, lo que puede acelerar significativamente la computación. 'cuda:0' especifica que deseas utilizar la primera GPU habilitada para CUDA (índice 0) disponible en tu sistema.

```bash
ls

fail  guppy_basecaller_log-2025-04-22_21-21-01.log  pass  sequencing_summary.txt  sequencing_telemetry.js
```

```bash
head -n 5 pass/fastq_runid_bcf4b7732185c1a3353d1b4fe80266cd3ac60162_0_0.fastq

@a2662a87-b1ee-4491-a847-763bcf84bb77 runid=bcf4b7732185c1a3353d1b4fe80266cd3ac60162 sampleid=no_sample read=7221 ch=100 start_time=2024-04-28T00:01:51Z model_version_id=2021-11-17_dna_r10.4_minion_promethion_1024_67af0493
TTATGTTCATTCTACTTGGTTCAGTTACGTATTGCTAAGGTTAAAACAAGTCTGTTGGGACCCATAGACAGCACCTGTTTGGTTCACTACGCTATCGAGACAATCTCTAATTGTGTTTTGATCATTATAAACCGGAATAGCTACAGTAAATATCATCTTTTTTCTCCTTAATTATTGTTTCCTATATAAAAACAAGTCCAGAATTATTCGAATCCAATTTTAAAAGTTACCATAATTTCTTTCTTTATAAATATGGGTTAAAAATTTTAATGTGTTTTTAAACCTAGCCACCGTAATCTAGATAATAAGATGGAATATTCCAGTAATTAAATTGGATTTTCCATAAGATCCCTAACAAATGCTTTGATTCATTTCTCTTTGAATTTGGAAAGCTCGCTTCATTTAATCCTAATTACGATACTTTGCGGATTTTTAATTTACCCATAAAAAAACACCTCTAAGTCGTTTTCAGGTATGATACCTGCTTTTCAACTTAAAGGTGCTTCTCCTCACTACAGGCCCAGACTCTCAAAAACTTCAACTTTTTATAACTTACTCTTTTCCGGCAGCGGCTTCCGCCTGTCCGTCTTTTAATTGATCATTGATTCTGGCGTCTTTCAAATACTCAGTCTTGAATCCGCTCTTCAGCGCCCACGCATAGAAGGCAAGGGCAACGATTGCGATCAGCCCCATATCCCAGCCGTACGGAATGATGTTCAGACCGCCGAATTTTCACTTTCCGAGCCATGAAATGACCATCATGCTGAGCAGATAGACAACCATCCAGACGCCGCCTTTAAAGTTTCTGCGGAATCCTTTCCACTTCGCTTTCGCTTGGTAGTAGAAATAAATCGGCAGGCCGATCAAAATGATAAACAGCACCTGCCCTGTTAACGGCCAGCGCGCCCAATACAGCACGAGAGACGCGAATACGAAGCCGAGCGGTGCAACCACGCTGAGGCCTTTCAGACGGAGAGGCCGGTACAAATCCGCCGCCGTCCGCCGCAGCGTCATCACCGTCACGGGTACCAGTAATAAGAAATCAGCGTCGCAACGGAAATGACTTCAGCAAGCACGCCCCATCCTCTGAATAAAAACAGAAAGATAAACGATACGATCAGGTTGAAAATCATCGCTTGGCGCGGCACGCCGTACAGCGGATGAAGCTTTCCGAAAATGCTCGGCATATATTTATTTTTTTCCATGCCGTAAATCATGCGTGACGTCGTAGCGGTATAAGTGATACCCGTTCCTGACGGAGAAACGAACGCGTCCGCATAAAGAATAATGACAAGCCAGTTGATATTCAATGCGATCGCCAAATCGGCAAATGGAGAGTTGAAGTTCAGGTGACTCCAGCCGTGAACGATCATGGAAGGTTCAACCGCACCGATAAATGCGATTTGCAATAGGACGTAAATGACGGTTGCGACCAGCAGCGAACCGACAACCGCAATCGGAATCGATTTGCCGGGATTTTTTGCTTCTCCGGCCATGTTAATGGTTTGAAACCCGTTAAACGCAAATACGATACCCCGATGTAGCCACCACCGT
+
#$$%%&&&&''()*-.2(((()0/..*)%%%&&')*++++,-66:;;-,,,/2))(&'()-//./88889ACDDCEFFHHFHHFHEDCBC00000D@@ABCKL{MJMJJKR{NLMONKJJN{NIK{JK;;:98:::EIIOMHGKJMO{PMLQ{SKJLMKDJFQIEBCBHK{KLKKQJKKJOM{LHMKFIIHQTJJK{LJGEIIJJMJGB>@@@BIIEDDHB>><11--((.344@AAC===<0573*=HNJHGNGHGGJFEFDE>8>=?EFGJIGJJJJHFJGCBACBGGGGGHKI{DEC43333475333467::=?A)**))*3<LLJOMOMHHKILNDTEDHHNQQNGEB?@?AHJH{>>>>>FNEBAAAD@PJFMJ@FIHHKMMRLPPGHE0////>===HHMHFGHJOMLHGGEFGHIMIR{LGDEIMK@@>?E>=?3/1777BFGLJDB@87A==?JKEEDEGCBAABIGLGKGKMJN{NKMNPHCBCCCII{MI60..,/0016))***.....===?AA?@==>>?VJ{ROFIHPJLLHHGGL=DIFFFGFIMEBDAC@9<<;::::9;;?CEEGDD;;@99:?:DDBECE;9983111*+(&&%%%%%)%&+9:HEGEC>>?@IKFKJ{MMKKJIKGBB?=6/,,E>>>?>ILMSJLHEGBEDCHH?===>F22222224?BABIJB?>9CGGLJIGOGGHG<<<<<C..333<,,,*),,.4:81226622BAA@BHHDEGIFDHBBDDHFEEGHGGFHMMGIFGGF?=>=@IGGFHJKA?<;;<==@BEFECD@?@@@BDBCCFGDDGDB>>>BBDFFD:66<=BAA@==>>=>>?EBBBCCIFGEEDEDEBBACCBACDEFFIIHFCBAAAC65556ACCABCFJFHGFEFFDDEC@A@ACBC@@>9:1/ECGGFDCDD?<;;;?@<2***),--.8889?A=>=>;:::988/()00.0/0>@ABB76666?JCIGGFFDFFFEEECCCBICDDCBCDFDHH@>>=<@ABEFAB454-+*)(+-/224==>CBBCCDED=<<<>>>A?=;*****:CA<<<::;?@AB@DFBBAAAFFFIFEDKFC@BACDFF:7854444:DCDFMCEGGCEFDIJAMRIKEEFABBHHJHNJIHHFFGDEGFFFIJ{OIMILGKF:;78;;?BD@@22222<FGECDD@=>>>>HLHA77ABBAA>>@AB@?:9::;HEBB?>>::<:;;3*('''')))/23--?=<=<@B?AAA>76533667E>>>>>CDCFFFHILGEEDCDDDFHGILHJIEEFGEH;9:::>988888861/,+,--+1113ECCDBAAAADFIHIHIH=;;;<A?:::HGE????=@@@BFJFLFJIGD:999:AA@@ADDGGFHIFA@@@@FFFEEDEDDCCCCCCEDFIFDABB>8888=@CBEFF+***+DGF@@@?@D?@@@BHFFGECDBAHILG;;;:;>>?ACB87777B?<<<=>BC6;.++&&&&&&%&*)1;:9<<ACC....---;0/0..//6+<<<BBBCB?>>*))))
@b54d96bc-40da-4cad-91d1-1f53b75ae40b runid=bcf4b7732185c1a3353d1b4fe80266cd3ac60162 sampleid=no_sample read=10540 ch=101 start_time=2024-04-27T23:58:25Z model_version_id=2021-11-17_dna_r10.4_minion_promethion_1024_67af0493
TTCTTTTTATGTATTCTACTCGTTCAGTTACGTATTGCTAAGGTTAAAACGAGTCTCTGGGACCCATAGACAGCACCTCTCTAAAGGGGGATATAGCCATGGGCAGAACAAAACTGGGAAACAGAAATGCTCAGAACGACAATGCCAAAAAGAAAAACGGCTTCGGACAGAAATTTGATTCTTATGCGGCCGTGAAGCTGAAAAGCTGATAGCAAGCAATAAAAGACACGGTGAGTAACGTGACGGCAGCATCTTCCAAATGGGGGGATGCTGTTTTTACCGCCTTCTTTGGTAAAATAGGAACATTGAATAAAAAGGAGTTTCGATATATCAATAATAAATTACTGCTCGTTGACGGCATGGCGCTTTTGTTCCACTAGTTTTTCGCGACGGCCGTTCATCGCAATTTTATGATAAATGAAAACGGAATTCCCACAAACGGCGTCAACGGTTTTTTAAAGCATCTTATTACGGCGGTTGATACGTTTTCAGCCCACACATGTCGTCTGCTGCTGGGATATGGGAAGCAAAACGTACCGCAATGATTTGTTTCAAGATTATAAGGCCAACAAAG
+
$$$%&&%&'&&'%$$$$&()('(*+.---++,,,99:;<IKNRLLMJLOB@>>>?@@8))*68:<-;77777667;;FBB??ABCE@DA?;::://////7777?EFFDDDIOJIFHGKLSTCEFGGGG550//044...+-,+-.*'''1;ACCERLBA@@@>;8668CDEHJCEDCCGCAB@@;6))+8;>>??DCCBBHHIIGFEDDBCCAAACDHIECCIP[HCCCBABCCDKHDCCFDGBCCCBEDD?>:557<956>BCFKNDDCC@9,+655>BFHKKMGDGEAHFHIILHFCDEDFFIKAAAA99840=:I@?@?:<<<<A@B,,,,,BA:<:8A=;;9320002<CB;667;?ACDD@<721225400133312?>=??;;;:;::933***((01DGHJQONGJMLLIIJKRQJFHEFGJGEFGEGCDDC@AA@ADBBCCBDFIJ{{KJKHGHH;;;;;MHEEFEEIIIMPHCE==<;8/;988;<E@96GFHJHGFGFFFCDCDCC?@BDC@3/.21100DB87777778HHRVKIJIGEDDFFGGJICEGFEDDE-,,++.+
@d10de390-43fc-48d6-83f9-c865ddf92885 runid=bcf4b7732185c1a3353d1b4fe80266cd3ac60162 sampleid=no_sample read=12796 ch=392 start_time=2024-04-27T23:59:17Z model_version_id=2021-11-17_dna_r10.4_minion_promethion_1024_67af0493
TTATGTAACCTACTTCGTTCAGTTACGTATTGCTAAGGTTAAAACGAGTCTCTTGGGACCCATAGACAGCACCTTGTCAGAAAAAGTCATCAGTGTGATAAAGAGACGTTCTCAAGCCGCATGACTGATGTGAAAAGCTCGATTGCAAAGTCCATGCTGAATATGGACCCGCCGAAACATACCCAAATCAGATCTGCCGTCAATCGCGCTTTCACTCCCCGCGTCTTGAAGAAATGGGAGCCGAGAATTAAAGACATTACCGATCATCTTCTGGAACGAGCAAGGACAAAGAGCAAGTGATATGGTCCGAAGTACTTCTCCCTTTGCCGGTGGTGGTGATTTCAGAATTATTAGGCGTTCCGTCCGAACGTATGGATCAGTTTAAAAAATGGTCGGATATTCTCGTCAGCATGCCGAAAGATGCGAGTCCTGAAGCGGCGGAGAAAAATCAGCAGGAACGTGACCAATGT
```

### Basecalling de POD5

#### Basecalling

```bash
cd ~/genomics/basecalling

mkdir pod5_db_sup

cd pod5_db_sup

dorado basecaller sup --kit-name SQK-NBD114-24 --min-qscore 10 --device 'cuda:0' --barcode-both-ends --models-directory 
/data/software/dorado-0.9.1-linux-x64/models /data/2025_1/database/nanopore/pod5/barcode15.pod5 > b15_calls.bam
```

#### Conversión de bam a fastq

```bash
for file in *.bam; do prefix="${file%.bam}"; samtools sort -n "$file" -o "${prefix}_sorted.bam"; done

for file in *_sorted.bam; do prefix="${file%.bam}"; bedtools bamtofastq -i "${prefix}.bam" -fq "${prefix}.fastq"; done

seqkit stats -a -j 4 *_sorted.fastq > stats_sorted_fastq.txt
```

> **Comentario:** 
> - `samtools sort -n`: Ordena los archivos BAM por nombre de lectura.
> - `bedtools bamtofastq`: Convierte los archivos BAM ordenados a formato FASTQ.
> - `seqkit stats`: Calcula las estadísticas de archivos FASTQ que han sido previamente ordenados.

```bash
cat stats_sorted_fastq.txt | head

file                    format  type  num_seqs    sum_len  min_len  avg_len  max_len   Q1   Q2       Q3  sum_gap    N50  N50_num  Q20(%)  Q30(%)  AvgQual  GC(%)  sum_n
b15_calls_sorted.fastq  FASTQ   DNA      8,056  9,351,266       26  1,160.8   26,983  555  814  1,298.5        0  1,423      721   89.24   80.11    19.24   45.7      0
```

```bash
mv b15_calls_sorted.fastq b15.fastq

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

gzip b15.fastq.gz
```

## 5. Análisis de calidad del secuenciamiento Nanopore 

### Visualización de la calidad

```bash
cd ~/genomics/quality

mkdir nanopore

cd nanopore

NanoPlot -t 2 --fastq ~/genomics/basecalling/pod5_db_sup/b15.fastq.gz -p b15_sup_db_ -o b15_sup_db --maxlength 1000000
```

> **Comentario:** 
> - `--fastq /home/ins_user/genomics/raw_data/nanopore/b01_fast.fastq`: Indica la ruta del archivo FASTQ que contiene las lecturas de secuenciación de ONT que se van a analizar.
> - `-p b15_sup_db_`: Define el prefijo que se usará para los nombres de los archivos de salida. En este caso, todos los gráficos generados comenzarán con "b15_sup_db_".
> - `-o b15_sup_db`: Especifica el directorio de salida donde se guardarán los gráficos. Si el directorio no existe, NanoPlot lo creará.
> - `--maxlength 1000000`: Establece la longitud máxima que se mostrará en los gráficos. Las lecturas que superen esta longitud serán truncadas en las visualizaciones. Esto ayuda a enfocar el análisis en la mayoría de las lecturas y evita que las lecturas extremadamente largas distorsionen la visualización.

### Eliminación de adaptadores

```bash
cd ~/genomics/trimming/

mkdir nanopore

cd nanopore

porechop -t 2 -i ~/genomics/basecalling/pod5_db_sup/b15.fastq.gz -o b15_sup_porechop.fastq.gz
```

> **Comentario:** 
> - `-i ~/genomics/basecalling/pod5_db_sup/b15.fastq.gz`: Esta opción indica la ruta del archivo FASTQ de entrada. Este es el archivo que contiene las lecturas de secuenciación de ONT que se van a procesar.
> - `-o b15_sup_porechop.fastq.gz`: Esta opción especifica el nombre del archivo FASTQ de salida comprimido con gzip. Este archivo contendrá las lecturas después de que Porechop haya recortado los adaptadores y separado las lecturas concatenadas.

### Eliminación de lecturas considerando su calidad y longitud

```bash
gunzip -c ~/genomics/trimming/nanopore/b15_sup_porechop.fastq.gz | NanoFilt -q 10 --length 1000 | gzip > b15_sup_nanofilt.fastq.gz
```

> **Comentario:** 
> - `gunzip -c ~/genomics/trimming/nanopore/b15_sup_porechop.fastq.gz`: Descomprime el archivo "b15_sup_porechop.fastq.gz".
> - `NanoFilt -q 10 --length 1000`: Filtra las lecturas descomprimidas utilizando NanoFilt, manteniendo solo aquellas que tengan un puntaje de calidad mínimo de 10 y una longitud mínima de 1000 bases.
> - `gzip > b15_sup_nanofilt.fastq.gz`: Comprime las lecturas filtradas y las guarda en un nuevo archivo llamado "b15_sup_nanofilt.fastq.gz".
> - `|`: Este símbolo es una "tubería" (pipe) que conecta la salida de un comando a la entrada de otro. 

```bash
cd ~/genomics/quality/nanopore

NanoPlot -t 2 --fastq ~/genomics/trimming/nanopore/b15_sup_nanofilt.fastq.gz -p b15_sup_filt_ -o b15_sup_filt --maxlength 100000
```
