# McMurGut 1.1 (MCMG754) - Metabolic reconstruction catalog of the murine gut  
**The McMurGut pipeline to create your individual model catalog**  

Retreiving murine genomes from our samples  
==========================================

16S rRNA gene amplicon sequencing of mouse feces. Using Qiime2 to receive taxonomy.tsv from all our 16S sequencing results (4 murine experiments). Collapsing to genera only. Remove non_taxonomic entries.  
 
Looking into the genome catalogs MGBC, CMMG, UHGG and NCBI (in this order); and finding (if available) 3 reference genomes (according to good sequence quality if available) of each species present in this genus, into a list of 754 genomes.  
Genomes were collected and compressed into .fna.gz format. CMMG genomes were transformed from .gff.gz into .fna.gz via GFFintoFASTAv06.ipynb script.  
Manifest-table was generated, containing metadata and directory of genomes.


2) Creating metabolic models via gapseq  
====================================
Using gapseq 1.2 for metabolic reconstruction and gapfilling of 754 genomes.  
gapseq doall  
gapseq version: 1.2; Sequence DB md5sum: 17e92c9 (2023-12-12, Bacteria) (04.2024)

Old version (gapseq 1.2 ccd1144, 2022) used for 1/754 genomes: GCA_022179725.1_ASM2217972v1_genomic.

Collecting .XML-files.  

3) Combining to McMurGut 1.1  
=========================  
Using Qiime2's export tool to combine 754 models.XML, into a single model catalog, on all taxonomy levels.  
MCMG754_species.qza  
MCMG754_genus.qza  
MCMG754_family.qza  
MCMG754_order.qza  



4) Creating diet file based on McMurGut  
====================================  
A skeleton medium was created, based on...  
- ssniff chow composition chart  
- theoretical mouse gut components, such as water, mucin, urea, murine bile acids  
- Micom's complete_db_medium (Micom 0.35.0 in Qiime2-amplicon-2024.2), with target doubling time of 0.1 (every ~7h), maximum flux input of 10 mmol/hour, aiming to enable growth of genera in McMurGut 1.1. 132 of 134 genera were growing (check_db_medium). See create_medium_v11.ipynb.  
Oxygen and toxic substances, which were automatically added in a first completion step, were excluded in a second run ("cpd00007", "cpd00007", "cpd00055", "cpd00071", "cpd00025", "cpd00239", "cpd00075", "cpd00116", "cpd00150").
Metainformation and construction:  
gapseq_gut_medium_modifytossniff_v06.xlsx

After complete_db_medium (Micom 0.35.0):
ssniff_MCMG754_v02_diet.qza  

Using McMurGut in Micom (0.35.0)
====================================

Integrate MCMG754_genus.qza and ssniff_MCMG754_v02_diet.qza in Micom simulation.  
