#Detection of G2-type PQS
./fastaRegexFinder.py -f pp.fasta -r '([gG]{2}\w{1,7}){3}[gG]{2}' > PQS_G2A.bed
./fastaRegexFinder.py -f pp.fasta -r '([gG]{2}\w{8,12}){3}[gG]{2}' > PQS_G2C.bed
./fastaRegexFinder.py -f pp.fasta -r '[gG]{2}\w{1,7}[gG]{2}\w{8,12}[gG]{2}\w{8,12}[gG]{2}' > G2_T1.bed
./fastaRegexFinder.py -f pp.fasta -r '[gG]{2}\w{8,12}[gG]{2}\w{1,7}[gG]{2}\w{8,12}[gG]{2}' > G2_T2.bed
./fastaRegexFinder.py -f pp.fasta -r '[gG]{2}\w{8,12}[gG]{2}\w{8,12}[gG]{2}\w{1,7}[gG]{2}' > G2_T3.bed
./fastaRegexFinder.py -f pp.fasta -r '[gG]{2}\w{8,12}[gG]{2}\w{1,7}[gG]{2}\w{1,7}[gG]{2}' > G2_T4.bed
./fastaRegexFinder.py -f pp.fasta -r '[gG]{2}\w{1,7}[gG]{2}\w{8,12}[gG]{2}\w{1,7}[gG]{2}' > G2_T5.bed
./fastaRegexFinder.py -f pp.fasta -r '[gG]{2}\w{1,7}[gG]{2}\w{1,7}[gG]{2}\w{8,12}[gG]{2}' > G2_T6.bed
cat G2_T1.bed G2_T2.bed G2_T3.bed G2_T4.bed G2_T5.bed G2_T6.bed| sort -k1,1 -k2,2n -k3,3n | uniq > PQS_G2B.bed

#Detection of G3-type PQS
./fastaRegexFinder.py -f pp.fasta -r '([gG]{3}\w{1,7}){3}[gG]{3}' > PQS_G3Abed
./fastaRegexFinder.py -f pp.fasta -r '([gG]{3}\w{8,12}){3}[gG]{3}' > PQS_G3C.bed
./fastaRegexFinder.py -f pp.fasta -r '[gG]{3}\w{1,7}[gG]{3}\w{8,12}[gG]{3}\w{8,12}[gG]{3}' > G3_T3.bed
./fastaRegexFinder.py -f pp.fasta -r '[gG]{3}\w{8,12}[gG]{3}\w{1,7}[gG]{3}\w{8,12}[gG]{3}' > G3_T4.bed
./fastaRegexFinder.py -f pp.fasta -r '[gG]{3}\w{8,12}[gG]{3}\w{8,12}[gG]{3}\w{1,7}[gG]{3}' > G3_T5.bed
./fastaRegexFinder.py -f pp.fasta -r '[gG]{3}\w{8,12}[gG]{3}\w{1,7}[gG]{3}\w{1,7}[gG]{3}' > G3_T6.bed
./fastaRegexFinder.py -f pp.fasta -r '[gG]{3}\w{1,7}[gG]{3}\w{8,12}[gG]{3}\w{1,7}[gG]{3}' > G3_T7.bed
./fastaRegexFinder.py -f pp.fasta -r '[gG]{3}\w{1,7}[gG]{3}\w{1,7}[gG]{3}\w{8,12}[gG]{3}' > G3_T8.bed
cat G3_T1.bed G3_T2.bed G3_T3.bed G3_T4.bed G3_T5.bed G3_T6.bed| sort -k1,1 -k2,2n -k3,3n | uniq > PQS_G3B.bed

#Merge G2-type PQS, G3-type PQS, and Total PQS
cat PQS_G2A.bed PQS_G2B.bed PQS_G2C.bed  | sort -k1,1 -k2,2n -k3,3n  | uniq  > All_PQS_G2.bed
cat PQS_G3A.bed PQS_G3B.bed PQS_G3C.bed  | sort -k1,1 -k2,2n -k3,3n  | uniq  > All_PQS_G3.bed
cat All_PQS_G2.bed All_PQS_G3.bed  | sort -k1,1 -k2,2n -k3,3n  | uniq  > All_PQS_G4.bed
