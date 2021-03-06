# Practical 1: Introduction to genetic data 
# ANSWERS

> (1) When is `less –S {file}` a better command to use to have a quick look at a file?

less -S is useful for wide files as it does not wrap each line. 
Instead it only shows the top left corner of a file. 
For ped files with thousands of columns, this is a much better command than less (without -S) or head.


> (2) What do you think the 4 columns in a .map file are?

```
[user@newblue2 data]$ head chr22.map
22      rs5747968       0       17067504
22      rs5747999       0       17075353
22      rs2096537       0       17094749
22      rs9604959       0       17099107
....
```

Chromosome, SNP rsID, unused (cM), base position

> (3) How many variants are there in this dataset?

```
[user@newblue2 data]$ wc -l chr22.map
7092 chr22.map
```

7092

> (4) How many individuals are there in this dataset?

```
[user@newblue2 data]$ wc -l chr22.ped
8237 chr22.ped
```

8237

> (5) How many columns are there in the .ped file before the genetic data columns? What might these be?

```
[user@newblue2 data]$ less -S chr22.ped
id1 id1 0 0 2 -9 T T A A.......
id2 id2 0 0 2 -9 G T C A.......
id3 id3 0 0 2 -9 T T C A ......
.....
```

6: Family ID, Individual ID, Mother ID, Father ID, sex, phenotype

> (6) What are the 2 possible alleles for the first SNP in the dataset? What is the name of this SNP?

```
[user@newblue2 data]$ less -S chr22.ped
id1 id1 0 0 2 -9 T T.....
id2 id2 0 0 2 -9 G T.....
....
[user@newblue2 data]$ head chr22.map
22      rs5747968       0       17067504
....
```

T/G rs5747968

> (7) Search for SNP rs7288409. What is the bp position for this SNP?

```
[user@newblue2 data]$ grep rs7288409 chr22.map
22      rs7288409       0       18542311
```

18542311

> (8) What is the difference between a .bim and a .map file?

```
[user@newblue2 data]$ head chr22.map
22      rs5747968       0       17067504
22      rs5747999       0       17075353
22      rs2096537       0       17094749
22      rs9604959       0       17099107
22      rs2845379       0       17202602
22      rs17433377      0       17228796
22      rs5748623       0       17265124
22      rs9605146       0       17265194
22      rs4819535       0       17278762
22      rs5748648       0       17280822
[user@newblue2 data]$ head chr22.bim
22      rs5747968       0       17067504        G       T
22      rs5747999       0       17075353        C       A
22      rs2096537       0       17094749        A       C
22      rs9604959       0       17099107        T       C
22      rs2845379       0       17202602        T       C
22      rs17433377      0       17228796        A       G
22      rs5748623       0       17265124        A       C
22      rs9605146       0       17265194        A       G
22      rs4819535       0       17278762        C       T
22      rs5748648       0       17280822        A       G
```

.bim files have extra columns of the two alleles to allow the data to be stored more efficiently.

> (9) What is the difference between a .fam and a .ped file?

```
[user@newblue2 data]$ less -S chr22.ped
id1 id1 0 0 2 -9 T T A A C C C C.....
id2 id2 0 0 2 -9 G T C A C C T C.....
.....
[user@newblue2 data]$ head chr22.fam
id1 id1 0 0 2 -9
id2 id2 0 0 2 -9
id3 id3 0 0 2 -9
id4 id4 0 0 1 -9
id5 id5 0 0 1 -9
id6 id6 0 0 2 -9
```

A .fam file contains only the first 6 columns of a .ped file. 


> (10) Above, you listed the possible alleles for rs5747968 (hopefully as G & T). If we were to represent the data as dosage of G, what would the dosages be for the first 8 people in the dataset?

0,1,0,0,0,0,1,2

This should agreee with what you see when you run this command:

```
[user@newblue2 data]$ less -S chr22_dosage.txt
FID IID PAT MAT SEX PHENOTYPE rs5747968_G........
id1 id1 0 0 2 -9 0 .....
id2 id2 0 0 2 -9 1 .....
id3 id3 0 0 2 -9 0 .....
id4 id4 0 0 1 -9 0 .....
id5 id5 0 0 1 -9 0 .....
id6 id6 0 0 2 -9 0 .....
id7 id7 0 0 2 -9 1 .....
id8 id8 0 0 1 -9 2 .....
```


# EXTRA - SNPTEST format questions
> (11) What format are the genotypes displayed in?

Genotype probabiities. 3 colums per SNP per individual. Corresponsing to the probability that individual has A1A1, A1A2 and A2A2 genotype at that position. The 3 probabilities sum to 1.

> (12) How can you tell which individual the first three columns of data belong to?

There are no individual IDs in the genotype file (as there are in Plink), so you need to refer to the corresponding .sample file. **NB. It is therefore crucial that all individuals with genotpye data are listed in this file, and this file is kept in the right order. This becomes very important when creating a .sample file with your own phenotype data. You must always ensure the number and order of rows in this file remains unchanged!**


