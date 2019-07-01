# RunOnBamToBigWig
Takes bam files from Run-On sequencing data as input and writes bigWig files as output to the user-assigned output-dir.

## Dependencies: 

The pipelines depend on several common bioinformatics tools: 
- [ ] samtools (http://www.htslib.org/download/)
- [ ] bedtools v2.28.0 (http://bedtools.readthedocs.org/en/latest/)
- [ ] bedGraphToBigWig (from the Kent source utilities http://hgdownload.cse.ucsc.edu/admin/exe/)

Please make sure you can call the bioinformatics tools from your current working directory.  

## Usage
```
Takes bam files from Run-On sequencing data as input and writes
bigWig files as output to the user-assigned output-dir.

Requirements in current working directory:
samtools, bedtools, and bedGraphToBigWig.

bash RunOnBamToBigWig.bsh [options]

options:

To get help:
-h, --help             Show this brief help menu.

Required options:
-SE, --SEQ=SE          Bam file from Single-end sequencing.
-PE, --SEQ=PE          Bam file from Paired-end sequencing.
-c, --chrom-info=PATH  Location of the chromInfo table.

I/O options:
-I, --bam=PREFIX.bam   Input bam file. If not specified, will take
                       *.bam in the current working directory as input
-T, --tmp=PATH         Path to a temporary storage directory.
-O, --output-dir=DIR   Specify a directory to store output in.

Required options for SE
-G, --SE_READ=RNA_5prime Single-end sequencing from 5' end of
                         nascent RNA, like GRO-seq.
-P, --SE_READ=RNA_3prime Single-end sequencing from 3' end of
                         nascent RNA, like PRO-seq.

Options for PE
--RNA5=R1_5prime    Specify the location of the 5' end of RNA
                    [default: R1_5prime].
--RNA3=R2_5prime    Specify the location of the 3' end of RNA
                    [default: R2_5prime].
                    Available options: R1_5prime: the 5' end of R1 reads
                                       R2_5prime: the 5' end of R2 reads
-5, --map5=TRUE     Report the 5' end of RNA [default on, --map5=TRUE].
-3, --map5=FALSE    Report the 3' end of RNA,
                    only available for PE [default off, --map5=TRUE].
-s, --opposite-strand=TRUE
                    Enable this option if the RNA are at the different strand
                    as the reads set at RNA5 [default: disable].

Optional operations:
--thread=1         Number of threads can be used [default: 1]
```

Example:

The pipeline requires chrom info (-c or --chrom-info=PATH).
Chrom info is a __tab-delimited__ file with two columns. The first column is the chromosome name and the second is the size of the chromosome. Please see http://hgdownload.cse.ucsc.edu/goldenPath/hg38/bigZips/hg38.chrom.sizes for example
```
export hg38_chinfo=/local/storage/data/hg38/hg38.chrom.sizes
bash RunOnBamToBigWig.bsh -SE -G -c $hg38_chinfo -I ABC.bam
```
