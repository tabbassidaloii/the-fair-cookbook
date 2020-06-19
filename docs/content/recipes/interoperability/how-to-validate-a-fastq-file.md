
# Table of Contents
0. [Abstract](#Abstract)
1. [Graphical Overview](#Graphical%20Overview)
2. [Requirements](#Requirements)
3. [Recipe instructions](#Recipe%20instructions)
4. [Possible improvements from the state of this recipe](#Possible%20improvements%20from%20the%20state%20of%20this%20recipe)
5. [Further reading](#Further%20reading)
6. [Capability & Maturity Table](#Capability%20&%20Maturity%20Table)
7. [FAIRification Objectives, Inputs and Outputs](#FAIRification Objectives, Inputs and Outputs)
5. [Table of Data Standards](#Table%20of%20Data%20Standards)
6. [Authors](#Authors)
8. [License](#License)

---

## Abstract

The FASTQ format is a popular format for storing sequences (i.e. letters representing nucleotides in a piece of DNA) and their corresponding quality scores. However, FASTQ files can exhibit a large variety of variants=dialects, or might get corrupted during file transfers. It is thus important to check the conformance of a given FASTQ file to a specific expectation of "how it should look like", e.g. to ensure compatibility with a given tool. This recipe will outline how a FASTQ file can be checked locally, i.e. without transferring it out of the borders of a certain local computer environment.

___


## Graphical Overview

[![](https://mermaid.ink/img/eyJjb2RlIjoiZ3JhcGggVERcbkF7UmVxdWlyZW1lbnRzIGZ1bGZpbGxlZD99IC0tPnxZZXN8IEJbQXBwbHkgdGhpcyByZWNpcGVdXG5BIC0tPnxOb3wgRChTVE9QKVxuQiAtLT4gQyhGQVNUUSBmaWxlIHZhbGlkYXRpb24gb3V0cHV0KVxuIiwibWVybWFpZCI6eyJ0aGVtZSI6ImRlZmF1bHQifSwidXBkYXRlRWRpdG9yIjpmYWxzZX0)](https://mermaid-js.github.io/mermaid-live-editor/#/edit/eyJjb2RlIjoiZ3JhcGggVERcbkF7UmVxdWlyZW1lbnRzIGZ1bGZpbGxlZD99IC0tPnxZZXN8IEJbQXBwbHkgdGhpcyByZWNpcGVdXG5BIC0tPnxOb3wgRChTVE9QKVxuQiAtLT4gQyhGQVNUUSBmaWxlIHZhbGlkYXRpb24gb3V0cHV0KVxuIiwibWVybWFpZCI6eyJ0aGVtZSI6ImRlZmF1bHQifSwidXBkYXRlRWRpdG9yIjpmYWxzZX0)

<div class="mermaid">
graph TD
A{Requirements fulfilled?} -->|Yes| B[Apply this recipe]
A -->|No| D(STOP)
B --> C(human-readable FASTQ file validation output)
</div>

---

## Requirements:

This recipe assumes the following:

  - you have a Linux machine available, preferentially Debian (no root access needed)
  - you have basic knowledge of how to use a terminal (called "shell", this can be bash or similar)
  - you are sufficiently skilled in Python (basic skills sufficient)
  - Python3 and pip are installed
  - your file is available from your home directory and we assume for simplicity in the following that it is called `myfile.fastq` (replace this filename as necessary in the recipe instructions; you can download a demo file from here: [/static_assets/myfile.fastq]


Checking the requirements (tests):

  - Start up a console. Type `echo hello` and hit return. You should see `hello` as output.
  - OPTIONAL: Switch to your favorite virtual environment solution (e.g. via `conda activate py3`), if you use such a solution.
  - Execute `python -V` and check its output. It should be roughly similar to `Python 3.7.4`.
  - Execute `pip -V` and check its output. It should be roughly similar to `pip 19.2.3 from /home/r.giessmann/anaconda3/envs/py3/lib/python3.7/site-packages/pip (python 3.7)`.

___

## Recipe instructions

### Install BioPython

On the shell, execute:

```
pip install --user biopython
```

(adapt if you are an experienced user)


We assume here `biopython-1.77` will be installed now.

### Start Python, load Biopython

On the shell execute:

`python`

This will bring you into the python parser. (More experienced users might want to start `ipython` instead.)

Now, load the Biopython package and the SeqIO module with:  

```
import Bio
import Bio.SeqIO
```

### Pre-load the FASTQ file, run a very basic file format validation check

Execute further in the python session from above:

```
fastq_iterator =  Bio.SeqIO.parse("myfile.fastq", format="fastq-sanger")
for read in fastq_iterator:
    pass
```

This will raise an Exception (actually: a ValueError) with a very short, and a possibly inconclusive error message.

If no message is obtained, the file format validation was successful in its given form.


### Limitations of this recipe

This recipe in its current form has the following limitations regarding format validation:

  - with the tool above, the nucleotide alphabet is checked by default only on whether it conforms to a "SingleLetterAlphabet", but this allows even insensible characters such as `ä` as nucleotide letters.
  - the error messages are not indicating at which position exactly an error occured, i.e. which letter of the quality score is incorrect (the error message is e.g. `ValueError: Invalid character in quality string` where it might be preferable to get an error message like `ValueError: Invalid character "ö" in quality string of read 12 at position 5.`)
  - the read names are not further checked and might not fulfill specific requirements of the subsequent tool, for which this check was supposed to be designed.


### Extendability of this recipe

- The tool above can also be used to check selectively for other variants of the PHRED score encoding, i.e. `fastq-illumina` or `fastq-solexa`. See <https://biopython.org/wiki/SeqIO> for a list of supported file formats.
- This recipe can also be applied to check general sequences without quality scores, e.g. files in FASTA format.


## Possible improvements from the state of this recipe

- It would be preferable to introduce a further, harder check for the specification of the nucleotide sequence, e.g. only allowing the the "IUPAC DNA alphabet" (see <https://www.ncbi.nlm.nih.gov/pmc/articles/PMC322779>), including degenerate bases (e.g. `B` representing the bases (`A` OR `G` OR `T`), lowercase and uppercase mixtures (e.g. `acGTgTGaa`), and gaps (symbolized by `.`).
- It might be possible to extend the tool above into the desired direction of more consistent checks, considering the content of <https://biopython.org/wiki/SeqIO_dev>.
- It would be preferable to be able to exchange the concrete FASTQ specification that was used to derive the validation result with other tools and/or make them visible.
- It would be preferable to document the result of the file format validation in a machine-readable and consistent way.


## Further reading

- The documentation of BioPython, and specifically Bio.SeqIO: <https://biopython.org/docs/1.77/api/Bio.SeqIO.QualityIO.html>


## Capability & Maturity Table

| Capability  | Initial Maturity Level | Final Maturity Level  |
| :------------- | :------------- | :------------- |
| Interoperability | minimal | repeatable |

----

## FAIRification Objectives, Inputs and Outputs

| Actions.Objectives.Tasks  | Input | Output  |
| :------------- | :------------- | :------------- |
| [Format Validation](http://edamontology.org/operation_0336)  | [FASTQ file](https://fairsharing.org/FAIRsharing.r2ts5t)  | [report](http://edamontology.org/data_2048)  |

---

## Table of Data Standards

| Data Formats  |
| :------------- |
| [FASTQ](https://fairsharing.org/FAIRsharing.r2ts5t)  |

---


## Authors:

| Name | Affiliation  | orcid | CrediT role  |
| :------------- | :------------- | :------------- |:------------- |
| Robert T. Giessmann |  Bayer AG | [0000-0002-0254-1500](https://http://orcid.org/0000-0002-0254-1500) | Writing - Original Draft |

---


## License:

<a href="https://creativecommons.org/licenses/by/4.0/"><img src="https://mirrors.creativecommons.org/presskit/buttons/80x15/png/by-sa.png" height="20"/></a>
