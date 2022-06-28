# lab-protocols

## About 

Protocols corresponding to the following paper:

Parallel changes in gene essentiality over 50,000 generations of evolution

Anurag Limdi, Sian V. Owen, Cristina Herren, Richard E. Lenski and Michael Baym (https://doi.org/10.1101/2022.05.17.492023)

In this project, we performed transposon sequencing of the ancestors and evolved clones after 50,000 generations of evolution to identify how the distribution of fitness effects and gene essentiality changes over evolution.


## Organization

The repository is organized into two main folders

### protocols

This folder contains protocols for the three main steps of the wet-lab experiments for the project

- Constructing transposon libraries
- Fitness assays in minimal media
- Sequencing library preps (UMI-TnSeq)

### barcode_compatibility

- For multiplexed sequencing of more than one sample on Illumina machines, we need to tag sequencing libraries with distinct DNA barcodes, so we can tell which read came from which sample. 
- Because of the error rate in the sequencing by synthesis approach, there is a small chance that the barcode sequence is incorrectly inferred. 
- This issue is compounded if two DNA barcode sequences are relatively close in sequence space. For instance, if barcode 1 is ATGC and barcode 2 is AAGC, a single mistake in reading the second position of the barcode can lead to sequencing reads being misattributed to the wrong sample, and messing up downstream analyses. This is known as `barcode switching`

To ensure that barcode switching is minimized in our Illumina NovaSeq run with >400 samples, I run the Jupyter notebook:

#### Choosing barcodes compatible with TnSeq primers.ipynb

- I iterate over every pair of barcodes for the whole genome sequencing samples (WGS) and the TnSeq samples, and calculate the Hamming distance.
- If the Hamming distance of a WGS barcode (compared against any TnSeq barcode) is greater than equal to 3, I exclude from use in any experiments for this sequencing run.