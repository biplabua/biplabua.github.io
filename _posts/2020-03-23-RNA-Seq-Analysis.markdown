# Creat necessary folders/directories
```
mkdir RNA_Seq_Analysis
cd RNA_Seq_Analysis
mkdir raw_data
mkdir scripts
mkdir bam_files
mkdir count_file
mkdir mata_data
```
# Download raw data from SRA
Go to following link and download accession list and metadata file.
[a link](https://www.ncbi.nlm.nih.gov/sra?linkname=bioproject_sra_all&from_uid=272684)
```
cd raw_data
cat SRR_Acc_List.txt | xargs fastq-dump
```


# Check quality of the raw data

# Mapping raw data to the genome

# Counting number of reads mapped to each feature

# Differential gene expression analysis