# genome-characterization
A small workflow to get general information (taxonomy, quality, etc) out of genomes or MAGs.

## Summary
* [1. Tool description](#tool)
* [2. Installation](#installation)
* [3. How to run](#run)
* [References](#references)
* [Author - contact](#author---contact)


## 1. <a name="tool"></a>Tool description
All the tools in use are from third-parties. To get more information about them, 
please check the links and references.

### 1.1 Third-parties databases and scripts:
CheckM: https://github.com/Ecogenomics/CheckM/wiki
Installation: https://github.com/Ecogenomics/CheckM/wiki/Installation \

gtdb_tk: https://github.com/Ecogenomics/GTDBTk \
Installation: https://ecogenomics.github.io/GTDBTk/running/

BBtools documentation: https://jgi.doe.gov/data-and-tools/bbtools/ \
Download: https://sourceforge.net/projects/bbmap/ 



## 2. <a name="installation"></a>Installation
### Download FAW repository:
Option 1: If you have git - clone the repository:
```
git clone git@github.com:sandragodinhosilva/FAW.git
```
Option 2: Download the current version of the code:
```
wget https://github.com/sandragodinhosilva/FAW.git
```
### Create conda environment & install dependencies
```
conda create -n genome-characterization
conda activate genome-characterization
conda install -c conda-forge -c bioconda -c defaults prokka
conda install diamond
conda install pandas 
```
### Download databases 
I:


## 3. <a name="run"></a>How to run

### Necessary input:
Unnotated genomes in Fasta format - nucleotides - in a single directory.

## 1. Get genome metrics

### 1.1) Quality check - CheckM

```bash
# checkm lineage_wf -t ${NSLOTS:-1}  --tab_table -x fa -f $3 $1 $2 
qsub  -N checkm_job    /path_to/submission_script.sh /data/msb/user/MAG_folder /data/msb/user/output/checkm /data/msb/user/output/checkm.tsv
```
**Output** that will later be used on this workflow: checkm.tsv

### 1.2) Get taxonomy - Gtdbtk

```bash
# gtdbtk  classify_wf --extension  fa  --cpus ${NSLOTS:-1} --genome_dir $1  --out_dir $2qsub  -N gtdbtk_job   /path_to/submission_script.sh /data/msb/user/MAG_folder /data/msb/user/output/
```
**Output** that will later be used: gtdbtk.bac120.summary.tsv \
**Note: **if adequate, also consider gtdbtk.ar122.markers_summary.tsv for the archaea domain.

### 1.3) Get genome metrics - BBtools

Run the script **statswrapper.sh** on the folder with the MAGs
```bash
bash /data/msb/tools/bbtools/bbmap/statswrapper.sh *.fa > bbtools.txt
```
**Note:** Simply run the script **statswrapper.sh**  on the directory with the MAGs. \
**Output** that will later be used: bbtools.txt


### <a name="references"></a>References


### <a name="author---contact"></a>How to cite:

### Author
Sandra Godinho Silva \
sandragodinhosilva@gmail.com
