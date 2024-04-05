# MicroHaplotypes
Phylogenomics through MicroHaplotype Analysis

# 1. Create MicroHaplotype fasta files:
```bash
g=`awk '$3 ~ /sequence2/ {print length($4)}' ../CposaOnlyHaplotypes.complete.txt | head -1`; for f in $(seq 1 50 $g); do awk -v var=$f '$3 ~ /sequence2/ {print ">" $1 "\n" substr($4, var, 50)}' ../CposaOnlyHaplotypes.complete.txt >> CposaSequence2_${f}.fasta; done
```
# 2. Build trees for each microhaplotype fasta:
```bash
for f in `ls CposaSequence2_*fasta` ;do /Applications/standard-RAxML-master/raxmlHPC-SSE3 -f a -m BINGAMMA -n ${f/\.fasta/}.nwk -s $f -p 12345 -x 12345 -# 100; done
```
# 3. Plot trees using facet_wrap:
