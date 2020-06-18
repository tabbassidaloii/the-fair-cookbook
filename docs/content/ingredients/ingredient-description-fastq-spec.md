

# Table of Contents
0. <#Abstract>
1. [#What is FASTQ used for?]
2. [#What means "weak specification"?](#Graphical%20Overview%20of%20the%20FAIRification%20Recipe%20Objectives)
3. [#What are the variants of FASTQ to expect?](#FAIRification%20Objectives,%20Inputs%20and%20Outputs)
4. [#References](#Capability%20&%20Maturity%20Table)
5. [#Authors](#Authors)
5. [#License](#License)

---

## Abstract

The FASTQ format is a popular format for storing sequences (i.e. letters representing nucleotides in a piece of DNA) and their corresponding quality scores. FASTQ is a text-based data format with weak specification. This ingredient description will exemplify how a FASTQ file can look like, what variants=dialects are commonly found, and will list some sources for weak=pseudo specifications of this important de facto standard file format.

___

## What is FASTQ used for?

The FASTQ format is a popular format for storing sequences (i.e. letters representing nucleotides in a piece of DNA) and their corresponding quality scores. It is used in most genomics research projects, and is a format of choice e.g. for EMBL-EBI's ENA (European Nucleotide Archive) [https://ena-docs.readthedocs.io/en/latest/faq/archive-generated-files.html?highlight=fastq#fastq-file-format], or for NCBI's SRA (Sequencing Read Archive) [https://www.ncbi.nlm.nih.gov/sra/docs/submitformats/#fastq-files]. It also sits in trillions of files on individual researcher's hard disks / drives, in academia as well as in the industry.

The FASTQ format transports not only the sequence as determined by the sequencing machine, but also the quality (=trustworthiness) of each letter.

For more information on the FASTQ format, the authors recommend the wikipedia article as a start: <https://en.wikipedia.org/wiki/FASTQ_format>

___




## Authors:

| Name | Affiliation  | orcid | CrediT role  |
| :------------- | :------------- | :------------- |:------------- |
| Robert T. Giessmann |  Bayer AG | [0000-0002-0254-1500](https://http://orcid.org/0000-0002-0254-1500) | Writing - Original Draft |

___


## License:

<a href="https://creativecommons.org/licenses/by/4.0/"><img src="https://mirrors.creativecommons.org/presskit/buttons/80x15/png/by-sa.png" height="20"/></a>
