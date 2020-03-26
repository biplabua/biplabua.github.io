Bioinformatics analysis involved in manipulating varius file formats. Manipulation of files require a solid understanding of different file formats. Here I will try to explain what what different type file formats. 

# FASTA

Text file that store either nucleotide or amino acid sequence of DNA or proteins respectively. 

Each record in a fasta file has two parts:
Line 1: '>' followed by sequene ID.
Line 2: One or more line of nucleotide or amino acid sequences.

For example:

```
>gi|425153|gb|L26238.1|MUSHOME Mus domesticus (lbx) homeodomain mRNA, partial cds 
CCATTTCAACAAGTACCTGACCAGGGCTCGGCGAGTGGAAGTTGCCGCTATTCTCGAGCTCAACGAAACT
CAAGTGAAAATT
```
Sequence ID: >gi|425153|gb|L26238.1|MUSHOME Mus domesticus (lbx) homeodomain mRNA, partial cds 
Sequence: CCATTTCAACAAGTACCTGACCAGGGCTCGGCGAGTGGAAGTTGCCGCTATTCTCGAGCTCAACGAAACTCAAGTGAAAATT

# FASTQ File

FASTQ files contain nucleotide sequence with quality score associated with each nucleotide. Each record in FASTQ file consist of four lines. 

Line 1: Starts with "@" followed sequence ID
Line 2: Sequence data
Line 3: Start with "+"
Line 4: Quality score for each base in the Line 2, score is encoded by the ASCII character. 

Example fastq file
```
@EAS139:136:FC706VJ:2:2104:15343:197393 1:Y:18:ATCACG
GATTTGGGGTTCAAAGCAGTATCGATCAAATAGTAAATCCATTTGTTCAACTCACAGTTT
+
!''*((((***+))%%%++)(%%%%).1***-+*''))**55CCF>>>>>>CCCCCCC65
```
```
Sequence ID: @EAS139:136:FC706VJ:2:2104:15343:197393 1:Y:18:ATCACG
Sequence: GATTTGGGGTTCAAAGCAGTATCGATCAAATAGTAAATCCATTTGTTCAACTCACAGTTT
Line 3: '+'
Quality score:!''*((((***+))%%%++)(%%%%).1***-+*''))**55CCF>>>>>>CCCCCCC65
```
Quality score means probability of an error in base calling. High score means low probability of error.

# GFF files
GFF file is nine column tab delimited file that describe information about each features in the genome. Each line in GFF file represents a feature in a genome such as gene, transcripts, exosome, promoter etc. 

Column 1: Chromosome name or ID.
Column 2: Program that generate the GFF file
Column 3: Feature type such as gene, exon and coding sequence
Column 4: Start position of feature in the chromosome
Column 5: End position of feature in the chromosome
Column 6: Score of the feature
Column 7: Strand +(forward) or -(reverse)
Column 8: frame denoted by one of the integers 0, 1, 2; base of nucleotide codon begins.
Column 9: Attributes of feature such as ID, Name, Alias, Parent, Target, Gap, Ontology term etc. Each attribute is separated by ";"

Example:

```
chrI	SGD	CDS	538	792	.	+	0	Parent=YAL068W-A_mRNA;Name=YAL068W-A_CDS;orf_classification=Dubious
```
Column 1: chrI - chromosome name
Column 2: SGD - GFF source of GFF file in this case yeast genome database (SGD)
Column 3: CDS - Feature type is coding sequence (CDS)
Column 4: 538 - Feature start at 538 position of chromosome
Column 5: 792 - Feature end at 792 position of the chromosome
Column 6: . Score for the feature
Column 7: + - which mean featue is in the forward strand
Column 8: 0 - Codon start at first base of the sequence
Column 9: Parent=YAL068W-A_mRNA;Name=YAL068W-A_CDS;orf_classification=Dubious 

# GTF file
First 8 columns are same as GFF file but 9th column has two different atrributes such as gene_id and transcript_id that are separated by ";"

# SAM File
Output from sequence alignment program that contain 11 column each line in the sam file alignment information about each read. Header lines that start with @
For example:
@HD - Header line
@SQ - Reference genome information
@RG - Read group information
@PG - Program information

```
HISEQ:496:C4KY7ACXX:8:1101:1606:2994    73      4       13740599        36      100M    *       0       0       ATCACAAAGAATATTCATCAATGCTTCACAAAACATTGGAAGGGGTAATAATGATGGAGACGTTTCCAAAAACAACCGTTGATGTTTTTCCATTGTTTCT    ;;?=?;=BDDCA:CEEE@4A?,AEB?A?9A?<+?::?CCCD1))08?BD4B?<BBD:C=)(5-;A7@AA=CC/=??(3>@5;;AD###############    MD:Z:32G10T45G5G4       NH:i:1  HI:i:1  NM:i:4  SM:i:36 XQ:i:40 X2:i:0  XO:Z:HU PG:Z:A
HISEQ:496:C4KY7ACXX:8:1101:1606:2994    133     *       0       0       *       4       13740599        0       ATACAATCGAAAATCATAGTTATTTATGCTCATTCATCGGAAGCTGGGGCAGACTGTTTCAGACAATTACCCATTATTTCTCGAACACTTGAACTAGCAT    (85@34?#############################################################################################    XO:Z:HU
```

Column 1: HISEQ:496:C4KY7ACXX:8:1101:1606:2994 - Query sequence ID
Column 2: 73 - Sam FLAG
Column 3: 3 - Reference sequence name is 3 that mean read align to chromosome 3
Column 4: 13740599 - 1 based 5' posistion in the chrosome where read align.
Column 5: 36 - Mapping quality
Column 6: 100M - CIGAR String 100M means 100 match
Column 7: * Ref. name of the mate read
Column 8: 0 Position of mate read
Column 9: 0 Observe template length
Column 10: Query sequence
Column 11: Quality score for the sequencee

Two important columns in SAM file are column 2 which is sam flag it is important that you understance meaning of sam FLAG. You input number in this column in this link and file what that FLAG means.
Another important column is column 6 which is a CIGAR string. Here is the explanation of CIGAR string. 

# BAM file
Binary format of SAM file is called bam file. 

















