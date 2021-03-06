# Analytical pipeline of the pea aphid (*Acyrthosiphon pisum*) AL4 strain genome
This document is a walkthrough of the methods and code used to analyze the chromosome-level pea aphid genome assembly (AL4 assembly). In the aphid paper, we used HiC and Chicago library to build the chromosome-level assembly and analyzed gene family evolution on chromosomes. We also sequenced seven *A. pisum* individuals for detecting X chromosome, carotenoid gene and wing-dimorphism related sequence variations. 

## 1 - Genome Assembly Verification: 


### 1.1 - BUSCO analysis 
Download the AL4 assembly under the NCBI accession number: PRJNA496478. The AL4 assembly will be called assembly.fasta in this pipeline. 

Install BUSCO version 3.0.2 and Insecta near-universal single-copy orthologs from OrthoDB v9: https://busco.ezlab.org

    python run_BUSCO.py -i assembly.fasta -l ./insecta_odb9/ -m geno -f -o busco_output -c 8 > assembly.log

### 1.2 - Microsatellite primer mapping
Microsatellite primer sequences can be found under: ./step_1.2/

Scripts can be found: ./step_1.2/cmd.sh

The R script for Figure 2 can be found under: ./step_1.2/

### 1.3 - Sequencing depth evaluation and Heterozygosity calculation: 
Data and scripts can be found: ./step_1.3/

The R script for Figure 3 is also under: ./step_1.3/

## 2 - Genome Annotation using WQ_MAKER: 

**The control file for MAKER can be found under ./step_2/**

    wget http://bipaa.genouest.org/sp/acyrthosiphon_pisum/download/annotation/v2.1b/aphidbase_2.1b_transcripts.fasta

    wget http://bipaa.genouest.org/sp/acyrthosiphon_pisum/download/annotation/v2.1b/aphidbase_2.1b_pep.fasta

    nohup wq_maker -contigs-per-split 1 -cores 1 -memory 204800 -disk 409600 -N wq_aphid_${USER} -d all -o master.dbg -debug_size_limit=0 -stats test_out_stats.txt > log_file.txt 2>&1 & 

## 3 - Genome Duplication Analysis: 

Scripts relate to BLASTP and finding reciprecal best BLAST hits: ./step_3/

The R script for Figure 4 is also under: ./step_3/

LAST alignment and Circos plot script is under: ./step_3/circos/

## 4 - Location of Functional Genes: 

Scripts can be found under: ./step_4/

## Citation:
Li, Y., Park, H., Smith, T.E. and Moran, N.A., 2019. Gene family evolution in the pea aphid based on chromosome-level genome assembly. Molecular biology and evolution, 36(10), pp.2143-2156.


