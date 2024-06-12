# McMurGut 1.1 (MCMG754) - Metabolic environment and model catalog of the murine gut  
**The McMurGut pipeline to create your individual model catalog and diet file to simulate the mouse microbiome**  

## 1) Retreiving murine genomes from our samples  

- Perform 16S rRNA gene amplicon sequencing on mouse feces, followed by Qiime2 taxonomy analysis (https://github.com/qiime2) to receive taxonomy file and abundance table.
- Alternatively, perform whole genome sequencing of mouse feces, followed by applying Kraken2(https://github.com/DerrickWood/kraken2)/Bracken(https://github.com/jenniferlu717/Bracken) to receive Bracken output. Transform it to mpa-like style via kreport2mpa.py (https://github.com/jenniferlu717/KrakenTools). Modify it to taxonomy file and abundance table via kr_to_Micom_v08.ipynb.
- Remove non_taxonomic entries from taxonomy file.
- Search genome catalogs such as MGBC, CMMG, UHGG and NCBI for (if available) 3 reference genomes for each species present in each genus
- Collect the genomes and compressed to .fna.gz format. CMMG genomes may be transformed from .gff.gz into .fna.gz via GFFintoFASTAv06.ipynb.

## 2) Creating metabolic models via gapseq  

Use gapseq 1.2 for metabolic reconstruction and gapfilling of the genomes (https://github.com/jotech/gapseq)  
> gapseq doall

McMurGut 1.1:
Version: 1.2; Sequence DB md5sum: 17e92c9 (2023-12-12, Bacteria) (04.2024) for 753/754 genomes.
Version: 1.2 ccd1144, 2022,  used for 1/754 genomes: GCA_022179725.1_ASM2217972v1_genomic.  

Collect .XML-files.  
Create a manifest file containing all XML files.

## 3) Combining to McMurGut 1.1  

Use Qiime2's export tool to combine XML models into a single model catalog, on all taxonomy levels.  

McMurGut 1.1: 
754 models.XML, creating...  
MCMG754_species.qza  
MCMG754_genus.qza  
MCMG754_family.qza  
MCMG754_order.qza  



## 4) Creating diet file based on McMurGut  

A skeleton medium was created, based on...  
- ssniff chow composition chart  
- theoretical mouse gut components, such as water, mucin, urea, murine bile acids  
- Micom's complete_db_medium (Micom 0.35.0 in Qiime2-amplicon-2024.2), with target doubling time of 0.1 (every ~7h), maximum flux input of 10 mmol/hour, aiming to enable growth of genera in McMurGut 1.1. 132 of 134 genera were growing (check_db_medium). See create_medium_v11.ipynb.  
Oxygen and toxic substances, which were automatically added in a first completion step, were excluded in a second run ("cpd00007", "cpd00007", "cpd00055", "cpd00071", "cpd00025", "cpd00239", "cpd00075", "cpd00116", "cpd00150").  
Metainformation and construction:  
gapseq_gut_medium_modifytossniff_v06.xlsx  

After complete_db_medium (Micom 0.35.0):  
ssniff_MCMG754_v02_diet.qza  

## 5) Using McMurGut in Micom

Integrate MCMG754_genus.qza and ssniff_MCMG754_v02_diet.qza in Micom simulation (0.35.0).  
