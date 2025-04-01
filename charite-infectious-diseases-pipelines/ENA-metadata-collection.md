---
title: ENA Raw Read Submission
layout: default
---

# 📤 ENA Metadata collection

## Mandatory info for samples: 


1. Taxonomy ID of the organism as in the  NCBI Taxonomy database. For example 9606 for Homo sapiens and 10090 for Mus musculus.

2. Scientific name

3. sample alias, title and description. These three can be the same. Alias is a unique ID, will be generated if not available. Or, consider this:

                                                                                                   
sample_alias 	sample_title 	sample_description
1_wt_ctr 	WT CT 	WT macrophage control


4. Collection date - could range from missing to restricted access to 2008-01-23 or 2008. Exact info is not needed.

5. geographic location, that is, country and/or sea. For example, Germany, if the experiment was performed at Charité.


Other info like sex, tissue type, isolate, cell line, strain etc. are optional.


## Mandatory info for reads:


Read file formats supported: CRAM, BAM, SE fastq, PE fastq, HDF5 and FAST5


Sample: Sample accession provided by ENA when samples checklist was uploaded (Samples report)

Study: Study accession (Study report)

[Can get Sample and Study only after starting the submission process]


Instrument_model: There are options to pick from. For example, Illumina Novaseq 6000

Library_name: could be similar to sample alias, etc

Library_source: choose from options, e.g., TRANSCRIPTOMIC

Library_selection: choose from options, e.g., PCR, cDNA

Library_layout: Options: single or paired reads


Forward_file_name and forward_file_md5

Reverse_file_name and reverse_file_md5

[Last two are from step 7a]

