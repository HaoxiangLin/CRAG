# CRAG
**C**ell f**R**ee dn**A** fra**G**mentation (CRAG): *De novo* characterization of cell-free DNA fragmentation hotspots.

## Table of Contents
1. [Quick start](#Quick-start)
2. [Installation](#Installation)
3. [Usage](#Usage)
4. [Citation](#Citation)
5. [License](#License)
6. [Contact](#Contact)

## Quick start
1. Install
	```
	git clone --recursive https://github.com/epifluidlab/CRAG.git
	cd CRAG
  	pip install pysam
	```

2. Run the example test file at your bash command line to call hotspot
	```
	cd CRAG/hotspots_calling
	python bam_read.py -in test.bam -out test_dir
	matlab -nodisplay -r 'CRAG test_dir 1; exit;' 	
	```
	
	This should produce the following files (inside test_dir/result_n/):
	* the hotspots (peak_all.mat, peaks.bed), 
	* fragmentation pattern around hotspots (IFS_plot.fig, IFS_plot.pdf)
	* enrichment patterns (TSS_plot.fig, TSS_plot.pdf, CTCF_plot.fig, CTCF_plot.pdf, Enrichment_plot.fig,Enrichment_plot.pdf) 

## Installation
#### Prerequisites
* Linux, Mac OSX, and Windows
* Matlab 2019b
* python 2.7 
* pysam 0.12.0.1 or above
* samtools 1.9

#### required files
1. Bam file (paired-end whole-genome sequencing, recommend to have at least 400 million fragments in autosomes after the samtools filtering step. If you want to call hotspots for several chrommsomes (not the whole autosome), you can provide the bam file only with the corresponding chromosomes.)
2. Dark regions (provided in resource folder for hg19, or could be downloaded from UCSC table browser)
3. Mappability files (provided in resource folder for hg19, or could be generated by [GEM library tools](https://wiki.bits.vib.be/index.php/Create_a_mappability_track)

## Usage

### Pre-process bam file
```
samtools view -bh -f 3 -F 3852 -q 30 input.bam > output.filtered.bam

python bam_read.py -in output.filtered.bam -out result_dir
```

### Hotspot calling
Two modes for the hotspot calling: 1 - call hotspots using IFS. 2 - call hotspots using GC bias corrected IFS.
There are two choices to run the tool:
- Run it directly at matlab (all the following code examples will follow this style)
```
CRAG('result_dir',1)
```
- Run it at linux bash with matlab installed
```
matlab -nodisplay -r 'CRAG result_dir 1; exit;'
```
#### Options for hotspot calling
```
-mappability track
-dark regions
-global p value cut-off
-local p value cut-off
-ks-test
-fdr cut-off
-hotspot distance for merging
```

### Unsupervised clustering, and t-SNE
	* For steps using GC bias corrected IFS:
	`cd `
	* For steps using IFS:
	`cd `
	
	1. Obtain IFS score in each sample. If using low-coverage WGS, please group samples based on their category. e.g.:
	`IFS_write('Breast_cancer/sample1')`
	
	2. Call hotspots:
	* based on GC bias corrected IFS:
	`nature_peak_GC('Breast_Cancer')`
	
	3. Merge hotspot locations:
	`nature_peak_file_merge()`
	
	4. Obtain IFS matrix:
	`nature_feature_obtain_GC('Breast_Cancer')`
	
	5. Select most variable hotspots by one-way ANOVA test:
	`ANVOA_GC()`
	
	6. run t-SNE:
	`TSNE()`
	
	7. Unsupervised clustering (will further filter hotspots based on their mean z-score difference within vs. outside group):
	`cluster_nature_GC()`


### Cancer vs. healthy classification
TBD

#### Options for cancer vs. healthy classification
```
- k fold
- random seed
- GC bias correction
```

* Recommanded setting:
`code`

### Tissues-of-origin prediction
TBD

#### Options for tissues-of-origin prediction
```
- k fold
- random seed
- GC bias correction
```

* Recommanded setting:
`code`

#### Raw source code in manuscript
The raw source code and their readme files are inside manuscript/

## Citation
```
Zhou X & Liu Y. "De novo characterization of cell-free DNA fragmentation hotspots boosts the power for early detection and localization of multi-cancer". In preparation.
```
## License
* For academic research, please refer to MIT license.
* For commerical usage, please contact the authors.

## Contact
* Xionghui Zhou <xionghui.zhou@cchmc.org>
* Yaping Liu <lyping1986@gmail.com>















	

