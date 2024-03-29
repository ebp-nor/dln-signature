# Harnessing data from biodiversity genomics projects

![image](https://user-images.githubusercontent.com/46928237/191249452-74e187c4-cc15-4807-af7e-59b0d0e756dd.jpeg)


This is the description for the project called "Harnessing data from biodiversity genomics projects" in the Digital Life Norway course [BT8121 - Transdisciplinary biotechnology](https://www.digitallifenorway.org/research-school/events/BT8121---transdisciplinary-biotechnology_2022.html). Here you will find relavant literature, introductions and guides to relevant tools and presentations given, in addition to the description of the project itself.

The overall aim of this project is to use comparative genomics tools on a set of species to find interesting patterns between those species. The species selected here are in [Mucoromycota](https://en.wikipedia.org/wiki/Mucoromycota), a division within fungi. Many species of this division have been used to produce lipids, polyphosphates and carotenoids. Since these are important in biotechnology, many of these species have published data regarding how well they produce these mentioned compounds. Therefore, another aspect of this project would be to find phenotypical differences (how much of a particular lipid produced for instance) and try to trace these differences to genomic differences and the other way, find genomic differences and figure out what these might lead to in phenotypical differences. 

To reach the aims of this project, you will have to use different comparative genomic tools, search existing litterature for experimental data and connect this based on the phylogeny between the different species. Here we will suggest some tools that should enable you to reach these goals, but you can also choose to use other approaches than these. 

As a starting point, you should use the relevant species from [EnsemblFungi](https://fungi.ensembl.org/index.html). For instance this link contains it all:
http://ftp.ensemblgenomes.org/pub/fungi/release-54/fasta/fungi_mucoromycota1_collection/. You should use an outgroup or two, for instance http://ftp.ensemblgenomes.org/pub/fungi/release-54/fasta/fungi_entomophthoromycota1_collection/conidiobolus_coronatus_nrrl_28638_gca_001566745/ and including http://ftp.ensemblgenomes.org/pub/fungi/release-54/fasta/saccharomyces_cerevisiae/ is likely a good idea. You need both the predicted proteins and the genome assemblies. (If you want all the mucoromycota genomes, you can use this command: `rsync -av rsync://ftp.ensemblgenomes.org/all/pub/fungi/release-54/fasta/fungi_mucoromycota1_collection/*/dna/*sm.toplevel.fa.gz ./` change and adapt for the outgroup and protein sequences).

We have set up a project on [Saga](https://documentation.sigma2.no/hpc_machines/saga.html) where you can install programs and run different analyses. If you are unsure of the usage of the command line and bash, you can take a look at https://swcarpentry.github.io/shell-novice/ to get an introduction. You should download the genomes and annotated proteins for the species from EnsemblFungi. Several steps can then be done in parallel:

- The different genomes might have been created at different time points, from different sequencing technologies and different programs. Fungi are often not so complicated to assemble, but there might still be some differences. To quantify and qualify these, you should get basic assembly statistics using [gfastats](https://github.com/vgl-hub/gfastats). More fragmented genomes might lead to poorer annotation because gene models might be split and genes missing altogether. To assess the gene complement (and possibly the quality of the assembly), [BUSCO](https://busco.ezlab.org) should be run on the genomes.

- To get an understanding of differences in gene sets between the species, [OrthoFinder](https://github.com/davidemms/OrthoFinder) is a good tool to run on the annotated proteins. Read more about it [here](tools/OrthoFinder.md). OrthoFinder can also create a phylogeny of the different species (which can be used for Cactus and other analyses).

- [Cactus](https://github.com/ComparativeGenomicsToolkit/cactus) can used to generate a multiple whole genome alignment of the species. The alignment can be used to genomic differences (insertions, deletions, inversions, duplications, transpositions) between the different species. For instance, a possible expansion in a gene family (from OrthoFinder results) can then be traced to the genome level. Read more about [Cactus here](tools/cactus.md).

- [CAFE5](https://github.com/hahnlab/CAFE5) provides a statistical foundation for evolutionary inferences. It can be interesting to run it on the OrthoFinder results.

As a starting point, [Comparative genomics applied to _Mucor_ species with different lifestyles](https://bmcgenomics.biomedcentral.com/articles/10.1186/s12864-019-6256-2), uses a couple of the above mentioned tools (OrthoFinder and CAFE) to do comparative genomics in Mucoromycota. It is most likely useful to familiarize yourself with that paper.

In addition to the comparative genomic analyses, you should find (phenotypic) differences between species based on existing litterature. The Wikipedia page for [Mucoromycota](https://en.wikipedia.org/wiki/Mucoromycota) has links to some relevant litterature, for instance [High-throughput screening of Mucoromycota fungi for production of low- and high-value lipids](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC5851148/) and [Comparative analysis of different isolated oleaginous mucoromycota fungi for their γ-linolenic acid and carotenoid production](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC7665918/).


The project area is in /cluster/projects/nn9986k on Saga. 

Please also look at the subfolders [tools](tools), [literature](literature) and [presentations](presentations). There might be information there which are not directly linked from this page.
