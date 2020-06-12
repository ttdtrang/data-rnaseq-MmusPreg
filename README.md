# Data package for transcriptomic profiles from mouse brain regions during pregnancy

## Sources

  * Experimental data were generated in SEQC Toxicogenomics project. Original citation: Ray S et al., "An Examination of Dynamic Gene Expression Changes in the Mouse Brain During Pregnancy and the Postpartum Period.", G3 (Bethesda), 2015 Nov 23;6(1):221-33 (PMID: [26596646](https://www.ncbi.nlm.nih.gov/pubmed/26596646))
  * Processing:
    * Sequencing reads were downloaded from SRA, at [PRJNA289455](https://www.ncbi.nlm.nih.gov/bioproject/?term=PRJNA289455)
    * Re-processed by first aligning on Mouse genome GRCm38.p6 + 92 ERCC sequences, annotated by Gencode (m25), using STAR 2.7.1a, and then quantified by RSEM for abundance levels at gene and transcript levels.
  
## Usage

Install the package, import the library and load the data set

```R
devtools::install_github('ttdtrang/data-rnaseq-MmusPreg')
library(data.rnaseq.MmusPreg)
data(mpreg.rnaseq.gene)
dim(mpreg.rnaseq.gene@assayData$exprs)
```

The package includes 2 data sets, one for transcript-level counts/TPM and another for gene-level counts/TPM. Counts are non-integer estimate of `expected_count` by RSEM.

## Steps to re-produce data curation

1. `cd data-raw`
2. Download all necessary raw data files which include
```
3.0M	feature_attrs.genes.tsv
7.0M	feature_attrs.transcripts.tsv
8.0K	featureCounts-summary.genes.tsv
8.0K	featureCounts-summary.transcripts.tsv
5.2M	matrix.gene.expected_count.RDS
4.2M	matrix.gene.featureCounts.RDS
5.4M	matrix.gene.tpm.RDS
17M	matrix.transcripts.expected_count.RDS
15M	matrix.transcripts.tpm.RDS
24K	PRJNA289455_metadata_cleaned.tsv
20K	starLog.final.tsv
```
3. Set the environment variable `DBDIR` to point to the path containing said files
4. Run the R notebook `make-data-package.Rmd` to assemble parts into `ExpressionSet` objects.

You may need to change some code chunk setting from `eval=FALSE` to `eval=TRUE` to make sure all chunks would be run. These chunks are disabled by default to avoid overwriting existing data files in the folder.
