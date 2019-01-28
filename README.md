vSNP Testing Files
======================

This document shows a small dataset that can be downloaded from NCBI SRA.  Brief instructions are provided.  It includes six Mycobacterium bovis and five Brucella suis biovar 1.  Average coverage varies from 60X to 230X.  Expect the SRA download to take a couple hours, depending on network speeds.  All FASTQ files can be ran together.  vSNP will determine the "best reference".  VCF output can be compared to the VCF files contained in the zipped files.  A successful run will produce VCF files very much if not exactly the same as those provided.  

Either the VCF files you create or the files provided in the zipped files can be use to test table generation.  Tables output should be very similar if not exactly the same as the tables provided.

## _Mycobacterium bovis_:

00-1MIDNRdeerAlc --> SRR8073662  
10-7224_MI_Emm_Beef_48 --> SRR1792265  
10-8963_MI_Alco_Beef_47 --> SRR1792271  
10-8965_MI_Alco_Beef_47 --> SRR1792272  
00-5559_MI_Alco_Beef_9 --> SRR1791698  
02-0572_MI_Alco_Beef_18 --> SRR1791772  

## _Brucella suis biovar 1_:
B13-0234_zc.vcf --> SRR2058984  
B13-0235_zc.vcf --> SRR2058985  
B13-0237_zc.vcf --> SRR2058987  
B13-0238_zc.vcf --> SRR2058988  
B13-0239_zc.vcf --> SRR2058989  

## Make list...
SRR2058984  
SRR2058985  
SRR2058987  
SRR2058988  
SRR2058989  
SRR8073662  
SRR1792265  
SRR1792271  
SRR1792272  
SRR1791698  
SRR1791772  

## Download FASTQs
for i in \`cat list`; do echo $i; fastq-dump --split-files $i; pigz ${i}*.fastq; done

## Update names
for i in *_1.fastq.gz; do mv $i ${i%_1.fastq.gz}_R1.fastq.gz; done

for i in *_2.fastq.gz; do mv $i ${i%_2.fastq.gz}_R2.fastq.gz; done

## Download Metadata
for i in \`cat list`; do wget -O ${i}.csv "http://trace.ncbi.nlm.nih.gov/Traces/sra/sra.cgi?save=efetch&db=sra&rettype=runinfo&term= $i"; done

# Run vSNP of FASTQ files

Working directory containing downloaded FASTQs

$ `vSNP.py`

To test reproducibility of step 1 VCF files output can be compared to pre-made VCF files.

# Run vSNP on pre-made VCF files

bovis_starting_files.zip  
suis1_starting_files.zip

Unzip files, set working directory to contain only VCF files.  
Bovis and suis1 VCF files must be ran separately.

# Expected table results
Mbovis-01_D20190125_1134-organized-table.xlsx

Bsuis1-09_D20190125_1135-organized-table.xlsx