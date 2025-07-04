---
title: ENA Raw Read Submission
layout: default
---

# ENA Raw Read Submission Pipeline

Raw reads associated with a study must be deposited in a public repository, such as ENA, SRA NCBI, DDBJ, etc. I found the submission process for ENA to be the easiest.

This pipeline walks you through submitting raw sequencing reads to the [`European Nucleotide Archive (ENA)`](https://www.ebi.ac.uk/ena/browser/home). See [`Resource 1`](https://ena-docs.readthedocs.io/en/latest/index.html) below for the official documentation from ENA

## Before uploading raw reads to ENA

The first step is to register as user on the [`Webin Submissions Portal`](https://www.ebi.ac.uk/ena/submit/webin/accountInfo) of ENA. This profile can be used to submit multiple studies

Supported read file formats are: CRAM, BAM, Single-end FASTQ, Paired-end FASTQ, HDF5 and FAST5

Read submission can be completed in 3 steps:

   1. Register study on web interface
   2. Sample metadata upload via web interface
   3. Read upload via command line interface
   4. Read metadata upload via web interface

For required mandatory metadata information, see [`Metadata collection`](ENA-metadata-collection.md)

ALWAYS complete a [`test version`](https://wwwdev.ebi.ac.uk/ena/submit/webin/login) first and then repeat the steps for the [`production version`](https://www.ebi.ac.uk/ena/submit/webin/login)

## 📤 Uploading data to ENA Webin Submissions Portal

1. **Register study** on the test service. Release date can be pushed back or forward. Abstract and description can be added later. Study acession will then become available in "Studies Report". Save it for later use
   
   The 3 lines on top left part of the screen opens the dashboard for navigation
   
2. **Register samples** -> Download spreadsheet. For human or mouse RNA-seq data, choose "Other checklists". Next, for human/mouse data, choose "default checklist". Fill it up ([`see metadata collection for help`](ENA-metadata-collection.md)), go back to "Register samples" on dashboard and select Upload. Save assigned sample accession IDs from "Samples Report" for the read files checklist

   For environmental and organismal (host-associated) samples, check [`resource 2`](https://biodiversitydata-se.github.io/mol-data/ena-metabar.html)

3. **Reads upload**: To fill out the read files checklist, follow Step 4 in [`resource 2`](https://biodiversitydata-se.github.io/mol-data/ena-metabar.html)

   a. First, generate md5 checksum to verify read file integrity after upload. In the folder with the read files, run in terminal:

         for f in *fastq.gz; do md5 $f | awk '{ gsub(/\(|\)/,""); print $1"\t" $2 }'; done > md5sums.tsv
      
   Note the correct file extension used for your files - fastq.gz, fq.gz, etc. This command creates a tab-separated file with the md5 checksums and the file names. It should look like this (or in the reverse order of the columns):

         | 3b078583e52381db7d88abf7912b76c1 | i712_0001_CGGCGCA_i512A_0001_GTCTCCCT_R1.fastq.gz |
   
         | de91c8fc0d76dbfe05a45e7431109c97 | i712_0002_AAAATCC_i512A_0002_TTATGGGT_R1.fastq.gz |                                                   

      
   > Troubleshoot:
   > If the correct info is not on the tsv file, run the following in the terminal with one file name. Examine which output columns contain the filename and checksum. 
      
   > `md5sum i712_0031_AAAATCCCAGTT_i512A_0031_AACGTTTAGGGG_R1.fastq.gz | awk '{ gsub(/\(|\)/,""); print $1"\t" $2 }'`
      
   > For example, print different columns such as $1 and $3 instead of $1 and $2 in the command above. 
      
       
   This works for Mac and Linux. [`Example on Windows`](https://stackoverflow.com/questions/41838664/md5-hash-of-files-in-a-windows-folder))
  
      
   b. Next, upload the read files to the ftp server of ENA, preferrably remotely, as it can take a long time.
      
      ```
      ## Connect to ENA FTP server
      lftp webin2.ebi.ac.uk -u Webin-XXXXX
      ## Expected response: lftp Webin-XXXXX@webin2.ebi.ac.uk:~>
      
      ## Transfer read files
      mput ~/read-files/*.fastq.gz
      ## Expected response: Total x files transferred
      
      ## Disconnect from server
      bye
      ```
      
   This works for Mac and Linux. [`Example on Windows`](https://unihost.com/blog/how-to-connect-to-ftp-server/)

4. **Reads metadata upload**: to upload the read files checklist along with the md5 checksum for each file, go to Dashboard -> Submit Reads -> Select download option based on file format -> fill it up ([`see here for help`](ENA-metadata-collection.md)) -> upload.

Here, it is critical that the md5sums on the checklist should match those on the FTP server for each file. Once they do, "Run Files Report" on dashboard will indicate this with "File archived" or similar. If there are errors, you will see it immediately.

> Troubleshoot, if md5 checksums don't match:
> Check md5sums of data at source to check if downloading was the issue. Redo md5sum step. For further help, contact ENA via "Support" in Webin user area. "Internal errors" usually resolve without intervention.


That's it!! All done for the test service 🎉

---

Now log in to [`production service`](https://www.ebi.ac.uk/ena/submit/webin/login) and repeat all steps.

> Caution: Study and sample accessions will be different to test service

For other errors like "internal checking error", etc, give it a couple of days to resolve on the production service. Contact support if errors persist.

Helpful resources:

[`Resource 1 - ena-docs.readthedocs.io`](https://ena-docs.readthedocs.io/en/latest/submit/general-guide/interactive.html)

[`Resource 2 - biodiversitydata-se.github.io`](https://biodiversitydata-se.github.io/mol-data/ena-metabar.html)

---
