BUSCO uses a set of genes that are expected to be found inside a particlar clade. It is widely used to assess the quality of a genome assembly. 
[This](https://currentprotocols.onlinelibrary.wiley.com/doi/full/10.1002/cpz1.323) is a good introduction to setting it up and running it. 

The output is something similar to this:

```
# BUSCO version is: 5.2.2
# The lineage dataset is: saccharomycetes_odb10 (Creation date: 2020-08-05, number of genomes: 76, number of BUSCOs: 2137)
# Summarized benchmarking in BUSCO notation for file /data/manni/busco_protocol/protocol1/Tglobosa_GCF_014133895.1_genome.fna
# BUSCO was run in mode: genome
# Gene predictor used: metaeuk
***** Results: *****
C:99.6%[S:99.5%,D:0.1%],F:0.1%,M:0.3%,n:2137
2129    Complete BUSCOs (C)
2126    Complete and single-copy BUSCOs (S)
3      Complete and duplicated BUSCOs (D)
3      Fragmented BUSCOs (F)
5      Missing BUSCOs (M)
2137    Total BUSCO groups searched
Dependencies and versions:
hmmsearch: 3.1
metaeuk: 4.a0f584d
```

It it searched for 2137 BUSCO groups, and found 2129 (99.6 %) of them. This is then a quite good genome assembly and we can for many purposes trust it.
