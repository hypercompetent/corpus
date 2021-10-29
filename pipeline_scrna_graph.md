```
graph TD

subgraph Per Well

  subgraph RNA
    rna_fq[RNA FASTQs]-->cr_rna[cellranger]
    cr_rna-->rna_01[tenx-rnaseq-pipeline <br/> run_add_rna_metadata.R]
    rna_01-->rna_split[BarMixer <br/> run_h5_split_by_hash.R]
  end

  subgraph HTO
    hto_fq[HTO FASTQs]-->hto_bc[BarCounter]
    hto_bc-->hto_parse[BarMixer <br/> run_hto_parsing.R]
    hto_parse-->rna_split
  end
  
end

subgraph Across Wells
  rna_split-->rna_merge[BarMixer <br/> run_h5_merge_by_hash.R]
end
```