```
graph TD

subgraph Multiome
  m_rna_fq[Multiome RNA FASTQs]-->cr_arc
  m_atac_fq[Multiome ATAC FASTQs]-->cr_arc
  cr_arc[cellranger-arc]-->atac_00[tenx-atacseq-pipeline <br/> 00_run_arc_formatting.R]
end

atac_00-->|rna_files|rna_01

subgraph RNA
  rna_fq[RNA-only FASTQs]-->cr_rna[cellranger]
  cr_rna-->rna_01[tenx-rnaseq-pipeline <br/> run_crossplatform_rna_metadata.R]
  rna_01-->rna_br[batchreporter <br/> Batch QC Approval]
  rna_br-->rna_cite{{CITE or TEA?}}
  rna_cite-->|yes|rna_inj[tenx-rnaseq-pipeline <br/> run_adt_injectionR]
  rna_cite-->|no|rna_hash{{hashed?}}
  rna_inj-->rna_hash
  rna_hash-->|yes|rna_split[cell-hashing-pipeline <br/> run_h5_split_by_hash.R]
  rna_hash-->|no|rna_label[cell-labeling-pipeline <br/> run_seurat_pbmc_label_transfer.R]
  rna_split-->rna_merge[cell-hashing-pipeline <br/> run_h5_merge_by_hash.R]
  rna_merge-->rna_label
end

subgraph HTO
  hto_fq[HTO FASTQs]-->hto_bc[BarCounter]
  hto_bc-->hto_parse[cell-hashing-pipeline <br/> run_hto_parsing.R]
  hto_parse-->hto_br[batchreporter <br/> Batch QC Approval]
  hto_br-->atac_11
  hto_br-->rna_split
end

subgraph ADT
  adt_fq[ADT FASTQs]-->adt_bc[BarCounter]
  adt_bc-->adt_qc[tenx-rnaseq-pipeline <br/> run_adt_well_qc]
  adt_qc-->adt_br[batchreporter <br/> Batch QC Approval]
  adt_br-->rna_inj
end

classDef br fill:#f96,color:#000;
class rna_br,atac_br,hto_br,adt_br br;

classDef ir fill:#67bce0,color:#000;
class rna_01,rna_inj,adt_qc ir;
```