Last updated 10. 2. 2023 

# Change file names for array jobs 
- You likely have to process multiple samples at the same time in the same way.<br>
  Use array jobs to process all of them simultaneously. <br>
  Below is an example where you can do fastqc for 30 files by specifying variable numbers with $LSB_JOBINDEX
  
```
#BSUB -J "job[1-30]" fastqc

fastqc ../S$LSB_JOBINDEX.fastq.gz
```

> Note: one can specify [1,3,25-30] to run S1.fastq.gz, S3.fastq.gz, S25.fastq.gz to S30.fastq.gz. <br>
> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; one can also use colon, such as [1-29:2] to run odd numbered files. <br>
> See this link for array jobs: [Job Arrays under LSF](https:///www.hpc.dtu.dk/?page_id=1434)

- You need to change file names for array job processing
> There may be easier way to automate this, but so far, I have been just manually changing names.

```
#!/bin/bash
#BSUB -J FNameConv

mv ../S01_S1_L001_R1_001.fastq.gz ../S1-R1.fastq.gz
mv ../S01_S1_L001_R2_001.fastq.gz ../S1-R2.fastq.gz
mv ../S02_S2_L001_R1_001.fastq.gz ../S2-R1.fastq.gz
mv ../S02_S2_L001_R2_001.fastq.gz ../S2-R2.fastq.gz
.
.
.
mv ../S29_S29_L001_R1_001.fastq.gz ../S29-R1.fastq.gz
mv ../S29_S29_L001_R2_001.fastq.gz ../S29-R2.fastq.gz
mv ../S30_S30_L001_R1_001.fastq.gz ../S30-R1.fastq.gz
mv ../S30_S30_L001_R2_001.fastq.gz ../S30-R2.fastq.gz
```
> Note: make sure 1) not making mistakes, 2) leaving a record for file name conversion.
> 
