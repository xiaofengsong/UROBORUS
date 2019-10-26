# UROBORUS

UROBORUS is a software tool for circular RNA identification from RNA-Seq data sets.

## Introduction

Recent evidence suggested that many endogenous circular RNAs (circRNAs) may play roles in biological processes. However, the presence of circRNAs and their expression patterns in human species are not well understood. Computationally identifying circRNAs from RNA-seq data is a primary step to study their expression pattern and biological roles. Here, we have developed computational pipeline named UROBORUS to detect circRNAs in total RNA-seq data. Compared with two available computational approaches, UROBORUS is an easy-to-use and efficient tool that can detect circRNAs with low expression levels in total RNA-seq without RNase R treatment. 

Please note that circular RNA does not has PloyA tail, so you can not detect any circRNA in PolyA RNA-seq. You should use PolyA minus or total RNA-seq data to detect circular RNA.

## Installation

The following fostware would be installed in your cluster or computer before running the UROBORUS.pl.

*  Perl (>=5.24.0), https://www.perl.org/get.html.   
    `Perl should be built using the useithreads configuration option. If not, you would recieve an error message – "Perl not built to support threads", when running UROBORUS.pl.`
    
*  Tophat (>=2.1.0), http://ccb.jhu.edu/software/tophat/index.shtml.

*  Bowtie (>=1.1.2), http://bowtie-bio.sourceforge.net/index.shtml.

*  Bowtie2 (>=2.2.9), http://bowtie-bio.sourceforge.net/bowtie2/manual.shtml.

*  Samtools (>=1.9), http://samtools.sourceforge.net/.    

## Usage

Before using UROBORUS.pl, you should use TopHat to align the reads to genome, and get the unmapped.sam and accepted_hits.bam files.

    UROBORUS.pl 2.1.1   (Oct. 1, 2019)
    usage:
            perl UROBORUS.pl -index /path/genome -gtf /path/genes.gtf -fasta /path/ unmapped.sam accepted_hits.bam
    Options:
            -index:	genome index (use bowtie1 index);
            -gtf:	gene annotation file (*.gtf file);
            -fasta:	path for genome sequence in fasta file (*.fa) in separate chromosome;
            -p:	    threads (Integer, default = 6);
            -temp:	keeping the temporary file (0 means no, 1 means yes, default = 0);
            -help:	usage help;
            
## Note

1. If the genome sequences were saved as '**chr1.fa**' or '**1.fa**', then the -fasta should be set as **-fasta path/**;
2. if the genome sequences were saved as '**Homo_sapiens.GRCh38.dna.chromosome.1.fa**', then the -fasta should be set as **-fasta path/Homo_sapiens.GRCh38.dna.chromosome**;

## Example
    
    Command:
            perl UROBORUS.pl -index bowtie1_hg19/hg19 -gtf genes.gtf -fasta Chromosomes_home/ unmapped.sa accepted_hits.bam

## Output file format:

    The output file contains eight columns:
        1.  Chromosome
        2.  Start of Junction
        3.  End of Junction
        4.  Strand
        5.  Parental Gene Name
        6.  Genomic Distance
        7.  Read Counts
        8.  Matched Transcript ID
        
    Output example:
        chr18	54426095	54448887	+	WDR7	22792	18	NM_052834
        chr5	64537930	64569274	-	ADAMTS6	31344	17	NM_197941
    
## Documentation

Documentation on the software can be found at http://bioinfo.nuaa.edu.cn/uroborus.html.

## Reference

**Song X**, Zhang N, Han P, Lai RK, Wang K, Lu W. Circular RNA Profile in Gliomas Revealed by Identification Tool UROBORUS. Nucleic Acids Research, 2016, 44:e87.
