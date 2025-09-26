#Obtain karyotype file
seqkit fx2tab -ln pp.fasta > pp.chr_len
less pp.chr_len | awk 'BEGIN{print "Chr" "\t" "Start" "\t" "End"} 
 {
if($1=="Chr01")print "01" "\t" "0" "\t" $2;
else if($1=="Chr02")print "02" "\t" "0" "\t" $2;
else if($1=="Chr03")print "03" "\t" "0" "\t" $2;
else if($1=="Chr04")print "04" "\t" "0" "\t" $2;
else if($1=="Chr05")print "05" "\t" "0" "\t" $2;
else if($1=="Chr06")print "06" "\t" "0" "\t" $2;
else if($1=="Chr07")print "07" "\t" "0" "\t" $2;
else if($1=="Chr08")print "08" "\t" "0" "\t" $2;
else if($1=="Chr09")print "09" "\t" "0" "\t" $2;
else if($1=="Chr10")print "10" "\t" "0" "\t" $2;
else if($1=="Chr11")print "11" "\t" "0" "\t" $2;
else if($1=="Chr12")print "12" "\t" "0" "\t" $2;
else if($1=="Chr13")print "13" "\t" "0" "\t" $2;
else if($1=="Chr14")print "14" "\t" "0" "\t" $2;
else if($1=="Chr15")print "15" "\t" "0" "\t" $2;
else if($1=="Chr16")print "16" "\t" "0" "\t" $2;
else if($1=="Chr17")print "17" "\t" "0" "\t" $2;
else if($1=="Chr18")print "18" "\t" "0" "\t" $2;
else if($1=="Chr19")print "19" "\t" "0" "\t" $2;
else if($1=="Chr20")print "20" "\t" "0" "\t" $2;
else if($1=="Chr21")print "21" "\t" "0" "\t" $2;
else if($1=="Chr22")print "22" "\t" "0" "\t" $2;
else if($1=="Chr23")print "23" "\t" "0" "\t" $2;
else if($1=="Chr24")print "24" "\t" "0" "\t" $2;
else if($1=="Chr25")print "25" "\t" "0" "\t" $2;
else if($1=="Chr26")print "26" "\t" "0" "\t" $2
 }' > pp.karyotype

#Chromosome bin
less pp.chr_len | awk '{print  $1 "\t" $2}' > pp.chr_len2
bedtools makewindows -g pp.chr_len2 -w 100000 > pp.chromosome_100k.windows

#Get density file
less All_G4.bed | awk '$1~"Chr" && $2>=1 && $3>=2{print $0}' > All_G4
less All_G4 | awk '{if($2<$3)print $1"\t"$2-1"\t"$3; else print $1"\t"$3-1"\t"$2}' > G4.bed
bedtools coverage -a pp.chromosome_100k.windows -b G4.bed | cut -f 1-4 > G4.cov
less G4.cov | awk 'BEGIN{print "Chr" "\t" "Start" "\t" "End" "\t" "Value" "\t" "Color"}
{
if($1=="Chr01")print "01" "\t" $2 "\t" $3 "\t" $4 "\t" "11df1f";
else if($1=="Chr02")print "02" "\t" $2 "\t" $3 "\t" $4 "\t" "11df1f";
else if($1=="Chr03")print "03" "\t" $2 "\t" $3 "\t" $4 "\t" "11df1f";
else if($1=="Chr04")print "04" "\t" $2 "\t" $3 "\t" $4 "\t" "11df1f";
else if($1=="Chr05")print "05" "\t" $2 "\t" $3 "\t" $4 "\t" "11df1f";
else if($1=="Chr06")print "06" "\t" $2 "\t" $3 "\t" $4 "\t" "11df1f";
else if($1=="Chr07")print "07" "\t" $2 "\t" $3 "\t" $4 "\t" "11df1f";
else if($1=="Chr08")print "08" "\t" $2 "\t" $3 "\t" $4 "\t" "11df1f";
else if($1=="Chr09")print "09" "\t" $2 "\t" $3 "\t" $4 "\t" "11df1f";
else if($1=="Chr10")print "10" "\t" $2 "\t" $3 "\t" $4 "\t" "11df1f";
else if($1=="Chr11")print "11" "\t" $2 "\t" $3 "\t" $4 "\t" "11df1f";
else if($1=="Chr12")print "12" "\t" $2 "\t" $3 "\t" $4 "\t" "11df1f";
else if($1=="Chr13")print "13" "\t" $2 "\t" $3 "\t" $4 "\t" "11df1f";
else if($1=="Chr14")print "14" "\t" $2 "\t" $3 "\t" $4 "\t" "11df1f";
else if($1=="Chr15")print "15" "\t" $2 "\t" $3 "\t" $4 "\t" "11df1f";
else if($1=="Chr16")print "16" "\t" $2 "\t" $3 "\t" $4 "\t" "11df1f";
else if($1=="Chr17")print "17" "\t" $2 "\t" $3 "\t" $4 "\t" "11df1f";
else if($1=="Chr18")print "18" "\t" $2 "\t" $3 "\t" $4 "\t" "11df1f";
else if($1=="Chr19")print "19" "\t" $2 "\t" $3 "\t" $4 "\t" "11df1f";
else if($1=="Chr20")print "20" "\t" $2 "\t" $3 "\t" $4 "\t" "11df1f";
else if($1=="Chr21")print "21" "\t" $2 "\t" $3 "\t" $4 "\t" "11df1f";
else if($1=="Chr22")print "22" "\t" $2 "\t" $3 "\t" $4 "\t" "11df1f";
else if($1=="Chr23")print "23" "\t" $2 "\t" $3 "\t" $4 "\t" "11df1f";
else if($1=="Chr24")print "24" "\t" $2 "\t" $3 "\t" $4 "\t" "11df1f";
else if($1=="Chr25")print "25" "\t" $2 "\t" $3 "\t" $4 "\t" "11df1f";
else if($1=="Chr26")print "26" "\t" $2 "\t" $3 "\t" $4 "\t" "11df1f"
}' > G4_density

#Running RIdeogram in R
require(RIdeogram)
PP_karyotype <- read.table("pp.karyotype", sep = "\t", header = T, stringsAsFactors = F)
Random_RNAs_500 <- read.table("G4_density", sep = "\t", header = T, stringsAsFactors = F)
ideogram(karyotype = PP_karyotype, label = Random_RNAs_500, label_type = "polygon", colorset1 = c("#e5f5f9", "#99d8c9"), output = "G4.svg")



