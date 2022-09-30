
# Whole Genome Alignment

This is modified from https://github.com/ForBioPhylogenomics/tutorials/blob/main/whole_genome_alignment/README.md. Not all content might have been adapted for this particular project, but should give a good overview of the processes.

## Summary

Large scale projects such as Earth BioGenome Project ([Lewin et al. (2018)](https://doi.org/10.1073/pnas.1720115115)), the Vertebrate Genomes Project ([Rhie et al. (2021)](https://doi.org/10.1038/s41586-021-03451-0)), and other similar efforts, aspire to sequence and assemble the genomes of all living species. More and more high quality genome assemblies are therefore being deposited in public databases, and these resources contain great potential and enables rigorous investigation into a multitude of aspects of biology through data and curiosity driven research. The further generation of high-quality genomes will hopefully facilitate great leaps in our understanding of, and ability to answer, core questions within fundamental biology such as in ecology and evolution, and in other fields such as medicine.

However, to actually understand these genomes, we need some way of analysing them. For smaller projects, sequencing and assembling a few species, annotating and analysing each can be done focussing on each in turn. However, for large projects such as Zoonimia (131 new genome assemblies) ([Zoonomia Consortium (2020)](https://doi.org/10.1038/s41586-020-2876-6)) or bird 10k (B10K; 267 new genome assemblies) ([Feng et al. (2020)](https://doi.org/10.1038/s41586-020-2873-9)), using that much time and effort on each genome is not scalable, and therefore they used whole-genome alignments to analyse their datasets. So far, the only whole-genome aligner that has been used successfully on such large datasets is Cactus ([Armstrong et al. 2020](https://doi.org/10.1038/s41586-020-2871-y)).

## Table of contents

* [Outline](#outline)
* [Dataset](#dataset)
* [Requirements](#requirements)
* [Softmasking with Red](#softmask)
* [Creating a guide tree with Mash](#mash)
* [Running Cactus](#cactus)

<a name="outline"></a>
## Outline

Originally this tutorial used one chromosome from six fish species. I have not rewritten it in total, so you'll see some references to these genome assemblies.

A short presentation of these concepts discussed is [available here](../presentations/whole_genome_alignment.pdf).

<a name="dataset"></a>
## Dataset

Here you use the dataset you yourself have defined.

<a name="requirements"></a>
## Requirements

You will basically just  [Cactus](https://github.com/ComparativeGenomicsToolkit/cactus). Red, Mash and rapidNJ should be available as modules on Saga, while Cactus works best as an container (the installation is non-trivial.)

<a name="cactus"></a>
## Running Cactus

Multiple genome alignment programs align multiple genomes toward each other, unlike pairwise genome alignment programs (such as Mummer and Minimap2) which only aligns two and two. They have existed for more than a decade, but several of the older were reference based, meaning that one genome was the reference and all others were aligned towards that. Any regions shared by the non-reference genomes would not be represented in the final alignment, a quite large limitation. [Cactus](https://github.com/ComparativeGenomicsToolkit/cactus), or Progressive Cactus as the authors also call it, is one of the few modern reference-free multiple genome aligners. The only other I know of is [SibeliaZ](https://github.com/medvedevgroup/SibeliaZ), but in my experience hasn't performed as well as Cactus.

Unfortunately, Cactus is not an easy program to use. There are likely multiple reasons for this, some might be that it parts are quite old (it builds directly on software older than a decade), which can lead to it being a bit clunky and not so easy to update those old parts. It is tightly connected to a system called Toil, which handles running jobs, and if that has some issues (we'll come back to that later), it can be hard to get working. For these reasons it can be difficult to install properly. Luckily they provide a Docker container, and Saga has support for that via Singularity, so we will use that.

To start, we need to grab the container. You don't have to do this, I put it into the work scripts, but this is basically the command:
```
singularity pull --name cactus-v2.2.0.sif docker://quay.io/comparative-genomics-toolkit/cactus:v2.2.2 
```




```
sbatch run_cactus_chr5.sh
```

And everything should work fine. In the end you'll get cichlids_chr5.hal and cichlids_chr5.maf files in your /cluster/projects/nn9458k/phylogenomics/$USERNAME folder, in addition to halValidation.chr5.txt and halStats.chr5.txt, a validation and a statistics file of the HAL file. The whole process took about 5 hours when I tried it.

halValidation.chr5.txt should basically just contain:
```
File valid
```

While halStats.chr5.txt should contain this:
```
hal v2.1
((neomar:0.0045736,neogra:0.004315)Anc1:0.00021445,((neopul:0.0033453,neooli:0.0032482)Anc3:0.00094829,neobri:0.0049009)Anc2:0.00032849,orenil:0.046583)Anc0;

GenomeName, NumChildren, Length, NumSequences, NumTopSegments, NumBottomSegments
Anc0, 3, 28764338, 471, 0, 562986
Anc1, 2, 22457867, 1162, 482173, 155250
neomar, 0, 22119859, 1278, 152061, 0
neogra, 0, 21364358, 1287, 148253, 0
Anc2, 2, 29214047, 356, 555446, 254028
Anc3, 2, 22168327, 1182, 133108, 140058
neopul, 0, 20898136, 1358, 133718, 0
neooli, 0, 21525845, 1293, 136975, 0
neobri, 0, 43197405, 18, 315265, 0
orenil, 0, 39714817, 1, 692510, 0
```
Running the full alignment is quite similar to the one above, but we need some extra information for the sbatch command since we have gotten two bigmem nodes reserved.

```
sbatch --reservation=nn9458k run_cactus_all.sh
```
If that is successful, you'll see cichlids_all.hal, halValidation.all.txt and halStats.all.txt with the content of the stats file this:

```
hal v2.1
((neomar:0.0045736,neogra:0.004315)Anc1:0.00021445,((neopul:0.0033453,neooli:0.0032482)Anc3:0.00094829,neobri:0.0049009)Anc2:0.00032849,orenil:0.046583)Anc0;

GenomeName, NumChildren, Length, NumSequences, NumTopSegments, NumBottomSegments
Anc0, 3, 681329676, 32958, 0, 16672331
Anc1, 2, 659155609, 75358, 15727138, 6780370
neomar, 0, 668470958, 89823, 6854395, 0
neogra, 0, 657998073, 91312, 6746422, 0
Anc2, 2, 662754018, 18173, 15927409, 5320178
Anc3, 2, 660323875, 78298, 4933681, 6370077
neopul, 0, 659878940, 94163, 6380869, 0
neooli, 0, 666859030, 91778, 6457234, 0
neobri, 0, 847910432, 9099, 6072207, 0
orenil, 0, 1005681550, 2460, 22880110, 0
```

You'll work further with the cichlids_chr5.maf file tomorrow.

One of the main advantages of having a multiple whole genome alignment is that you can pinpoint conserved sequences across the species. In many cases that will be exons, and a HAL file can be use for [comparative annotation](https://github.com/ComparativeGenomicsToolkit/Comparative-Annotation-Toolkit). This is outside the scope of this tutorial.

You have come to the end and are done with the tutorial. Congratulations!

