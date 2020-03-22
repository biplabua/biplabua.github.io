
I am a cell biologist; I perform experiments in a laboratory to answer scientific questions. Due to corona virus outbreak our laboratory has been closed, so I am spending all my time at home. I have decided to write some tutorials for bioinformatics data analysis, so that I can go back to these tutorials whenever I will need. These tutorials might be useful for other biologists as well. If you have a Mac computer you can search for terminal in your computer, when you open the terminal, a black screen will appear where we can write command to perform task by computer and computer will give back results. If you are using windows machine, you can google "how to use command line in windows" I think will be able to figure it out. 

If you have terminal open in your computer, you are using our computer from terminal. First we are going to see how to navigate around different folders/directories in our computer. First thing we would like to check is that, where we are in our computer, to get your location at your computer you can type the command 'pwd' your computer will give back your location at the computer. The location you get after opening the terminal is your 'home directory', please remember this term you might need it in future.

```
pwd
```
output

```
/Users/biplab
```

After starting terminal and entering 'pwd' command I get the path to the home directory, which is my working directory when you open the terminal. At a given time your location in the computer is called current/working directory. 'pwd' means 'print working directory'. Now what is path? Folders or directory structure in our computer has a heigharchical starting with the 'root directory'. The output from 'pwd' command '/Users/biplab' the '/' at beginng denotes the root directory. 

Now we would like check, what are the files and directory inside the home directory. We can check that by the command 'ls'

```
ls
```
output
```
Applications			Movies
Desktop				Music
Documents			Pictures
Downloads			Public
Dropbox (Partners HealthCare)	opt
Library
```

Output from 'ls' command gives name of the directories and files in my working directory. Here I can see I have Application, Desktop and Documents directories

We can go to any directory we want let say, we would like to go to Documents directory. In order to change the directory, we can use the command 'cd' which means 'change directory'. So far, we typed command but did not give any input to the command. This time we need to give input to the 'cd' command, the input to the command called 'argument' remember the term arguments. Argument should be separated by space. Argument to the 'cd' command is the name or path to the directory where we would like to go. Let's say I would like to go to Documents directory then I need to put 'Documents' with a space after cd. If you do not put any argument after cd command, you will go back to your home directory.
```
cd Documents
```
This command will not give back anything if the directory name or path is correct. If you give an incorrect name in the argument you will get an error message saying 'no such file or directory:' Above command will change my working directry to Documents. Again, you can check path to working directory by 'pwd' command. You use 'ls' command to check what are files or directories in your current location. 

Now I am at Documents directory, I can check what is in documents directory by ls command. 
```
ls
```
output
```
AB.pdf			Presentation		Tutorial
ACMB.pdf		ResearchArticles	Writing
MATLAB			ResearchData		megacc
MEGA X			Scripts
```
Let say I would like to go to ResearchData directory, I can again use cd command and name of the directory to go to ResearchData directory. I am in ResearchData directory, but I would like to go one directory up, which is Documents directory. In this case if you put cd Documents, it will give an error. Instead of Documents argument you need to put '..' which will take you to directory that is one step back that Documents directory.

```
cd ..
```

Now we are able to move around our computer's directories. In my Documents directory I have two pdf files, which I would to copy to Presentation directory. I can use 'cp' command for copying files or directory. You need to give two argument for 'cp' command, one is the file name or path to the file and directory or path to the directory where you would like to copy the file. 
```
cp AB.pdf Tutorial
```
Now we would like to change name of the file AB.pdf to bioinformatics.pdf we can use 'mv' command to change file name or move a file from one directory to another. 
```
mv AB.pdf bioinformatics.pdf
```
Next thing is about deleting file from the computer. We can use 'rm' command to remove file from the computer.
```
rm AB.pdf
```

I have lamina.bd file in Tutorial folder I can check content of the file by 'cat' command. 'cat' command will print content of the file on the screen.
```
cat lamina.bed
```
If the file is very big it is good idea to use 'less' command to look at the content of the file. 
```
less lamina.bed
```
You can press enter to see more content of the file. Press 'q' to go back to your command line again. 

Most of the time I use 'head' command to check first few lines of the file and 'tail' command to check last few line of the file. 
```
head lamina.bed
```
output
```
chrom	start	end	value
chr1	11323785	11617177	0.86217008797654
chr1	12645605	13926923	0.934891485809683
chr1	14750216	15119039	0.945945945945946
chr1	18102157	19080189	0.895174708818636
chr1	29491029	30934636	0.892526250772082
chr1	33716472	35395979	0.911901081916538
chr1	36712462	37685238	0.95655951346655
chr1	37838094	38031209	0.944206008583691
chr1	38272060	39078902	0.940932642487047
```

```
tail lamina.bed
``` 
output

```
chrX	135187116	135597436	0.940133037694013
chrX	135860243	138648904	0.888570404872805
chrX	138846031	148357359	0.83263937080731
chrX	148454624	148844607	0.784702549575071
chrX	153719866	153904495	0.772413793103448
chrY	2940166	7172793	0.808911201757138
chrY	7880008	13098461	0.79400260756193
chrY	13556427	13843364	0.892655367231638
chrY	14113371	15137286	0.93640897755611
chrY	15475619	19472504	0.813842482100239
```
Let do something more useful. I would like to know how many lines in lamina.bed. I can use 'wc' command with the option '-l' to count number of lines in the file. 
```
wc -l lamina.bed 
```
```
    1345 lamina.bed
```
 The lamina.bed file has 1345 lines. 

