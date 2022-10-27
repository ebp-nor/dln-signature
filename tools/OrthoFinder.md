
# Orthofinder

[Orthofinder](https://github.com/davidemms/OrthoFinder) is an easy, fast and great tool to study the evolutionary relationship between genes, and identify gene duplications. It also provides a species tree, as well as gene trees. 

![image](https://user-images.githubusercontent.com/46928237/191227132-3227f638-abd4-4804-9b91-fbc080c905d9.png)


## What are orthologs? paralogs? homologs? 
Homology is similarity due to shared ancestry between a pair of structures or genes in different taxa. If two genes share ancestry following a speciation event, they are known as orthologs. If two genes trace their ancestry back to a gene duplication event, they are known as paralogs.

![image](https://user-images.githubusercontent.com/46928237/193239122-33223055-afc8-4f47-91a1-3d341e18535f.png)

Orthofinder identifies something they call orthogroups. An orthogroup is the set of genes derived from a single gene in the last common ancestor of all the species under consideration.

## Orthofinder tutorial

[Step-by-Step OrthoFinder Tutorials](https://davidemms.github.io/menu/tutorials.html): This is a series of tutorials that go through how to find data and use it to run OrthoFinder. 

They show you how to manually downliad data from different databases. To do this step on the command line, look at tips and tricks in the databases section. 

## Example script
```
#!/bin/bash

#SBATCH --job-name=orthofinder
#SBATCH --account=nn9986k
#SBATCH --time=4:0:0
#SBATCH --mem-per-cpu=4500M
#SBATCH --nodes=1
#SBATCH --ntasks-per-node=15


source /cluster/projects/nn9986k/miniconda3/etc/profile.d/conda.sh

eval "$(conda shell.bash hook)"

conda activate braker

orthofinder -a 15 \
-t 15 \
-f proteins > orthofinder.out 2> orthofinder.err
```
