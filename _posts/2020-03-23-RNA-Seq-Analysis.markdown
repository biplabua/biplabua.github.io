# Creat necessary folders/directories
```
mkdir RNA_Seq_Analysis
cd RNA_Seq_Analysis
mkdir raw_data
mkdir fastqc_out
mkdir scripts
mkdir bam_files
mkdir count_file
mkdir mata_data
```
# Download raw data from SRA
Go to following link and download accession list and metadata file.
[Accession list download link](https://www.ncbi.nlm.nih.gov/sra?linkname=bioproject_sra_all&from_uid=272684)

“click on 'Send to'(top right corner)”  Select “Run Selector”  then click on 'go' Select above mentioned run then by clicking Metadata and Accession List we will get metadata and accession list file which we will use for our analysis. Accession list file name is SRR_Acc_List.txt and metadata file name is SraRunTable.txt.
Move the acession list file to the raw data directory and SraRunTable.txt file to the metadata directory

```
cd raw_data
cat SRR_Acc_List.txt | xargs fastq-dump
```

# Check quality of the raw data
We will use fastqc to check quality of raw data that we downloaded from sra database. The fastqc will generate html report of every file, I am not going to explain everything about those report but you can check this link to read about inpretation of fastqc report. 

```
fastqc -o ~/RNA_Seq_Analysis/fastqcout `ls *fastq`
```

# Mapping raw data to the genome

Data we downloaded is RNA sequencing data from yeast strain between two different condition. In order to map this data to yeast genome I need to download yeast genome. I can download yeast genome using following command. 

In order to consider sliced site I need to generate a file containing spliced site using extract_splice_sites.py script, which part of hisat2 software. Please download the hisat2
```
wget ftp://ftp.ccb.jhu.edu/pub/infphilo/hisat2/downloads/hisat2-2.1.0-Linux_x86_64.zip
unzip hisat2-2.1.0-Linux_x86_64.zip
```
```
wget ftp://ftp.ensembl.org/pub/release-99/fasta/saccharomyces_cerevisiae/dna/Saccharomyces_cerevisiae.R64-1-1.dna_sm.toplevel.fa.gz
gunzip Saccharomyces_cerevisiae.R64-1-1.dna_sm.toplevel.fa.gz
```

```
wget ftp://ftp.ensembl.org/pub/release-99/gtf/saccharomyces_cerevisiae/Saccharomyces_cerevisiae.R64-1-1.99.gtf.gz
gunizp Saccharomyces_cerevisiae.R64-1-1.99.gtf.gz
```
```
python ./scripts/hisat2-2.1.0/hisat2_extract_splice_sites.py ./annotation/Saccharomyces_cerevisiae.R64-1-1.99.gtf > ./annotation/splicesites.txt
```

```
for fqfile in `ls *.fastq | sed 's/.fastq//g' | sort -u`
do
hisat2 -x ~/Documents/Tutorial/RNA_Seq_Analysis/annotation/Saccharomyces_cerevisiae.R64-1-1.dna_sm.toplevel --known-splicesite-infile ~/Documents/Tutorial/RNA_Seq_Analysis/annotation/splicesites.txt $fqfile.fastq | samtools view -Sb > ~/Documents/Tutorial/RNA_Seq_Analysis/bam_files/$fqfile.bam
done
```

```
for bam_file in `ls *bam | sed 's/.bam//g' | sort -u`;
do
samtools sort $bam_file.bam > $bam_file.sorted.bam
done
```
```
for bam_file in `ls *sorted.bam`;
do
samtools index $bam_file 
done
```
# Counting number of reads mapped to each feature
```
for bam_file in `ls *bam.sorted`;
do
featureCounts -s 2 -t exon -g gene_id -a ~/Documents/Tutorial/RNA_Seq_Analysis/annotation/Saccharomyces_cerevisiae.R64-1-1.99.gtf -o ~/Documents/Tutorial/RNA_Seq_Analysis/counts/$bam_file ~/Documents/Tutorial/RNA_Seq_Analysis/bam_files/$bam_file
done
```	
