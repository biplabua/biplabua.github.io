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

## Peak calling
macs2 callpeak -t ../results/bowtie2/SRR3997985_unique.bam -c ../results/bowtie2/InputDox.bam -f BAM -g mm --outdir ../macs2 -n Oct4_dox_R1 -q 0.001
macs2 callpeak -t ../results/bowtie2/SRR3997986_unique.bam -c ../results/bowtie2/InputDox.bam -f BAM -g mm --outdir ../macs2 -n Oct4_dox_R2 -q 0.001
macs2 callpeak -t ../results/bowtie2/SRR3997987_unique.bam -c ../results/bowtie2/InputDox.bam -f BAM -g mm --outdir ../macs2 -n Oct4_dox_R3 -q 0.001
macs2 callpeak -t ../results/bowtie2/SRR3997988_unique.bam -c ../results/bowtie2/InputDox.bam -f BAM -g mm --outdir ../macs2 -n Smad3_dox_R1 -q 0.001
macs2 callpeak -t ../results/bowtie2/SRR3997989_unique.bam -c ../results/bowtie2/InputDox.bam -f BAM -g mm --outdir ../macs2 -n Smad3_dox_R2 -q 0.001
macs2 callpeak -t ../results/bowtie2/SRR3997990_unique.bam -c ../results/bowtie2/InputDox.bam -f BAM -g mm --outdir ../macs2 -n Smad3_dox_R3 -q 0.001 
macs2 callpeak -t ../results/bowtie2/SRR3997991_unique.bam -c ../results/bowtie2/Input.bam -f BAM -g mm --outdir ../macs2 -n Smad3_R1 --broad -q 0.001
macs2 callpeak -t ../results/bowtie2/SRR3997992_unique.bam -c ../results/bowtie2/Input.bam -f BAM -g mm --outdir ../macs2 -n Smad3_R2 --broad -q 0.001
macs2 callpeak -t ../results/bowtie2/SRR3997993_unique.bam -c ../results/bowtie2/Input.bam -f BAM -g mm --outdir ../macs2 -n Smad3_R3 --broad -q 0.001 


## Bamcoverage
```
bamCompare --operation reciprocal_ratio --effectiveGenomeSize 2150570000 -b1 Oct4_dox.bam -b2 InputDox.bam -o Oct4Dox.bw
bamCompare --operation reciprocal_ratio --effectiveGenomeSize 2150570000 -b1 Smad3_dox.bam -b2 InputDox.bam -o Oct4Dox.bw
```

## computeMatrix

```
computeMatrix reference-point --referencePoint center --sortRegions descend -a 2000 -b 2000 -R Oct4_dox_R1_summits.bed -S ../results/bowtie2/Oct4Dox.bw -o Oct4Dox.mat
```

## plotHeatmap