# EBM-Panel-Coverage
Workflow for the Illumina EBM panel target-based coverage analysis using Snakemake.

## Requirement
- Linux (tested on Debian v9.13)
- snakemake v7.25.0   
- python v3.11.3 
- mosdepth v0.3.3
- bedtools v2.28.0
- r-xlsx v0.6.5


## General Information
For each Illumina EBM hybridization-based sequencing run, a target-based coverage analysis is performed to identify the mean coverage, regions and bases failed to reach the target region coverage. For this, a coverage threshold of 30x and exon/intron boundaries of +/-20 bp based on the coding sequences of the target regions were defined. This snakemake workflow will look for the samplesheet of the sequencing run and the "Alignment_1" directory with the output data from the Illumina Pisces pipeline and will serve as input for the coverage analysis. The pipeline should be executed from the corresponding flowcell directory and the output data will be stored in a toplevel directory called "coverage". The main results of the coverage analysis are stored in a sample-wise manner in excel-based worksheets. 


## Usage
1. Change directory to the MiSeq flowcell folder of the current sequencing run for which the coverage analysis should be run:

```bash
cd "/mnt/nas-5268189/ifh-rechenzentrum1/illumina/MiSeqOutput/230413"
```

2. Create a samplesheet with the corresponding samples and targeted genes as depicted here. First column with sample ids should be tab seperated and the corresponding genes comma seperated. The file should be named as following "Run_" + "Date" + "_Genliste.txt" and stored in the toplevel directory of the flowcell folder:

```bash
57045	APC,MUTYH,NTHL1,POLD1,POLE
57149	BRCA1,BRCA2
57163	BRCA1,BRCA2
57225	BRCA1,BRCA2
57226	BRCA1,BRCA2
57281	BRCA1,BRCA2
57282	BRCA1,BRCA2
57300	BRCA1,BRCA2
57304	CFTR
57322	BRCA1,BRCA2
57325	TP53,CHEK2
57364	CFTR
```

3. Clone the repository into the runfolder:

    ```bash
    git clone "https://github.com/GenoMixer/EBM-Panel-Coverage.git"
    ```

4. Activate the snakemake environment with the relevant tools, i.e. mosdepth, bedtools and r-xlsx:

    ```bash
    conda activate "/mnt/nas-5268189/ifh-rechenzentrum1/bioinformatik/conda/envs/coverage"
    ```

5. Start a dry run (-n) and estimate the numbers of jobs(-j) provided by snakemake:

    ```bash
    snakemake -j 48 -n
    ```
