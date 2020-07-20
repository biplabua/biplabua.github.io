```python
from itertools import groupby
import sys
class Bioseq(object):
    def __init__(self, id, seq):
        self.id = id
        self.seq = seq
        self.length = len(seq)
    def percent_bases(self):
        bases = {}
        for base in self.seq:
            if base not in bases:
                bases[base]=0
            bases[base] += 1
        for base in bases:
            bases[base] = bases[base]/self.length
        return bases
    def GC_Percent(self):
        return self.percent_bases()["G"] + self.percent_bases()["C"]
        
    
def read_fasta(file_path):
    with open(file_path, 'r') as fh:
        faiter = (x[1] for x in groupby(fh, lambda line: line[0] == ">"))
        for header in faiter:
            header = header.__next__()[1:].strip()
            seq = "".join(s.strip() for s in faiter.__next__())
            yield Bioseq(header, seq)
fa = read_fasta("/Users/biplab/L1E1_oligos.fasta")

c = 0
plat = []
latter = ['A', 'B', 'C', 'D', 'E', 'F', 'G', 'H']
for l in latter:
    for i in range(1, 13):
        plat.append(l + str(i))
        c += 1


```


```python
seq_id = []
sequence = []
c = 0
for f in fa:
    if "COL1A1" in f.id:
        c += 1
        seq_id.append("COL1A1_ENST00000225964.10_Probe{}".format(c))
        s = f.seq.split()
        for probe in s:
            if len(probe) == 30:
                sequence.append(probe + "A" + "readoutProbe")

```


```python
fa = read_fasta("/Users/biplab/oligos.fasta")
```


```python
seq_id_ASS1 = []
sequence_ASS1 = []  
plat_ass1 = plat[48:93]
c = 0
for f in fa:
    if "ASS1" in f.id:
        c += 1
        seq_id_ASS1.append("ASS1_ENST00000352480.10_Probe{}".format(c))
        s = f.seq.split()
        for probe in s:
            if len(probe) == 30:
                sequence_ASS1.append(probe + "A" + "AGGGTGTGTTTGTAAAGGGT")
```

    



```python
import pandas
df1 = pandas.DataFrame(data={"Well Position": plat[0:48], "Name": seq_id[0:48], "Sequence":sequence[0:48]})
df2 = pandas.DataFrame(data={"Well Position": plat[48:92], "Name": seq_id_ASS1, "Sequence":sequence_ASS1})
result = pandas.concat([df1,df2])
result.to_csv("COL1A1_ASS1_Oligo.csv", sep=',',index=False)
```


```python
print(len(sequence_ASS1))
print(len(plat[48:92]))
print(len(seq_id))
print(len(sequence))
print(result)
```
