First issue I had was creating a new enviroment for this session, I kep having errors while trying to install the software:

`(ngs_env) ahmed@AHMEDPC:~$ mamba install bwa samtools bedtools freebayes bcftools htslib picard`
`warning  libmamba 'repo.anaconda.com', a commercial channel hosted by Anaconda.com, is used.`

`warning  libmamba Please make sure you understand Anaconda Terms of Services.`

`warning  libmamba See: https://legal.anaconda.com/policies/en/`
`bioconda/linux-64                                    5.4MB @   5.5MB/s  1.0s`
`bioconda/noarch                                      5.2MB @   4.3MB/s  1.2s`
`pkgs/main/linux-64                                   9.9MB @   6.7MB/s  1.6s`
`pkgs/main/noarch                                   815.1kB @ 906.3kB/s  1.0s`
`pkgs/r/linux-64                                      1.6MB @   1.1MB/s  1.6s`
`pkgs/r/noarch                                        2.0MB @   1.9MB/s  1.2s`
`[+] 3.6s`
`conda-forge/linux-64 ━━━━━━━━━━━━━━━━━━━━━━╸━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━  19.0MB /  51.2MB @   5.7MB/s  3.6s`
`conda-forge/noarch   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━╸━━━━━━━━━━━━━━━━━━━  17.6MB /  24.8MB @   5.4MB/s  3.6s`
`[process exited with code 1 (0x00000001)]`
`You can now close this terminal with Ctrl+D, or press Enter to restart.`

This issue was probably due to the memory limit that the WSL had on my computer, but to fix the crash I had to restart my computer. Once I downloaded all the packages individually while making sure I only had the WSL open to save on memory. All the packages were installed into my environment succesfully

For Exercise 2, when I was creating the BAM & SAM formats I forgot to change the filename extension from the SAMEA2569438.chr10.bam to .sam, not really a challenge but a reminder to always make sure that the output format is specified correctly.

Exercise 3 was challenging as I had difficulty understading the unsorted and sorted/indexed BAM files without headers, so I asked claude to help explain the structure to me and I was able to recognize which section was the CRAG and where the position of the query was etc.
I also had trouble determining how to calculate the percentage from all of the depth read data because I had forgotten about awk, with Claude the solution became quite simple. 

Exercise 4 

Some syntaxes in the updated version of picard didnt exactly match with the script in the session example. However picard was able to handle this and convert it into the new syntax with no issue.
The indexing of the created markduplicates BAM file was not explicitly stated in the session instructions so I was a little confused as to which second file IGV was asking for, which was an  indexed samtools index SAMEA2569438.chr10.sorted.reheaded.mark_duplicates.bam.bai


Exercise 5

 During the filtering I filtered a higher amount of variants than within the session 5, this could've been due to a different software version.
