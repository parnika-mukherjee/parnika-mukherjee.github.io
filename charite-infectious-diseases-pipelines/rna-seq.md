---
title: Charité Infectious Disease Pipelines
layout: default
---

What is bulk RNA-seq data?

Bulk RNA-seq provides a snapshot of the average gene expression levels at a specific time point across a population of cells, rather than individual cells.

Key characteristics:

  - High sensitivity: It's good at detecting even low-abundance transcripts because of deeper sequencing per sample.

  - Less expensive and simpler than single-cell RNA-seq.

  - No cell-level resolution: You can’t distinguish what genes individual cells were expressing — only the average. (Cell types can be resolved with deconvolution tools)

---

What does bulk RNA-seq data look like?


---

Applications of RNA-seq data

Demystifying emerging bulk RNA-Seq applications: the application and utility of bioinformatic methodology
Amarinder Singh Thind , Isha Monga , Prasoon Kumar Thakur , Pallawi Kumari , Kiran Dindhoria , Monika Krzak , Marie Ranson , Bruce Ashford
Briefings in Bioinformatics, Volume 22, Issue 6, November 2021, bbab259, https://doi.org/10.1093/bib/bbab259

---

Data analysis steps:
1. Quality control
2. Read-mapping and quantification of features
3. Differential gene expression
4. Process / pathway enrichment

Quality control

---

Read-mapping and quantification

Pipeline for read-mapping and feature quantification is [here](https://github.com/parnika91/nf-pipelines/)

---

Differential gene expression

---

Functional enrichment

---
