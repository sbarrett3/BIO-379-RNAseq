made directory

```
#!/bin/bash
#SBATCH --job-name=sbatch1 --output=z01.%x
#SBATCH --mail-type=END,FAIL --mail-user=sb1918@georgetown.edu
#SBATCH --nodes=1 --ntasks=1 --cpus-per-task=1 --time=72:00:00
#SBATCH --mem=4G
#-----DEFINE FILE LOCATIONS----#
trim_prog=/home/sb1918/Trimmomatic-0.39/trimmomatic-0.39.jar
#--------------------------------------#
java -jar trimmomatic-0.39.jar PE \
adapters=../Trimmomatic/Trimmomatic-0.39/adapters/TruSeq3-PE.fa
input_R1=WTA1_1.fq.gz
input_R2=WTA1_2.fq.gz
output_R1_PE=WTA1_1_PE.trmPE.fq.gz
output_R1_SE=WTA1_1_SE.trmPE.fq.gz
output_R2_PE=WTA1_2_PE.trmPE.fq.gz
output_R2_SE=WTA1_2_SE.trmPE.fq.gz
java -jar $trim_prog PE \
$input_R1 \
$input_R2 \
$output_R1_PE $output_R1_SE \
$output_R2_PE $output_R2_SE \
ILLUMINACLIP:$adapters:2:30:10 \
LEADING:10 \
TRAILING:10 \
SLIDINGWINDOW:4:15 \
MINLEN:75
