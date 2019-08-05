# Quantify transcripts with RNA-seq

Salmon is a fast and accurate tool for quantifying trancript
abundances, which can then be used to also generate gene-level
quantifications.

The latest binary for running Salmon can be found here:

<https://github.com/COMBINE-lab/salmon/releases>

A workflow of how to run Salmon can be found here:

<https://combine-lab.github.io/salmon/getting_started/>

First you'll need to download or generate a FASTA file of all of the
transcript sequences. You can download a FASTA file of transcript
sequence from
[GENCODE](https://www.gencodegenes.org/). You can also generate such a
file using a tool such as
[rsem-prepare-reference](http://deweylab.biostat.wisc.edu/rsem/rsem-prepare-reference.html)
with a GTF file and a genome FASTA file. It's a good idea to download
the GTF file whenever you download a transcripts FASTA file.

Then, the two Salmon steps are generating an index, and then quantifying each
sample against that index. Good to use a descriptive index name.
You should put the version number on the end of the index name (whatever 
version you are using, not 0.7.2).

```
salmon index -t gencode.v27.transcripts.fa -i gencode.v27_salmon_0.7.2
```

Quantifying reads against this index might look like:

```
salmon quant -i gencode.v27_salmon_0.7.2 \
  -l IU \
  -1 fastq/sample_1.fastq.gz \
  -2 fastq/sample_2.fastq.gz \
  -p 6 -o quants/sample
```

The `-l IU` parameter specifies we have paired-end reads facing inward
and an unstranded protocol. For other library types, see the Salmon website.

See the workflow above for an example of how to incorporate this into
a bash script across a number of samples.
