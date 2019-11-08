## How to submit genome assembly to ENA

ENA has made genome assembly really simple using webin-cli. Web-cli is only the way to submit genome assembly to ENA.

1) First, download the webin-cli jar file from github repo - https://github.com/enasequence/webin-cli/releases
2) Prepare the manifest file with all metadata on the genome assembly. If you already have submitted the raw seqeunce reads, used in assembly, to ENA before, you will have a project accession id starting PRJEB. If you have not submitted, I suggest you to submit raw sequence reads to ENA first and get a PRJEB accession id.

Manifest file is a tab delimited 2 column file. See the complete files that are accepted in this link:
https://ena-docs.readthedocs.io/en/latest/submit/general-guide/webin-cli.html#stage-2-prepare-the-files

Below is the sample manifest file I prepared:

```
STUDY	PRJEBXXXXX
SAMPLE	SAMEAXXXXXX
ASSEMBLYNAME	Assembly of abc genome
ASSEMBLY_TYPE	clone or isolate
COVERAGE	100
PROGRAM	velvet
PLATFORM	Illumina Genome Analyze,Illumina Genome Analyze II
MOLECULETYPE	genomic DNA
DESCRIPTION	Describe the full text of assembly here. It is optional, however.
RUN_REF	(This is list of ERR accession of raw reads. e.g ERR10000,ERR20000,ERR30000,..........)
FASTA	/path_to_your_assembly_fasta_gzipped_file
```
3) Validate the manifest file you prepared with the command below. You should have java version as the webin-cli documentation says. Please check that you have requirements to run webin-cli.

```
java -jar /path/to/webin-cli-1.8.12.jar -context=genome -manifest manifest.txt -username webin-username -password webin-password -centerName 'your institute/centre name' -validate
```

You might get error during validation if there is any incorrect information in the manifest file. If you get any error, make corrections in the manifest file and re validate.

When validation is successful, it will say:

```
INFO : Your application version is x.x.xx
INFO : Creating report file: /your_output_dir/./webin-cli.report
INFO : The submission has been validated successfully.
```

4) Submit the assembly

```
java -jar /path/to/webin-cli-1.8.12.jar -context=genome -manifest manifest.txt -username webin-username -password webin-password -centerName 'your institute/centre name' -submit
```

The output will display the analysis accession for the assembly. Make note of that accession for publication purposes.

