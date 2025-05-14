# Analysis of FACS based pooled CRISPR screens in iPSC derived microglia like cells using MAGeCK 

This directory contains the files to analyse pooled CRISPR screens in iPSC derived microglia like cells (iMGL) as described in Washer et al 2025 and Perez-Alcantara et al 2025. 

## An overview of the protocol: 

![CRISPR Screening Graphical Abstract (1)](https://github.com/user-attachments/assets/682099d5-029a-432f-b03a-329976de4a82)

Two libraries and independent screens have been benchmarked to this pipeline. 
* Single guide all-in-one CRISPR v3 - containing a sgRNA and Cas9 within the same vector (Washer et al 2025) - library size: 83
* Dual guide all-in-one CRISPR v3 - containing two guides and Cas9 within the same vector (Perez-Alcantara et al 2025) - library size: 783

The libraries were transduced into macrophage precursors cells at an MOI of 1.5 - resulting in approx 70% positive cells following puromycin selection during titration. This is to reduce the background of untransduced cells in the final timepoints. After 14d of differentiation to iMGL
the cells are ready for the phenotypic assay of choice.

Our assay utilised a phagocytic cargo of dead neurons double labelled with mCherry-EGFP (pmChGIP SH-SY5Y, upon phagocytosis into the iMGL the EGFP is quenched to form a single mCherry positive population. iMGL are allowed to phagocytose these neurons for 6 hours before washing, lifting, and fixing. The
mCherry positive iMGL were then sorted into four equal bins based on their mCherry+ signal, with increased mCherry indicating increased phagocytosis upon knockout. 

![SH-SY5Y Traffic Light Assay (1)](https://github.com/user-attachments/assets/d446eca4-42ff-477a-992a-133024af10d1)

DNA was then extracted from the iMGL and the gRNA were amplified through nested PCR and sequenced through Illumina NovaSeq or HiSeq and analysed through MAGeCK as described here. 

## Files within this directory

The data included within this repository is from the Washer et al 2025 pilot project: 

* Scripts
  + CRISPR_Screening in Microglia.rmd - A .rmd file containg the analysis script required to generate a consise report based on the input data outlined below

* Outputs from the MAGeCK count required for the downstream analysis in R  
  + Reverse_Merged.count.txt - count matrix containing read counts of each sgRNA per sample  
  + Reverse_Merged.count_normalized.txt - a normalised count matrix (normalised to library size or controls - utilised for plotting the guide abundances across the bins)  
  + Reverse_Merged.countsummary.txt - summary file containing mapping rates and gini indexes utilised for the QC pipelines

* Outputs from the MAGeCK test required for the downstream analysis in R
  + L20_T20_controlnorm.gene_summary.txt - a .txt file containing the gene level log2 fold changes, p-values, and FDR corrected p-values  
  + L20_T20_controlnorm.sgrna_summary.txt - a .txt file containing the sgRNA level log2 fold changes across the compared populations
 
* Generated files from running the .rmd script
  + CRISPR_Analysis.html - A .html file containing the output analysis from running the above script
  + L20_T20_controlnorm.gene_summary.csv - a .csv file containing the gene level log2 fold changes, p-values, and FDR corrected p-values  
  + L20_T20_controlnorm_gdata.csv - a .csv file containing the gene name, Score (log2 fold change), FDR corrected p-values, and the Rank (based on Log2 fold changes)  
