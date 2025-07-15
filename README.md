# Identificación y análisis comparativo de genes ortólogos en pinzones de Darwin: un enfoque evolutivo
## Nombre del Autor: Gabriel Achig
## Proposito del programa:
El objetivo principal es encontrar y examinar los ortólogos en varias pinzonas de Darwin para comprender los procesos evolutivos que han llevado a sus cambios de forma y función Al emplear métodos de análisis de datos biológicos, tiene como objetivo examinar las secuencias de codificación de proteínas, alinalos y construir árboles evolutivos que revelen patrones de conservación y variación genética, ofreciendo pruebas de selección natural y adaptación ecológica en este avance notable

## Cómo usar el programa

* Preparar el ambiente de trabajo:
- Utilizar las herramientas necesarias, como MUSCLE, IQTREE, ATOM. Luego, descarga las secuencias codificantes de proteínas de las especies de pinzones de Darwin desde bases de datos públicas como NCBI o Ensembl.

* Identificación de genes ortólogos:

- Con grep "", identificar los genes ortologos que se puede descargar para poder realizar un buen alineamiento.

* Alineamiento de genes:
- Emplea MUSCLE para realizar alineamientos múltiples de las proteínas ortólogas identificadas. Este paso es fundamental para comparar las secuencias y detectar regiones conservadas.

4. Edición manual:
- Abre los archivos de alineamiento en Atom para verificar y corregir posibles errores en los nombres de las secuencias o en el alineamiento, asegurando la calidad de los datos.

5. Construcción de árboles filogenéticos:
- Utiliza IQ-TREE para inferir árboles filogenéticos a partir de los alineamientos de proteínas. Esto permitirá observar las relaciones evolutivas entre las especies.

6. Visualización y anotación:
- Abre los árboles filogenéticos en FigTree para visualizar, editar y anotar los resultados, facilitando la interpretación de los patrones evolutivos.

7. Interpretación:
- Analiza los patrones de conservación y divergencia genética observados en los árboles filogenéticos para inferir procesos evolutivos y adaptaciones específicas en los pinzones de Darwin.

## ¿En qué organismo o grupo de organismos vas a trabajar?
- Grupo taxonómico: **Pinzones de Darwin**
- Familia: **Thraupidae**
- Especies representativas:
  - *Geospiza fortis* (pinzón de tierra mediano)
  - *Geospiza scandens* (pinzón de cactus común)
  - *Camarhynchus parvulus* (pinzón carpintero pequeño)

---

## ¿Qué programas vas a usar en tu proyecto?

- **BLASTp:** para buscar e identificar genes ortólogos entre especies.
- **MUSCLE:** para realizar alineamientos múltiples de proteínas.
- **IQ-TREE:** para inferir árboles filogenéticos de proteínas ortólogas.
- **Atom:** para edición manual de alineamientos y nombres de secuencia.
- **FigTree:** para visualizar y anotar árboles filogenéticos.

## Especies de Pinzones de Darwin

* *Geospiza fortis* (Pinzón de tierra mediano)  
![Geospiza fortis](https://datazone.darwinfoundation.org/images/checklist/Medium_ground_finch.jpg))

---

* *Geospiza scandens* (Pinzón de cactus común)  
![Geospiza scandens](https://live.staticflickr.com/5569/14526971708_a05780c112_b.jpg)

---

* *Camarhynchus parvulus* (Pinzón carpintero pequeño)  
![Camarhynchus parvulus](https://multimedia20stg.blob.core.windows.net/especies/01_Camarhynchus%20parvulus.jpg)

---

* *Platyspiza crassirostris* (Pinzón vegetariano)  
![Platyspiza crassirostris](https://datazone.darwinfoundation.org/images/checklist/_mg_9066.jpg)

## Genes que se van a utilizar para el analisis comparativo 
- ALDH2
- ALX1
- HMGA2

## Lista de comandos

* Crear carpeta
```
mkdir Proyecto_pinzones
```
* Navegar al directorio de datos
```
cd Proyecto_pinzones
```
* Verificar las secuencias ortólogas
```
grep "gen de interes" Orthologs.IDS.txt
```
* Descargar secuencias de proteínas de NCBI
```
./datasets download gene symbol ALDH2 --ortholog Thraupidae  --filename ALDH2_Thraupidae.zip
./datasets download gene symbol ALX1 --ortholog Thraupidae  --filename ALX1_Thraupidae.zip
./datasets download gene symbol HMGA2 --ortholog Thraupidae  --filename HMGA2_Thraupidae.zip
``` 

* Descomprimir archivos
```
unzip *.zip 
o descomprimir uno por uno
```
* **Cambiar el nombre de todos los genes descomprimidos**

* Combinar todas las secuencias en un solo archivo para BLAST
```
cat *.faa > todas_proteinas.faa
```
* Crear base de datos BLAST
```
module av blast
module load blast+/2.11.0
makeblastdb -in todas_proteinas.faa -dbtype prot -out pinzones_db
```
* Ejecutar BLASTp
```
blastp -query todas_proteinas.faa -db nr -out results.barcode02.out -remote
```
* Ejecutar MUSCLE para alineamiento múltiple
```
./muscle3.8.31_i86linux64 -in todas_proteinas.faa -out muscle_todas_proteinas.faa -maxiters 1 -diags
```
* Abrir en editor de texto (Atom), comandos especificos de atom:
```
**Find**
^>[^ ]+ (\w+) \[organism=([^\]]+)\].*
**Replace**
>$1 [organism=$2]
```
* Ejecutar IQ-TREE para inferencia filogenética
```
module av iqtree
module load iqtree
iqtree -s muscle_todas_proteinasaATOM.faa
```
* Explicación de parámetros:
``
-s: archivo de alineamiento
-m MFP: selección automática del mejor modelo
-bb 1000: bootstrap con 1000 réplicas
-nt AUTO: uso automático de núcleos de CPU
``
* Abrir el árbol resultante en FigTree
* Realizar el mismo procedimiento con las secuencias de RNA y comparar los arboles filogeneticos

# Comparativa de Arboles filogenéticos
* Árbol de Proteínas
![Proteina](https://github.com/GabrielUwU07/Pinzones_filogen-a-/blob/main/ArbolProteinas.jpg)
* Árbol de rna
![RNA](https://github.com/GabrielUwU07/Pinzones_filogen-a-/blob/main/Arbolrna.jpg.png)

# Carpetas adicionales
![Programs](https://github.com/GabrielUwU07/Programs.git)
![SCRIPS](https://github.com/GabrielUwU07/SCRIPS.git)
