#Output two repeated overlapping peaks
bedtools intersect -a G4_rep1.bed -b G4_rep2.bed > merge_G4_peak.bed
sort -k1,1 -k2,2n -k3,3n merge_G4_peak.bed > sorted_G4_peak.bed
bedtools merge -i sorted_G4_peak.bed > G4_peak.bed

#Output overlap with PQS
bedtools intersect -a PQS_G2A.bed -b G4_peak.bed -wa -f 1.0 > G2A.bed
bedtools intersect -a PQS_G2B.bed -b G4_peak.bed -wa -f 1.0 > G2B.bed
bedtools intersect -a PQS_G2C.bed -b G4_peak.bed -wa -f 1.0 > G2C.bed
bedtools intersect -a PQS_G3A.bed -b G4_peak.bed -wa -f 1.0 > G3A.bed
bedtools intersect -a PQS_G3B.bed -b G4_peak.bed -wa -f 1.0 > G3B.bed
bedtools intersect -a PQS_G3C.bed -b G4_peak.bed -wa -f 1.0 > G3C.bed

#Merge G2-type eG4, G3-type eG4, and Total eG4
cat G2A.bed G2B.bed G2C.bed  | sort -k1,1 -k2,2n -k3,3n  | uniq  > All_G2.bed
cat G3A.bed G3B.bed G3C.bed  | sort -k1,1 -k2,2n -k3,3n  | uniq  > All_G3.bed
cat All_G2.bed All_G3.bed  | sort -k1,1 -k2,2n -k3,3n  | uniq  > All_G4.bed

