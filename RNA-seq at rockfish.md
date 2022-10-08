


# 0. Set-up
### Directory
I recommend you to organize a directory tree setup similar to that shown below as it is the best practice to use my script in the class.  
Of course, you can have your own structure for your project.  

taeyoung  
|── Software  
|── Genome  
|── Results  
|── Script  
|── 1.Fastq  
|── 2.Alignment  
└── 3.Count  

### Fastq files
$ cp /home/thwang12/ME-440/taeyoung/1.Fastq/*[0-9].fastq.gz YOUR_FASTQ_DIRECOTRY

# 1. Fastqc
We will use an interactive session to use compute nodes at rockfish. An interactive session is useful to perform small tasks and test workflows.  

Request 3 cores (-n 4) and 3GB RAM (-m 3G) and 1 hr working time (-t 1hr).

$ interact -n 4 -m 3g -t 01:00:00

Now you are at the compute nodes. The promot should be seen as [thwang12@c714_teyoung]$, not a log-in node like [thwang12@login01 taeyoung]$.  

$ cd 1.Fastq  
$ module load fastqc  
$ fastqc --help  
$ fastqc -t 3 *.fastq.gz  
$ exit  

**Note that 3 fastq files are processed at a time.**

# (optional) Trimming adapters
You can still use an interaction mode, but this time, we will submit a job to use computational nodes.

First, check the batch script and modify it necessarily.
$ nano ./Script/cutadapt.sbatch
Then, go to the folder and submit a job.  
$ cd 1.Fastq  
$ sbatch cutadapt.sbatch

# 2. Alignment

First, check the batch script and modify it necessarily.
$ nano ./Script/star_align.sbatch
Then, go to the folder and submit a job.  
$ cd 2.Alignment  
$ sbatch star_align.sbatch

# 3. Counting

First, check the batch script and modify it necessarily.
$ nano ./Script/featureCounts.sbatch
Then, go to the folder and submit a job.  
$ cd 3.Count  
$ sbatch featureCounts.sbatch

# 4. Result
In this step, we will use a R script to save count results in a single Rda file.  
Use an interaction mode to run R script line by line or use an Rstudio session through portoal.rockfish.edu  

### Interaction mode

$ interact -n 1 -m 3g -t 01:00:00

$ module load R  
Then run makeCountTable.R line by line. 

### Rstudio on portal.rockfish.edu
Run makeCountTable.R line by line. 

# 5. Differential expression analysis
I usually download the rda file that has just generated to my mac/PC and analyze it locally to avoid connection issue. You can also use Rstudio session on portal.rockfish.edu.


