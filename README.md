# Identificación y análisis comparativo de genes ortólogos en pinzones de Darwin: un enfoque evolutivo
## Nombre del Autor: Gabriel Achig
## Proposito del programa:
El objetivo principal es encontrar y examinar los ortólogos en varias pinzonas de Darwin para comprender los procesos evolutivos que han llevado a sus cambios de forma y función Al emplear métodos de análisis de datos biológicos, tiene como objetivo examinar las secuencias de codificación de proteínas, alinalos y construir árboles evolutivos que revelen patrones de conservación y variación genética, ofreciendo pruebas de selección natural y adaptación ecológica en este avance notable

## Cómo usar el programa

1. Preparar el ambiente de trabajo:
Instala Conda y crea un ambiente específico para el proyecto con las herramientas necesarias, como BLASTp, MUSCLE e IQ-TREE. Luego, descarga las secuencias codificantes de proteínas de las especies de pinzones de Darwin desde bases de datos públicas como NCBI o Ensembl.

2. Identificación de genes ortólogos:
Utiliza BLASTp para comparar las secuencias de proteínas entre las especies y encontrar genes ortólogos. Esto te permitirá detectar similitudes significativas en las proteínas codificadas.

3. Alineamiento de proteínas:
Emplea MUSCLE para realizar alineamientos múltiples de las proteínas ortólogas identificadas. Este paso es fundamental para comparar las secuencias y detectar regiones conservadas.

4. Edición manual:
Abre los archivos de alineamiento en Atom para verificar y corregir posibles errores en los nombres de las secuencias o en el alineamiento, asegurando la calidad de los datos.

5. Construcción de árboles filogenéticos:
Utiliza IQ-TREE para inferir árboles filogenéticos a partir de los alineamientos de proteínas. Esto permitirá observar las relaciones evolutivas entre las especies.

6. Visualización y anotación:
Abre los árboles filogenéticos en FigTree para visualizar, editar y anotar los resultados, facilitando la interpretación de los patrones evolutivos.

7. Interpretación:
Analiza los patrones de conservación y divergencia genética observados en los árboles filogenéticos para inferir procesos evolutivos y adaptaciones específicas en los pinzones de Darwin.

## Q1. ¿En qué organismo o grupo de organismos vas a trabajar?
- Grupo taxonómico: **Pinzones de Darwin**
- Familia: **Thraupidae**
- Especies representativas:
  - *Geospiza fortis* (pinzón de tierra mediano)
  - *Geospiza scandens* (pinzón de cactus común)
  - *Camarhynchus parvulus* (pinzón carpintero pequeño)

---

## Q2. Brevemente describe qué piensas hacer en tu proyecto

- Identificar **genes ortólogos** entre distintas especies de pinzones de Darwin.
- Utilizar secuencias codificantes de proteínas disponibles en bases de datos públicas (NCBI/Ensembl).
- Comparar genes relacionados con adaptaciones morfológicas y funcionales (como forma del pico o señalización).
- Alinear proteínas ortólogas usando **MUSCLE**.
- Construir **árboles filogenéticos** con IQ-TREE para observar patrones evolutivos.
- Analizar la conservación o divergencia de estos genes como evidencia de selección o especialización ecológica.

---

## Q3. ¿Qué programas vas a usar en tu proyecto?

- **Conda:** para gestionar e instalar ambientes bioinformáticos.
- **BLASTp:** para buscar e identificar genes ortólogos entre especies.
- **MUSCLE:** para realizar alineamientos múltiples de proteínas.
- **IQ-TREE:** para inferir árboles filogenéticos de proteínas ortólogas.
- **Atom:** para edición manual de alineamientos y nombres de secuencia.
- **FigTree:** para visualizar y anotar árboles filogenéticos.
- **Linux:** como sistema operativo para ejecutar todo el flujo de trabajo desde línea de comandos.

## 📸 Especies de Pinzones de Darwin