Sometimes we need specific column of the data file. We can use 'cut' command with '-f' option to select specific column from the data file. For '-f' option we need to provide column number that we would like to select.
```
cut -f 1,2 lamina.bed
```
This command will output first and second column of lamina.bed file. Sometime columns are separated by comma instead of space in that case 'cut' command has an option to input how the columns are separated. I have a comma separated file with four column. For that file I need to use -d ","
```
cut -d "," -f 1,2 lamin_head.bed
```
If we need to sort data based on data in one column we can use 'sort' command with 'k' option to sort data. 

```
sort -k2n lamina.bed 
```
output
```
chrom	start	end	value
chr20	11619	194068	0.980891719745223
chr8	696699	1664048	0.736240913811007
chr9	808574	2755227	0.904992729035385
chr18	857086	2083983	0.93071000855432
chr10	1193532	3050735	0.827242524916944
chr20	1406160	1690748	0.96989966555184
chr5	1715774	5463587	0.817772511848341
chr2	1829412	3344344	0.865861027190332
chr20	1876704	2021710	0.951351351351351
chr8	1971125	6247858	0.872897196261682
```
In the above commend 'k2n' means consider column 2 as number. We can see that output are sorted based number in column 2.

One advantage of command line is that you can redirect output from one command to another command by using pipe character '|'. In first column of the lamina.bed file contain chromosome name; we can select first column by 'cut' command then redirect to uniq command to see what are the unique chromosome in that file.

```
cut -f 1 lamina.bed | uniq
```

So far we are printing all of our output on the screen, you can redirect output to a file by using '>'. Let say we would like to redirect output from above command to a file name called chrome_name.txt.

```
cut -f 1 lamina.bed | uniq > chrome_name.txt
```
Sometimes we need to replace a specific character from a file with another character. For example, lamina_head.bed file is comma separated, now I would like to replace comma with space. We can use 'tr' command to replace comma by space. 1st argument for 'tr' command is the pattern we would like to replace, and second argument is the character that we would like to replace with. In our case, 1st argument is "," second argument is space which is given inside quote " ". 'tr' commend cannot operate on file directly so I print content of by file by 'cat' then redirect to 'tr' command.

```
cat lamin_head.bed | tr "," " " 
```

Wild card

A lot of time I use wild card character, which act as a place holder for any one or more character. Most of the time I use star * wildcard.
\*.txt means any one or more character before ".txt" similarly abc\* means any one or more character after "abc". Let see one example of using wild card. In my working directory I have a lot of different types of files such as pdf, doc, jpg, fasta files. I only want list of file that are pdf, here I can use wild \*.pdf to print list of files that are pdf.

```
ls *.pdf
```

```
AB.pdf		ACMB.pdf
```

Bioinformatic analysis involve downloading data from web. We can use 'wget' or 'curl' command to download data from website. 'wget' or 'curl' take web link of the file as an argument. 

```
wget https://downloads.yeastgenome.org/sequence/S288C_reference/genome_releases/S288C_reference_genome_R63-1-1_20100105.tgz
```
This will download S288C_reference_genome_R63-1-1_20100105.tgz file in your working directory. This is a genome sequence file from Saccharomyces Genome Database. 

Files for genomic data is very big, so to reduce size of the file is compressed as gzip file. The file we downloaded from SGD website is a 'tgz' file. One of the way compress the file using gzip. File name end with .gz that the file compressed by gzip and you need to use 'gunzip' command to decompress .gz file. Sometimes multiple files are archived and compressed together to a single file called 'tarball' and the file name has extension of '.tgz' or 'tar.gz'. This file we downloaded is a tarball file compressed with gzip. This file can be extracted by following command.

```
tar -zxvf S288C_reference_genome_R63-1-1_20100105.tgz
```

Above command will decompress the file we downloaded, and you will see a directory name 'S288C_reference_genome_R63-1-1_20100105'. You can go into that directory and check files. 

Another command I use a lot is 'grep' command. You can look for pattern is file using grep command and grep command will output the line that match the pattern. 'S288C_reference_genome_R63-1-1_20100105' directory contain multi fasta files. We know that name of sequence in a fasta file start with '>'. If we would like to extract name of sequences in multifasta file, we can grep command with '>' as pattern and name of the file as an argument. 
```
grep '>' S288C_reference_sequence_R63-1-1_20100105.fsa
```
This will print seqence names in S288C_reference_sequence_R63-1-1_20100105.fsa fasta file on the screen. Sometimes I need to print line that does not contain the pattern, in that case I 'grep' with option '-v'.
```
grep -v '>' S288C_reference_sequence_R63-1-1_20100105.fsa
```

This will print sequences in the file without the name. 

So far we were working with single files, in reality I need to pass a commands to mutlple files and stored the output in multiple file. You can write a for loop to perform this kind of work. Let write a simple for loop in shell. "S288C_reference_sequence_R63-1-1_20100105" directory has multiple fasta file we would like to print head of every files. Below is the for loop to do that. 

```
for i in `ls *.fasta` do
head $i done
```
I use simillar for loop to perform a lot of tasks where multiple files need to be processed by same command. 

This is a very simple command line applications, you can do many more in command line. Most commands I talked about has various options you google about every command to find more. This I hope will help you get started with command line. 


