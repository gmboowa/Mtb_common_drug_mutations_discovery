#! /bin/bash

start=$SECONDS
echo $HOSTNAME

echo $"Written by"  'Gerald Mboowa 🙏🧘 🍷🐒😍 ☣ 🇩🇪 ' | sed $'s/Gerald Mboowa 🙏🧘 🍷🐒😍 ☣ 🇩🇪 /\e[32m&\e[0m/';

echo $"This is" 'FastQC MultiQC Snippy Rapid Bacterial SNP Calling Script  Version 1.0.0' | sed $'s/FastQC MultiQC Snippy Rapid Bacterial SNP Calling Script  Version 1.0.0/\e[36m&\e[0m/';

echo $"Author email"  '...@gmail.com' or '...@chs.mak.ac.ug' or '...@bcm.edu' or '...@alumni.bcm.edu' | sed $'s/...@gmail.com or ...@chs.mak.ac.ug or ...@bcm.edu or ...@alumni.bcm.edu/\e[33m&\e[0m/';

##For MTB the references utilised here include;
##https://www.thelancet.com/pdfs/journals/laninf/PIIS1473-3099(15)00062-6.pdf {Whole-genome sequencing for prediction of Mycobacterium tuberculosis drug susceptibility and resistance: a retrospective cohort study}
##https://www.nature.com/articles/ncomms5812  {A robust SNP barcode for typing Mycobacterium tuberculosis complex strains}

cd ~/working-directory

echo $"Now Running FastQC for the Samples" | sed $'s/Now Running FastQC for the Samples/\e[32m&\e[0m/';

for sample in `cat list.txt`
do

    fastqc ${sample}*_1.fastq.gz ${sample}*_2.fastq.gz

done

echo $"Now Running MultiQC for the Samples" | sed $'s/Now Running MultiQC for the Samples/\e[36m&\e[0m/';

multiqc .

echo $"Now Running Snippy for the Samples" | sed $'s/Now Running Snippy for the Samples/\e[33m&\e[0m/';


for sample in `cat list.txt`
do

  R1=${sample}_1.fastq.gz
  R2=${sample}_2.fastq.gz

~/snippy --cpus 16 --outdir ${sample}.snps --ref ~/NCBI_Reference.gbk --R1 $R1 --R2 $R2


echo $"Now Running MTB Uga.Genotype and Drug Resistance Annotations for the Samples" | sed $'s/Now Running MTB Ug.Genotype and Drug Resistance Annotations for the Samples/\e[31m&\e[0m/';

{ grep -E "ahpC|fabG1|inhA|katG|ndh|rpoB|embA|embB|embC|embR|iniA|iniC|manB|rmlD|pncA|rpsA|gyrA|gyrB|rpsL|gidB|rrs|tlyA|eis" ${sample}.snps/snps.tab | grep "missense_variant" ; egrep -w --color -E 'p.Thr80Ala|874787|1501468' ${sample}.snps/snps.tab;}  > ${sample}.Details-of-UG-MTB-Genotype-and-Drug_resistance.txt

echo $"Now Running Summaries for MTB Genotype and Drug Resistance for the Samples" | sed $'s/Now Running Summaries for MTB Genotype and Drug Resistance for the Samples/\e[33m&\e[0m/';

{ grep -q -E 'p.Thr80Ala|7539' ${sample}.Details-of-UG-MTB-Genotype-and-Drug_resistance.txt; if [ $? -eq 0 ]; then echo "MTB Uganda Detected" ; fi ; grep -q  '874787' ${sample}.Details-of-UG-MTB-Genotype-and-Drug_resistance.txt; if [ $? -eq 0 ]; then echo "MTB Uganda I Detected" ; fi ; grep -q  '1501468' ${sample}.Details-of-UG-MTB-Genotype-and-Drug_resistance.txt; if [ $? -eq 0 ]; then echo "MTB Uganda II Detected" ; fi ; grep -q  'rpoB' ${sample}.Details-of-UG-MTB-Genotype-and-Drug_resistance.txt; if [ $? -eq 0 ]; then echo "Rifampicin Resistance Detected" ; fi; grep -q -E  'embA|embB|embC|embR|iniA|iniC|manB|rmlD'  ${sample}.Details-of-UG-MTB-Genotype-and-Drug_resistance.txt; if [ $? -eq 0 ]; then echo "Ethambutol Resistance Detected" ; fi; grep -q  'gyrA'  ${sample}.Details-of-UG-MTB-Genotype-and-Drug_resistance.txt; if [ $? -eq 0 ]; then echo "Ofloxacin | Moxifloxacin | Ciprofloxacin Resistance Detected" ; fi ; grep -q  'rpsL'  ${sample}.Details-of-UG-MTB-Genotype-and-Drug_resistance.txt; if [ $? -eq 0 ]; then echo "Streptomycin Resistance Detected" ; fi; grep -q  'eis'  ${sample}.Details-of-UG-MTB-Genotype-and-Drug_resistance.txt; if [ $? -eq 0 ]; then echo "Kanamycin Resistance Detected" ; fi; grep -q -E  "gidB|rrs|tlyA"  ${sample}.Details-of-UG-MTB-Genotype-and-Drug_resistance.txt; if [ $? -eq 0 ]; then echo "Amikacin | Capreomycin Resistance Detected" ; fi; grep -q -E  'pncA|rpsA' ${sample}.Details-of-UG-MTB-Genotype-and-Drug_resistance.txt; if [ $? -eq 0 ]; then echo "Pyrazinamide Resistance Detected" ; fi; grep -q -E  'ahpC|fabG1|inhA|katG|ndh' ${sample}.Details-of-UG-MTB-Genotype-and-Drug_resistance.txt; if [ $? -eq 0 ]; then echo "Isoniazid Resistance Detected" ; fi;} > ${sample}.Summary-and-Interpretation-of-UG-MTB-Genotype-and-Drug_resistance.txt

