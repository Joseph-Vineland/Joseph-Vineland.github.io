# Self-Correcting Genome Assembly

The following flowchart describes the genome assembly process.

![alt text](https://www.melbournebioinformatics.org.au/tutorials/tutorials/assembly/media/assembly-flowchart.png?raw=true)

In particular, the “Quality evaluation” step should definitely include building a k-mer frequency histogram.  Why?  It tells you so much about the data and the organism in one concise image.  It shows read coverage, heterozygosity levels, the amount of genome duplication, the error rate of your reads, the estimated size of your genome, etc.  It lets you know what you are working with and what you are up against.  This step should never be skipped.

![alt text](https://ucdavis-bioinformatics-training.github.io/2020-Genome_Assembly_Workshop/kmers/figures/genomescope.png?raw=true)

I recommned using Genomescope for your k-mer frequency histogram.

Anyways, I digress.  In my experience you can get caught in the flowchart's loop for months.  You can assemble the genome, find out the assembly isn’t OK, then try to fix the issues and assemble again, only to find out the assembly still isn’t OK.  This happens over and over.  
However, I have found a solution for this, provided you have Hi-C data and a genetic map to work with.  

The juicer/3d-dna pipeline takes contigs and assembles scaffolds with the help of Hi-C data. The Chromonomer software take scaffolds and assembles chromosomes with the help of genetic linkage maps.
Why is this a good strategy for genome assembly? These software tools will automatically correct assembly errors made during previous steps in a logical fashion. They prevent you from having to “double back” and repeat previous steps after trying to fix the assembly errors yourself. It saves loads of time, since the software edits your inputs for you. If your data is good, you will get a high quality, chromosome-level genome assembly with minimal effort.
In order to carry out this procedure, you need to create AGP file.
Here is a [script](https://github.com/Joseph-Vineland/AGPfromHiC) I wrote to render an AGP file from the outputs of the 3d-dna software: https://github.com/Joseph-Vineland/AGPfromHiC

This script generates an AGP file from the output of the juicer/3d-dna pipeline. The resulting AGP file is input to Chromonomer in order to construct a chromosome-level genome assembly.

Usage: `perl mkAgpFileFromHiC.pl <assembly.FINAL.fasta> <assembly.FINAL.assembly>`

I hope it can help you on your genome assembly journey!

Links to external software:

https://github.com/aidenlab/juicer

https://github.com/aidenlab/3d-dna

http://catchenlab.life.illinois.edu/chromonomer/

(Use the juicer/3d-dna software to assemble your scaffolds.  Use the script in this repository to generate an AGP file.  Then use the chomonomer software to build the chromosomes out of the scaffolds.)

