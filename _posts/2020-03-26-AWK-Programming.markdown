Awk read every line in file one by one and look for the line that match the pattern. Pattern can be regular expression enclosed with //. It could be boolean expression, ! denotes the negates the match. 
After match action is performed on every line that matches pattern. If action is not provided program print all line or pattern is not provided action is performed on every line. 
The record separator is new line
RS: Record separator
NR: Number of the variable in current record
FS: Each record split into field FS is field separator. The default field separator is white space.
$0: The entire line, only field variable start with $.

```
awk '{print $0}' splicesites.txt
```
Print all line in the file

```
awk '{print $1,$2}' splicesites.txt
```
Print first two column of the file

You can print number of field in each record by NF
```
awk '{print NF, $0}' splicesites.txt
```
Print third to last field
```
awk '{print $(NF-2) }' splicesites.txt
```
You can do computation on field value
```
awk '{print $1, $3-$2}' splicesites.txt
```

You can print number of line
```
awk '{print NR, $0}' splicesites.txt
```

You add text in the output
```
awk '{print "Chromosome:",$1,"Start:"$2,"End:"$3, "Strand:"$4}' splicesites.txt
```

You can use use printf function for formating string
```
awk '{printf("Chromosome: %s Start: %d End: %d Strand: %s\n", $1,$2,$3,$4)}' splicesites.txt
```
We have a GTF file, I would like to choose features that are gene from the gtf file. We can use text content by awk.

```
awk '{if($3=="gene") print $0}' Saccharomyces_cerevisiae.R64-1-1.99.gtf
```
Lets choose features that are transcript or exon
```
awk '{if($3=="transcript" || $3=="exon") print $0}' Saccharomyces_cerevisiae.R64-1-1.99.gtf
```

Let say we would lik to choose line with pattern "XVI" in file splicesites.txt

```
awk '/XVI/{print$0}' splicesites.txt
```
Default field separator in awk is space, but we can change it using -F option. Below is code for printing first field of a comma separated file.

```
awk -F, '/CA/{print $1}' list.txt
```
Lets print each field in a separate line
```
awk -F, '/CA/{print $1; print $2; print $3}' list.txt
```
Lets use for loop to print first three field of the file splicesites.txt.
```
awk '{for (i = 1; i <= 3; i++) print $i}' splicesites.txt
```