##Interpretation of Multi-Drug Resistant Mycobacterium tuberculosis and Ug.Genotypes
##For Multi-drug Resistant (MDR-tuberculosis)

{ grep -q -E 'Rifampicin Resistance Detected|Isoniazid Resistance Detected' ${sample}.Summary-and-Interpretation-of-UG-MTB-Genotype-and-Drug_resistance.txt; if [ $? -eq 0 ]; then echo "Rifampicin Resistance Detected|Isoniazid Resistance Detected" ; fi ;} > ${sample}.MDR-TB.txt

##cat ${sample}.MDR-TB.txt  | { grep -q -E 'Amikacin Resistance Detected|Capreomycin Resistance Detected|Kanamycin Resistance Detected' ${sample}.Summary-and-Interpretation-of-UG-MTB-Genotype-and-Drug_resistance.txt && if [ $? -eq 1 ]; then echo "Extensively drug-resistant tuberculosis (XDR-TB) Detected" ; fi;} >  ${sample}.Extensively-drug-resistant-tuberculosis-XDR-TB.txt

##cat ${sample}.MDR-TB.txt | { grep -q -E 'Amikacin Resistance Detected|Capreomycin Resistance Detected|Kanamycin Resistance Detected' ${sample}.Summary-and-Interpretation-of-UG-MTB-Genotype-and-Drug_resistance.txt && if [ $? -eq 0 ] ; then echo "Extensively drug-resistant tuberculosis (XDR-TB) Detected" ; fi;} > ${sample}.Extensively-drug-resistant-tuberculosis-XDR-TB.txt

##cat ${sample}.MDR-TB.txt || { echo 'MDR-TB' ; exit 0; } &  PIDIOS=$!  && { grep -q -E 'Amikacin Resistance Detected|Capreomycin Resistance Detected|Kanamycin Resistance Detected'  ${sample}.Summary-and-Interpretation-of-UG-MTB-Genotype-and-Drug_resistance.txt| if [ $? -eq 0 ] ; then echo "Extensively drug-resistant tuberculosis (XDR-TB) Detected" ; fi;} &  PIDMIX=$! wait $PIDIOS wait $PIDMIX >  ${sample}.Extensively-drug-resistant-tuberculosis-XDR-TB.txt

##cat ${sample}.MDR-TB.txt || { echo 'my_command failed' ; exit 0; } && { grep -q -E 'Amikacin Resistance Detected|Capreomycin Resistance Detected|Kanamycin Resistance Detected'  ${sample}.Summary-and-Interpretation-of-UG-MTB-Genotype-and-Drug_resistance.txt | if [ $? -eq 0 ] ; then echo "Extensively drug-resistant tuberculosis (XDR-TB) Detected" ; fi;} >  ${sample}.Extensively-drug-resistant-tuberculosis-XDR-TB.txt

##cat ${sample}.MDR-TB.txt  && { grep -q -E 'Amikacin Resistance Detected|Capreomycin Resistance Detected|Kanamycin Resistance Detected' ${sample}.Summary-and-Interpretation-of-UG-MTB-Genotype-and-Drug_resistance.txt; if [ $? -eq 1 ] ; then echo "Extensively drug-resistant tuberculosis (XDR-TB) Detected" ; fi;} >  ${sample}.Extensively-drug-resistant-tuberculosis-XDR-TB.txt

##{grep 'Multi-Drug Resistant Tuberculosis Detected' ${sample}.MDR-TB.txt && { grep -q -E 'Amikacin Resistance Detected|Capreomycin Resistance Detected|Kanamycin Resistance Detected'  ${sample}.Summary-and-Interpretation-of-UG-MTB-Genotype-and-Drug_resistance.txt| if [ $? -eq 0 ] ; then echo "Extensively drug-resistant tuberculosis (XDR-TB) Detected" ; fi;} }  >  ${sample}.Extensively-drug-resistant-tuberculosis-XDR-TB.txt

##Generates and ‘Extensively-drug-resistant-tuberculosis-XDR-TB.txt’ which contains both “Multi-Drug Resistant Tuberculosis Detected” and “Extensively drug-resistant tuberculosis (XDR-TB) Detected”

