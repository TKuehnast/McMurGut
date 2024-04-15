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
