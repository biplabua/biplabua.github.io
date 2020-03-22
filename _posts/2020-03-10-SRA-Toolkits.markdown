
#Installation of SRA toolkit

How to downloads RNA Seq data from SRA database?
Now a days all most all labs are performing RNA-Seq experiments. If an article has RNA-Seq data the labs need to make data available to SRA repository for anybody to download analyze it. In order to download data from SRA database as fastq formate you need to use SRA toolkit software. 

How to install SRA toolkit?
Download SRA toolkit using wget command.

```
wget https://ftp-trace.ncbi.nlm.nih.gov/sra/sdk/2.9.6-1/sratoolkit.2.9.6-1-mac64.tar.gz
```

Unizp the tarball 
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

#Dowload fastq file from SRA database.



