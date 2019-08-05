# Downloading files (from European Nucleotide Archive)

Downloading files is a pretty simple task. For sequencing data, I like
to see if the file exists on the European Nucleotide Archive, because
they offer simple ftp downloads of gzipped FASTQ files, whereas the
Sequence Read Archive requires a slower decompression process.

The ENA is here:

http://www.ebi.ac.uk/ena

You'll want to find urls that start with `ftp://` and end with
`.fastq.gz`. If the data is paired-end RNA-seq data, you'll need the
`_1.fastq.gz` file as well as the `_2.fastq.gz` file for a given
experiment. 

In order to download the files in one go, my steps are the following:

* Download a plain-text sample table from SRA's Run Selector (by
  clicking *All runs* from an SRX page) or from ArrayExpress.
* Write an R script to read in this file, clean it up, and write out a
  list of ftp locations, as well as a separate CSV file linking ERR or
  SRR to sample ID and/or phenotypic information
* Run `wget` with the following type of call:

```
wget -o logfile \
     -i urls \
	 --no-clobber \
	 --progress=dot:mega \
	 --random-wait \
	 -P /path/to/files/
```

If you need to convert from ERR identifiers to ftp locations, you can
always use this function:

https://gist.github.com/mikelove/f539631f9e187a8931d34779436a1c01

---

**Note**: If you need to download from SRA, the link is here:

https://www.ncbi.nlm.nih.gov/sra

And you'll need to use `fastq-dump` in the SRA Toolkit to decompress
the files. You can provide `fastq-dump` a list of SRA accession IDs
and it will download the compressed `.sra` files into a hidden
directory in your home, and then decompress the files into your
working directory in one step.

https://trace.ncbi.nlm.nih.gov/Traces/sra/sra.cgi?view=toolkit_doc

https://trace.ncbi.nlm.nih.gov/Traces/sra/sra.cgi?view=toolkit_doc&f=fastq-dump

