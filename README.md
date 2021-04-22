# virus_assembly

A bash pipeline for de novo assembly of viral genomes generated via Illumina NGS. Currently handles the following viruses: HIV-1, RSV, RRV and HMPV.

Current version: V1

**Table of contents**
- [Requirements](#requirements)
- [Installation](#installation)
- [Usage](#usage)
- [Example](#example)

## Requirements
A conda package manager like [Miniconda3](https://docs.conda.io/en/latest/miniconda.html).

## Installation

1.  Download the initial environment installation file 
   ```
   wget https://raw.githubusercontent.com/laulambr/virus_assembly/main/scripts/install_env.sh
   ```
2. Run the script in the terminal 
  ```
   bash ./install_env.sh
   ```
3. Check if installation worked
  ```
   conda activate virus_assembly
  ```
 ## Usage
   ```
 Pipeline: NGS pipeline for viral assembly.
usage: virus_assembly [-h -v -p -q] (-i dir -m value -t value )
(-s string) 
with:
    -h  Show help text
    -v  Version of the pipeline
    -n  Name of RUN.
    -i  Input directory
    -s  Viral species
    -c  Perform clipping of primers
    -q  Perform quality check using fastQC
    -m  Memory
    -t  Number of threads
   ```
 ### Usage
 1. Activate environment.
 
   ```
   conda activate virus_assembly
  ```
 2. Head to the directory where you will perform the analysis.
 3. Place the raw fastq.gz files in a directory called source.  
 4. Create a list holding the sample names from you sequencing files called IDs.list and place it in the main directory.
 5. Start the pipeline using the following command
   ```
   virus_assembly -i path/to/main/directory -s VIRUS 
  ```
6. When the pipeline has finished, 5 additional folders will have been created:
      * 1_reads: Includes the trimmed and normalised reads.
      * 2_ref_map: Includes a bam file of the trimmed reads against the viral reference genome and a pdf with the qualimap results.
      * 3_contigs: Includes the de novo assembled contigs by megahit for each sample.
      * 4_filter: Includes the high converage contigs generated by megahit (_ *_hicov.fasta_), filtered and reorientated against the viral reference genome (_ *_reoriented.fa_)
      * 5_remap: Includes both a fasta file holding the viral contigs for that sample and a bam file of the trimmed reads agains those contigs. 
  
  ### Example
 1. Activate environment.
 
   ```
   conda activate virus_assembly
  ```
  2. Head to the directory with the github clone of this repository and head to the test data folder 
   ```
 cd $CONDA_PREFIX/virus_assembly/test_data
  ```
  3. Run the following command
   ```
 virus_assembly -i $CONDA_PREFIX/virus_assembly/test_data -s HIV
  ```
  4. The pipeline will run, check the newly created 5_read directory for a fasta file containing the new de novo assembled HIV-1 provirus.
   
  ### Included viral reference genomes
  * **HIV**: K03455.1
  * **RSV**: MH760627; MH760652
  * **RRV**: RRV_ref (Accession pending)
  * **HMPV**: HMPV205; HMPV218 (Accessions pending)

