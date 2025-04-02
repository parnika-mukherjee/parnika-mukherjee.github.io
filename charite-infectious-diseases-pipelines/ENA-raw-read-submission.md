---
title: ENA Raw Read Submission
layout: default
---

# ENA Raw Read Submission Pipeline

This pipeline walks you through submitting raw sequencing reads to the **European Nucleotide Archive (ENA)**.

Supported read file formats are: CRAM, BAM, Single-end FASTQ, Paired-end FASTQ, HDF5 and FAST5

Read submission can be completed in 3 steps:
1. Sample metadata upload via web interface
2. Read upload via command line interface
3. Read metadata upload via web interface

[`-> Go to metadata collection`](./ENA-metadata-collection.md)

ALWAYS complete a [`test version`](https://wwwdev.ebi.ac.uk/ena/submit/webin/login) first and then repeat the steps for the [`production version`](https://www.ebi.ac.uk/ena/submit/webin/login)

## 📤 Uploading data to ENA Webin Submissions Portal

1. Register user on [`Webin Submissions Portal`](https://www.ebi.ac.uk/ena/submit/webin/accountInfo). Center name example: MDC/BIH Genomics Facility
2. Register study on the test service. Release date can be pushed back or forward. Abstract and description can be added later
3. After this, study acession will become available in Studies Report. It starts with "PRJEB". Save it for later use
   (3 lines on top left part of the screen opens the dashboard for navigation)
4. Register samples -> Download spreadsheet. For human or mouse RNA-seq data, choose "Other checklists". Next, for human/mouse data, choose default checklist. Fill up ([`see here for help`](./ENA-metadata-collection.md)), go back to "Register samples" on dashboard and select Upload. Save assigned sample accession IDs from "Samples Report" for the read files checklist.
For environmental and organismal (host-associated) samples, check resource 2.
5. To fill out the read files checklist, we can follow Step 4 in resource 2.
   a. We first generate md5sum check to verify read file integrity after upload. In the folder with the read files, run in terminal:

      `for f in *fastq.gz; do md5 $f | awk '{ gsub(/\(|\)/,""); print $1"\t" $2 }'; done > md5sums.tsv`

      Modify this command based on file names. This creates a tab-separated file with the md5sums and the file names. It should look like this (or in the reverse order of the columns):

      | 3b078583e52381db7d88abf7912b76c1 | i712_0001_CGGGAACCCGCA_i512A_0001_GTCTTTGGCCCT_R1.fastq.gz |
      | de91c8fc0d76dbfe05a45e7431109c97 | i712_0002_AAACGTTCATCC_i512A_0002_TTAGTAACTGGG_R1.fastq.gz |                                                   

      
   <span style="color: grey">Troubleshoot:
      If the correct info is not on the tsv file, print out the output of 
      
      `md5sum i712_0031_AAAATCCCAGTT_i512A_0031_AACGTTTAGGGG_R1.fastq.gz | awk '{ gsub(/\(|\)/,""); print $1"\t" $2 }'`
      
      with your own read file name. Check by changing 1 and 2 to 3 and 4 in the command what gives out one such row as an output. 
      
      This works for Mac and Linux. For Windows, check online for an easy method (for example, [`see this`](https://stackoverflow.com/questions/41838664/md5-hash-of-files-in-a-windows-folder))
   </span>
      
   b. Next, time to upload the read files to the ftp server of ENA, preferrably remotely, as it can take a long time.
      
      ```
      ### Connect to FTP server [replace Xs, and provide password when prompted]
      lftp webin2.ebi.ac.uk -u Webin-XXXXX
      ### Expected response: lftp Webin-XXXXX@webin2.ebi.ac.uk:~>
      
      ### Transfer your read files
      mput ~/your-read-file-dir/*.fastq.gz
      ### Expected response: ... Total x files transferred
      
      ### Disconnect from server
      bye
      ```
      
      This works for Mac and Linux. [`Example on Windows.`](https://unihost.com/blog/how-to-connect-to-ftp-server/)

8. Last step, to upload the read files checklist along with the md5sum for each file, go to Dashboard -> Submit Reads -> Select download option based on file format -> fill up ([`see here for help`](./ENA-metadata-collection.md)) -> upload.

Here, it is critical that the md5sums on the checklist should match those on the FTP server for each file. Once they do, "Run Files Report" on dashboard will indicate this with "File archived" or similar. If there are errors, you will see it immediately.

<span style="color: grey">Troubleshoot, if mdsums don't match:
Check md5sums of data at source to check if downloading was the issue. Redo md5sum step. For further help, ontact ENA via "Support" in Webin user area. "Internal errors" usually resolve without intervention.
</span>

That's it!! All done :tada:

Now log in to [`production service`](https://www.ebi.ac.uk/ena/submit/webin/login) and repeat all steps.
<span style="color: red">Caution</span>: Study and sample accessions will be different to test service


For other errors like "internal checking error", etc, give it a couple of days to resolve on the production service. Contact support if errors persist.

Helpful resources:
[`Resource 1 - ena-docs.readthedocs.io`](https://ena-docs.readthedocs.io/en/latest/submit/general-guide/interactive.html)
[`Resource 2 - biodiversitydata-se.github.io`](https://biodiversitydata-se.github.io/mol-data/ena-metabar.html)

---
