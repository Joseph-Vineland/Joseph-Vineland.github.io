## Predicting a batch of protein structures


We recently installed RoseTTAFold on our server. What a powerful tool!  I want to share with you a routine to predict a protein structure for every protein sequence in a batch.  

```shell
# follow the directions to install RoseTTAFold: https://github.com/RosettaCommons/RoseTTAFold

# in the RoseTTAFold installation directory, create a subdirectory for protein structure predictions and enter that subdirectory

mkdir predictions && cd predictions

# move all your protein sequence fasta files into this subdirectory

# activate the RoseTTAFold conda environment

conda activate RoseTTAFold

# for each protein sequence in this directory, use RoseTTAFold to predict a protein structrue

for i in $(ls *.fasta | sed 's/.fasta//')
do  
    mkdir ${i}_output	
    ../run_e2e_ver.sh  ${i}.fasta  ${i}_output	
    mv  ${i}_output/t000_.e2e.pdb  ${i}.pdb
done

```
