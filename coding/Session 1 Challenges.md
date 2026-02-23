## Session 1 
### 1.2) Challenges

First challenge was to navigate through the help function for much of the software to find the right information, for example understanding what the default output format was. Through looking through the literature for blast online I was able to find that the default format was pairwise and then find the corresponding codes for pairwise and tabular to understand their differences.

Challenge in understanding what I was looking at in the sequence profile, as the structure was quite confusing at first. 
![[Pasted image 20260204131746.png]]


For Exercise 6, I had very little information on how to start in terms of writing the code so I asked Claude to write simple scripts for me with explanations for each step. I then verified the information with sources online to learn better on how to complete this quicker in the future. I didnt know how to extract the sequence information from the Blast format, I then learned about how to customize the output formats to also include the necessary sequences and thus make it simpler.  

`blastp -db uniprot_Atha.fasta -query test.faa -outfmt "6 sseqid bitscore sseq" -out test.faa.blast.withseq`
`awk '$2 > 200 {print ">"$1"\n"$3}' test.faa.blast.withseq > high_score_seqs.faa`
`clustalo -i high_score_seqs.faa -o high_score_alignment.aln --outfmt=clustal`
`hmmbuild ARF6.hmm high_score_alignment.aln`
`hmmscan --tblout ARF6_hmmscan.tbl ARF6.hmm uniprot_Atha.fasta > ARF6_hmmscan.out`

However this code would only give partial sequences matching the aligned portions only, so it was suggested to use a grep loop. This worked to fetch the complete sequences:
awk '$12 > 200 {print $2}' test.faa.blast > high_score_ids.txt
while read id; do grep -A 1 "^>.*$id" uniprot_Atha.fasta; done < high_score_ids.txt > high_score_seqs.faa

Afterwards, when searching the HMM built with the previous sequence using hmmscan, I ran into an error:
Error: Failed to open binary auxfiles for ARF6.hmm: use hmmpress first
Through this I learned that hmmscan requires the data to be pressed, usually because hmmscan searches through thousands of HMM databases, in this case we only have one HMM file, therefore hmmsearch might be more appropriate but I decided to use hmmscan as it was specified in the exercise and the output would the same with an extra step.

I needed help learning how to interpret the results of this scan, Claude recommended: 
`head -20 ARF6_hmmscan.tbl`

to output the positive hits.


For Exercise 7, I used grep to find the sequence for AT1G30330.2

`grep -A 1 "AT1G30330.2" uniprot_Atha.fasta > AT1G30330.faa`

however that didnt work but then I realised that the name was used for ARF6 so I just searched that 

 grep -A 1 "ARF6" uniprot_Atha.fasta

HHPred was easy enough however I forgot to change the database when searching against the AlphaFold PDB in https://www.ebi.ac.uk/Tools/sss/ncbiblast and searched the UniProtKB/Swiss-Prot (The manually annotated section of UniProtKB) database, which left me confused with the results but I realised my error and found the AlphaFold PDB in the Structures section.


https://claude.ai/share/408f1ab8-8606-41ea-9882-057ac20a9884



For exercise 8, http://eggnog-mapper.embl.de/ was broken 