### 1. *Geospiza fortis* (Pinzón de tierra mediano)  
![Geospiza fortis](https://datazone.darwinfoundation.org/images/checklist/Medium_ground_finch.jpg))

---

### 2. *Geospiza scandens* (Pinzón de cactus común)  
![Geospiza scandens](https://live.staticflickr.com/5569/14526971708_a05780c112_b.jpg)

---

### 3. *Camarhynchus parvulus* (Pinzón carpintero pequeño)  
![Camarhynchus parvulus](https://multimedia20stg.blob.core.windows.net/especies/01_Camarhynchus%20parvulus.jpg)

---

### 4. *Platyspiza crassirostris* (Pinzón vegetariano)  
![Platyspiza crassirostris](https://datazone.darwinfoundation.org/images/checklist/_mg_9066.jpg)

### Programa del proyecto
# Actualizar paquetes existentes
sudo apt-get update

# Instalar Miniconda (versión ligera de Anaconda)
wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh
bash Miniconda3-latest-Linux-x86_64.sh
source ~/.bashrc

# Crear y activar ambiente conda para el proyecto
conda create -n pinzones_ortologos python=3.8 blast muscle iqtree -c bioconda
conda activate pinzones_ortologos

# Instalar programas adicionales
conda install -c bioconda figtree
# Crear estructura de directorios
mkdir -p proyecto_pinzones/{datos,blast,alineamientos,arboles}

# Navegar al directorio de datos
cd proyecto_pinzones/datos

# Descargar secuencias de proteínas de NCBI (ejemplo con Geospiza fortis)
# Nota: Reemplaza las URLs con las reales de NCBI o Ensembl
wget https://ftp.ncbi.nlm.nih.gov/genomes/Geospiza_fortis/protein.faa.gz -O Geospiza_fortis.faa.gz
wget https://ftp.ncbi.nlm.nih.gov/genomes/Geospiza_scandens/protein.faa.gz -O Geospiza_scandens.faa.gz
wget https://ftp.ncbi.nlm.nih.gov/genomes/Camarhynchus_parvulus/protein.faa.gz -O Camarhynchus_parvulus.faa.gz

# Descomprimir archivos
gunzip *.faa.gz

# Combinar todas las secuencias en un solo archivo para BLAST
cat *.faa > todas_proteinas.faa

# Crear base de datos BLAST
makeblastdb -in todas_proteinas.faa -dbtype prot -out pinzones_db

# Ejecutar búsqueda BLASTp (ejemplo con una proteína de interés)
# Primero extraemos una proteína como query (ejemplo)
head -n 20 Geospiza_fortis.faa > proteina_query.faa

# Ejecutar BLASTp
blastp -query proteina_query.faa -db pinzones_db -out blast_resultados.txt -outfmt 6 -evalue 1e-5
# Extraer secuencias de interés basadas en resultados BLAST (ejemplo)

# Esto requeriría un script personalizado, pero aquí un ejemplo básico
grep -A 1 "patron_de_interes" todas_proteinas.faa > secuencias_ortologas.faa

# Ejecutar MUSCLE para alineamiento múltiple
muscle -in secuencias_ortologas.faa -out alineamiento_ortologos.afa -clw

# Opcional: convertir formato para mejor visualización
muscle -in alineamiento_ortologos.afa -out alineamiento_ortologos.fasta -fasta

# Abrir en editor de texto (Atom) - desde Git Bash puedes usar:
start alineamiento_ortologos.fasta

# Ejecutar IQ-TREE para inferencia filogenética
iqtree -s alineamiento_ortologos.afa -m MFP -bb 1000 -nt AUTO

# Explicación de parámetros:
# -s: archivo de alineamiento
# -m MFP: selección automática del mejor modelo
# -bb 1000: bootstrap con 1000 réplicas
# -nt AUTO: uso automático de núcleos de CPU
# Abrir el árbol resultante en FigTree
start alineamiento_ortologos.afa.treefile

# Opcional: Filtrar alineamientos por conservación
trimal -in alineamiento_ortologos.afa -out alineamiento_filtrado.afa -gt 0.8

# Opcional: Reconstruir árbol con alineamiento filtrado
iqtree -s alineamiento_filtrado.afa -m MFP -bb 1000 -nt AUTO

# Mover archivos a sus respectivos directorios
mv blast_resultados.txt ../blast/
mv alineamiento_* ../alineamientos/
mv *.treefile ../arboles/

# Crear archivo README con metadatos del análisis
echo "Análisis de genes ortólogos en pinzones de Darwin" > README.txt
echo "Fecha: $(date)" >> README.txt
echo "Parámetros BLAST: evalue 1e-5" >> README.txt
echo "Modelo seleccionado por IQ-TREE: $(grep 'Best-fit model' alineamientos/alineamiento_ortologos.afa.log)" >> README.txt

# Crear archivo comprimido con los resultados importantes
tar -czvf resultados_pinzones.tar.gz blast/ alineamientos/ arboles/ README.txt
# Pinzones_filogen-a-
