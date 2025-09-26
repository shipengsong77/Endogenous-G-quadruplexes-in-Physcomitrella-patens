#Summarize two replicate peaks
cat CK_G4_rep1.bed CK_G4_rep2.bed | sort -k1,1 -k2,2n | bedtools merge -i - > merged_CK_G4_peak.bed
cat T4_G4_rep1.bed T4_G4_rep2.bed | sort -k1,1 -k2,2n | bedtools merge -i - > merged_T4_G4_peak.bed

#Output two repeated overlapping peaks
bedtools intersect -a CK_G4_rep1.bed -b CK_G4_rep2.bed > CK_merge_G4_peak.bed
sort -k1,1 -k2,2n -k3,3n CK_merge_G4_peak.bed > CK_sorted_G4_peak.bed
bedtools merge -i CK_sorted_G4_peak.bed > CK_overlap_peak.bed
bedtools intersect -a T4_G4_rep1.bed -b T4_G4_rep2.bed > T4_merge_G4_peak.bed
sort -k1,1 -k2,2n -k3,3n T4_merge_G4_peak.bed > T4_sorted_G4_peak.bed
bedtools merge -i T4_sorted_G4_peak.bed > T4_overlap_peak.bed

#Find differential G4 peaks
bedtools subtract -a CK_overlap_peak.bed -b merged_T4.bed > Tu_G4_peak.bed
bedtools subtract -a T4_overlap_peak.bed -b merged_CK.bed > Tf_G4_peak.bed

#Output Tf G4 and Tu G4
#Tf G4
bedtools intersect -a PQS_2A.bed -b Tf_G4_peak.bed -wa -f 1.0 > Tf_G2A.bed
bedtools intersect -a PQS_2B.bed -b Tf_G4_peak.bed -wa -f 1.0 > Tf_G2B.bed
bedtools intersect -a PQS_2C.bed -b Tf_G4_peak.bed -wa -f 1.0 > Tf_G2C.bed
bedtools intersect -a PQS_3A.bed -b Tf_G4_peak.bed -wa -f 1.0 > Tf_G3A.bed
bedtools intersect -a PQS_3B.bed -b Tf_G4_peak.bed -wa -f 1.0 > Tf_G3B.bed
bedtools intersect -a PQS_3C.bed -b Tf_G4_peak.bed -wa -f 1.0 > Tf_G3C.bed 
cat Tf_G2A.bed Tf_G2B.bed Tf_G2C.bed  | sort -k1,1 -k2,2n -k3,3n  | uniq  > All_Tf_G2.bed
cat Tf_G3A.bed Tf_G3B.bed Tf_G3C.bed  | sort -k1,1 -k2,2n -k3,3n  | uniq  > All_Tf_G3.bed
cat All_Tf_G2.bed All_Tf_G3.bed  | sort -k1,1 -k2,2n -k3,3n  | uniq  > All_Tf_G4.bed
#Tu G4
bedtools intersect -a PQS_2A.bed -b Tu_G4_peak.bed -wa -f 1.0 > Tu_G2A.bed
bedtools intersect -a PQS_2B.bed -b Tu_G4_peak.bed -wa -f 1.0 > Tu_G2B.bed
bedtools intersect -a PQS_2C.bed -b Tu_G4_peak.bed -wa -f 1.0 > Tu_G2C.bed
bedtools intersect -a PQS_3A.bed -b Tu_G4_peak.bed -wa -f 1.0 > Tu_G3A.bed
bedtools intersect -a PQS_3B.bed -b Tu_G4_peak.bed -wa -f 1.0 > Tu_G3B.bed
bedtools intersect -a PQS_3C.bed -b Tu_G4_peak.bed -wa -f 1.0 > Tu_G3C.bed 
cat Tu_G2A.bed Tu_G2B.bed Tu_G2C.bed  | sort -k1,1 -k2,2n -k3,3n  | uniq  > All_Tu_G2.bed
cat Tu_G3A.bed Tu_G3B.bed Tu_G3C.bed  | sort -k1,1 -k2,2n -k3,3n  | uniq  > All_Tu_G3.bed
cat All_Tu_G2.bed All_Tu_G3.bed  | sort -k1,1 -k2,2n -k3,3n  | uniq  > All_Tu_G4.bed
