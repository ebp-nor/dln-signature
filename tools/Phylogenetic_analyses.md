# Phylogenetic Analyses

Once you have your species tree and your gene trees you want to use these to make biological inferences. There are many methods that analyse data in a phylogenetic setting. Also, there are many useful tools to help you plot and visualize your phylogenetic trees. Here are some tips and tricks on how to get started with phylogenetic analyses. 

## Constructing trees
To make the phylogenetic tree you can use [Orthofinder](OrthoFinder.md). This program will give you both a species tree and gene trees. There are many more sophisticated ways of generating phylogenetic trees, but this is beyond the scope of your project. Using the output from Orthofinder is more than good enough. 

## File formats
Trees come in many different file formats. Nexus files (file.nex, .nxs etc), newick files (.nwk) or tree files (.tre). There are many more. 

The trick is to find a program that can interpret your data. [Figtree](http://tree.bio.ed.ac.uk/software/figtree/) is a free program that is easy to use. Dowload this to your desktop and use it to open up treefiles, for instance from Orthofinder. In my experience, Figtree will recognize a treefile even if the extension is just .txt. It can open most trees. 

## Trait evolution 

Once you have your species tree you want to map some data on specific traits and infer how these traits have evolved. Here is a nice introduction to trait evolution on a [phylogentic tree](https://www.nature.com/scitable/topicpage/trait-evolution-on-a-phylogenetic-tree-relatedness-41936/). There are many statistical frameworks for trait evolution using phylogenetic information. In 1985 [Felsenstein](https://www.jstor.org/stable/2461605#metadata_info_tab_contents) came up with a method using something called phylogenetic independent contrasts [pic](https://www.r-phylo.org/wiki/HowTo/Phylogenetic_Independent_Contrasts). Here you can run a regression between for instance number of genes in a gene family and lipid production, while controlling for phylogenetic relatedness (i.e. data from related species is not independent).

## Plotting and analysing trees in R

There are many R packages that are really handy for visualizing and analysing trees. Here is a list of tutorials that might prove useful to you. 

[Combining trees with other plots](https://thackl.github.io/ggtree-composite-plots)

[Phylogenetic visualization](https://yulab-smu.top/treedata-book/chapter7.html)

[Phylogenetics in R](https://guangchuangyu.github.io/ggtree-book/chapter-treeio.html), here there is also an explanation of file formats used in phylogenetics

[combining plots in R](https://yulab-smu.top/pkgdocs/aplot.html#axis_align)



