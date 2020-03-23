
# Installation of SRA toolkit

Now a days all most of the labs are performing RNA-Seq experiments. If an article has RNA-Seq data, they need to make it available in SRA repository for anybody to download and analyze it. In order to download data from SRA database as fastq format you need to use SRA toolkit software. 

How to install SRA toolkit?
Download SRA toolkit using wget command.

```
wget https://ftp-trace.ncbi.nlm.nih.gov/sra/sdk/2.9.6-1/sratoolkit.2.9.6-1-mac64.tar.gz
```

Unzip the tarball 
```
tar -xvzf sratoolkit.2.9.6-1-mac64.tar.gz
```

go to bin directory inside ratoolkit.2.9.6-1-mac64. 

```
cd ratoolkit.2.9.6-1-mac64/bin
```
get the path to bin directory..

```
pwd
```

copy the output.. 

```
export "PATH=$PATH:put the path here" >> ~/.zshrc
```

or 

```
export "PATH=$PATH:put the path here" >> ~/.bash_profile
```

Open a new terminal type 

```
fastq-dump -h
```

Should output the help manual

# Installation of Bioinformatic Softwares using Bioconda
As you have seen above that installation of bioinformatic software can be little complicated, in order to reduce complication of software installation you can install bioconda, package management system in your computer. Bioconda contains a large number of bioinformatics software you can easily install any one of those by using 'conda install' command.

For mac user you can install conda by command below:
```
curl -O https://repo.anaconda.com/miniconda/Miniconda3-latest-MacOSX-x86_64.sh
```
```
sh Miniconda3-latest-MacOSX-x86_64.sh
```
After installing conda, you need to add the bioconda channels and dependency by running commands below in order:
```
conda config --add channels defaults
conda config --add channels bioconda
conda config --add channels conda-forge
```

Now we will install few bioinformatic softwares using bioconda. 
Once we get next generation sequencing data from the sequencing facility, first we need to check quality of data by using the software fastqc. Then we might need to pre-process our raw data using, we can do this by using trimmomatic software. Then we need to align reads to the reference genome if reference genome is available. I usually do the align reads to the reference genome by the software hisat2. We will install all three by following commands.

```
conda install -c bioconda fastqc
conda install -c bioconda trimmomatic
conda install -c bioconda hisat2
```
Now you have conda installed in your computer, if you were not able to sratoolkit yet, you can use conda install for installation of sratoolkit.
```
conda install -c bioconda sra-tools
```
From now I will use conda install if bioinformatic software is available in bioconda package manager. 

# How to download fastq files from SRA database.
Once you install sra toolkit in your computer downloading raw fastq data from the sra database become very simple. 

Find out SRR numbers for the raw data, then use fastq-dump command to download data to local computer. For example, I got SRR number for RNA-Seq of yeast strain, which is SRR1761158

```
fastq-dump SRR1761158
```
Above commend will download data in fastq format which is SRR1761158.fastq. 

If the data in pair-end format, you need to use --split-files option of fastq-dump. SRR6145788 is a pair-end RNA-Seq data which I can download by following command.

```
fastq-dump --split-files SRR6145788
```
Above command will download two files with SRR6145788_1.fastq and SRR6145788_2.fastq in your current directory.

This fastq file will not tell you anything about the sample information. You can use run selector to download information about the sample. Please navigate around the SRA database, it will help you to understand how data are stored in SRA database. 




