# McMurGut - Metabolic reconstruction catalog of the murine gut
**The McMurGut pipeline to create your individual model catalog**

1) Take sequencing data from your microbiome same, such as 16S data via QIIME2, or WGS data via Kraken/Bracken, and create a taxonomy file
2) Take the taxonomy file and crop down all columns except your desired taxon level (species, genus, etc), remove duplicate, save as new file
3) Search for the taxa in specific genome catalogs or NCBI, like MGBC, CMMG, MGnify, download the genomes and prepare it in one folder
4) Create a manifest file containing all informations, genome name, taxa name, taxonomy hierarchy (domain to species)
5) Install gapseq
6) Use gapseq to create models from each downloaded genome
7) Use Qiime2 to pack all models into a single .qza file
8) Catalog is finished


Retreiving murine genomes from our samples 
==========================================

Taking taxonomy.tsv from all our 16S sequencing results (4 murine experiments). Collapse to genera only. Remove non_taxonomic entries.
 
Looking into MGBC, CMMG, UHGG and NCBI (in this order); and finding (if available) 3 reference genomes (according to good sequence quality if available) of each species present in this genus, into a list of 754 genomes.  
Genomes were compressed to .fna.gz format. CMMG genomes were transformed from .gff.gz into .fna.gz via GFFintoFASTAv06.ipynb script.  

Creating metabolic models via gapseq 
====================================
Using gapseq 1.2 for metabolic reconstruction and gapfilling of 754 genomes.  
gapseq doall  
gapseq version: 1.2; Sequence DB md5sum: 17e92c9 (2023-12-12, Bacteria) (04.2024)

Old version (gapseq 1.2 ccd1144, 2022) used for 1/754 genomes: GCA_022179725.1_ASM2217972v1_genomic.

Combining to McMurGut 1.1
=========================
Using Qiime2's export tool to combine 774 models, saved as .XML-files, into one model catalog, on all taxonomy levels.  
MCMG754_species.qza  
MCMG754_genus.qza  
MCMG754_family.qza  
MCMG754_order.qza  



Creating diet file based on McMurGut  
====================================
A skeleton medium was created, based on... (gapseq_gut_medium_modifytossniff_v06.xlsx)
- ssniff chow composition chart
- theoretical mouse gut components, such as water, mucin, urea, murine bile acids
- Micom's complete_db_medium (Micom 0.35.0 in Qiime2-amplicon-2024.2), with target doubling time of 0.1 (every ~7h), maximum flux input of 10 mmol/hour, aiming to enable growth of genera in McMurGut 1.1. 132 of 134 genera were growing (check_db_medium). See create_medium_v11.ipynb.
Oxygen and toxic substances were excluded from the completion step. "cpd00007", "cpd00007", "cpd00055", "cpd00071", "cpd00025", "cpd00239", "cpd00075", "cpd00116", "cpd00150"


The constructed media/diet file ssniff_MCMG754_v02_diet.qza was used in all upcoming mouse gut microbiome simulations.