##We then use the “Multi-Drug Resistant Tuberculosis Detected” to clean out any files that may present as “Extensively-drug-resistant-tuberculosis-XDR-TB.txt” but yet they only have either Rifampicin or Isoniazid monoresistance and not both as defined by MDR.
##XDR-TB is MDR plus resistance to 'Amikacin or Capreomycin or Kanamycin

##awk '/Rifampicin Resistance Detected|Isoniazid Resistance Detected/{print $0}' ${sample}.MDR-TB.txt > ${sample}.Extensively-drug-resistant-tuberculosis-XDR-TB.txt ; { grep -E -q 'Amikacin Resistance Detected|Capreomycin Resistance Detected|Kanamycin Resistance Detected' ${sample}.Summary-and-Interpretation-of-UG-MTB-Genotype-and-Drug_resistance.txt ;  if [ $? -eq 0 ]; then echo "Extensively drug-resistant tuberculosis (XDR-TB) Detected" ; fi;} >> ${sample}.Extensively-drug-resistant-tuberculosis-XDR-TB.txt

grep -E 'Rifampicin Resistance Detected|Isoniazid Resistance Detected' ${sample}.Summary-and-Interpretation-of-UG-MTB-Genotype-and-Drug_resistance.txt > ${sample}.Extensively-drug-resistant-tuberculosis-XDR-TB.txt ; grep -E 'Amikacin Resistance Detected|Capreomycin Resistance Detected|Kanamycin Resistance Detected' ${sample}.Summary-and-Interpretation-of-UG-MTB-Genotype-and-Drug_resistance.txt  >> ${sample}.Extensively-drug-resistant-tuberculosis-XDR-TB.txt

##find . -name "*.Extensively-drug-resistant-tuberculosis-XDR-TB.txt"| grep -v "Multi-Drug Resistant Tuberculosis Detected" | xargs rm

## deletes  "*.Extensively-drug-resistant-tuberculosis-XDR-TB.txt" file if it misses the Multi-Drug Resistant Tuberculosis Detected


echo $"Interrogating files for MTB Uganda I and New Missense Variant {Novel} Detected" | sed $'s/Interrogating files for MTB Uganda I and New Missense Variant {Novel} Detected/\e[36m&\e[0m/';

{ grep -q '874787' ${sample}.snps/snps.tab && grep -q 'Novel' ${sample}.snps/snps.tab && echo "MTB Uganda I and New Missense Variant {Novel} Detected";} >  ${sample}.MTB-Uganda-I-and-New-Missense-Variant.txt

echo $"Interrogating files for MTB Uganda II and New Missense Variant {Novel} Detected" | sed $'s/Interrogating files for MTB Uganda II and New Missense Variant {Novel} Detected/\e[36m&\e[0m/';

 { grep -q 'Novel' ${sample}.snps/snps.tab && grep -q '1501468' ${sample}.snps/snps.tab && echo "MTB Uganda II and New Missense Variant {Novel} Detected";} > ${sample}.MTB-Uganda-II-and-New-Missense-Variant.txt

## Make Script for saving only UG-I or UG-II or the new missense_variant {Novel}
## Make Script that only prints true for a combination of UG-II plus new missense_variant {Novel}
## Search and delete empty files in the current directory and subdirectories:
## -type f is necessary because also directories are marked to be of size zero.

## find -name 'file*' -size 0 -delete
## https://stackoverflow.com/questions/5475905/linux-delete-file-with-size-0
## https://mycyberuniverse.com/linux/find-and-delete-the-zero-size-files-and-empty-directories.html
## find . -size 0 | while read f; do rm "${f%.*}."* ; done
## https://superuser.com/questions/363716/bash-find-files-with-zero-size-and-delete-files-with-different-extensions

echo $"Deleting all non-MDR-TB and other Redundant files" | sed $'s/Deleting all non-MDR-TB and other Redundant files/\e[36m&\e[0m/';

find . -name '*.MDR-TB.txt' -size 0 -print0 | xargs -0 rm

find . -name '*.MDR-TB.txt' | xargs grep -Z -L 'Rifampicin' | xargs rm

find . -name '*.MDR-TB.txt' | xargs grep -Z -L 'Isoniazid' | xargs rm

find . -name '*.Extensively-drug-resistant-tuberculosis-XDR-TB.txt' | xargs grep -Z -L 'Rifampicin' | xargs rm

find . -name '*.Extensively-drug-resistant-tuberculosis-XDR-TB.txt' | xargs grep -Z -L 'Isoniazid' | xargs rm

find . -name '*.Extensively-drug-resistant-tuberculosis-XDR-TB.txt' | xargs grep -Z -L 'Amikacin\|Capreomycin\|Kanamycin' | xargs rm

find . -type f -size 0 -delete



##Get more on these color codes at https://stackoverflow.com/questions/5947742/how-to-change-the-output-color-of-echo-in-linux

end=$SECONDS

echo "duration: $((end-start)) seconds."

done

exit
