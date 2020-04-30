## Downlaod raw data for analysis
```
VAR=$(tail -n +2 SraRunTable.txt | cut -d ',' -f 1)

for i in ${VAR}
	do
				fastq-dump ${i}
	done

```
## Run fastqc

## Align to the genome
```
VAR=$(tail -n +2 ../meta_data/SraRunTable.txt | cut -d ',' -f 1)

for i in ${VAR}
	do
		
		bowtie2 -p 8 -q --local -x ../reference/mm9 -U ../raw_data/${i}.fastq -S ../results/bowtie2/${i}.sam
	done
```
## Convert sam file to bam file
```
VAR=$(tail -n +2 ../meta_data/SraRunTable.txt | cut -d ',' -f 1)

for i in ${VAR}
	do
		
		samtools view -h -S -b ../results/bowtie2/${i}.sam -o ../results/bowtie2/${i}.bam
		#echo ${i}
	done
```
## Sort bam file
```
VAR=$(tail -n +2 ../meta_data/SraRunTable.txt | cut -d ',' -f 1)

for i in ${VAR}
	do
		
		samtools sort -t 2 -o ../results/bowtie2/${i}_sorted.bam ../results/bowtie2/${i}.bam
		#echo ${i}
	done
```
## Remove duplicate by samtools markdup 

```
VAR=$(tail -n +2 ../meta_data/SraRunTable.txt | cut -d ',' -f 1)

for i in ${VAR}
	do
		
		samtools markdup -r ../results/bowtie2/${i}_sorted.bam ../results/bowtie2/${i}_unique.bam
		#echo ${i}
	done
```

## Filter reads with low mapping quality

```
VAR=$(tail -n +2 ../meta_data/SraRunTable.txt | cut -d ',' -f 1)

for i in ${VAR}
	do
		
		samtools view -q 40 ../results/bowtie2/${i}_unique.bam -o ../results/bowtie2/${i}_mapq40.bam
		#echo ${i}
	done
```

## Merge bamfile

```
samtools merge -r Oct4_dox.bam SRR3997985_mapq40.bam SRR3997986_mapq40.bam SRR3997987_mapq40.bam
samtools merge -r Smad3_dox.bam SRR3997988_mapq40.bam SRR3997989_mapq40.bam SRR3997990_mapq40.bam
samtools merge -r Smad3.bam SRR3997993_mapq40.bam SRR3997994_mapq40.bam SRR3997995_mapq40.bam
samtools merge -r InputDox.bam SRR3997991_mapq40.bam SRR3997992_mapq40.bam
```

## Remove blacklisted region

## Bamcoverage
```
bamCompare --operation reciprocal_ratio --effectiveGenomeSize 2150570000 -b1 Oct4_dox.bam -b2 InputDox.bam -o Oct4Dox.bw
```

## computeMatrix

## plotHeatmap