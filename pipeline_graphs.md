```
graph TD

subgraph Multiome
  m_rna_fq[Multiome RNA FASTQs]-->cr_arc
  m_atac_fq[Multiome ATAC FASTQs]-->cr_arc
  cr_arc[cellranger-arc]-->atac_00[tenx-atacseq-pipeline <br/> 00_run_arc_formatting.R]
end


subgraph RNA
  rna_fq[RNA-only FASTQs]-->cr_rna[cellranger]
  cr_rna-->rna_01[tenx-rnaseq-pipeline <br/> run_crossplatform_rna_metadata.R]
  rna_01-->rna_br[batchreporter <br/> Batch QC Approval]
  rna_br-->rna_cite{{CITE or TEA?}}
  rna_cite-->|no|rna_hash{{hashed?}}
  rna_cite-->|yes|rna_inj[tenx-rnaseq-pipeline <br/> run_adt_injectionR]
  rna_inj-->rna_hash
  rna_hash-->|no|rna_label[cell-labeling_pipeline <br/> run_seurat_pbmc_label_transfer.R]
  rna_hash-->|yes|rna_split[cell-hashing-pipeline <br/> run_h5_split_by_hash.R]
  rna_split-->rna_merge[cell-hashing-pipeline <br/> run_h5_merge_by_hash.R]
  rna_merge-->rna_label
end

atac_00-->|rna_files|rna_01
atac_00-->|atac_files|atac_01

subgraph ATAC
  atac_fq[ATAC-only FASTQs]-->cr_atac[cellranger-atac]
  cr_atac-->atac_01[tenx-atacseq-pipeline <br/> 01_crossplatform_preprocessing.sh]
  atac_01 --> atac_02[tenx-atacseq-pipeline <br/> 02_run_crossplatform_atac_qc.R]
  atac_02-->atac_br[batchreporter <br/> Batch QC Approval]
  atac_br-->atac_hash{{hashed?}}
  atac_hash-->|no|atac_10[tenx-atacseq-pipeline <br/> 10_filter_fragments.sh]
  atac_hash-->|yes|atac_11[tenx-atacseq-pipeline <br/> 11_split_fragments_by_hash.sh]
  atac_11-->atac_12[tenx-atacseq-pipeline <br/> 12_merge_fragments_by_hash.sh]
  atac_12-->atac_13[tenx-atacseq-pipeline <br/> 13_split_meta_by_hash.sh]
  atac_13-->atac_14[tenx-atacseq-pipeline <br/> 14_merge_meta_by_hash.sh]
  atac_10-->atac_20[tenx-atacseq-pipeline <br/> 20_crossplatform_postprocessing.sh]
  atac_14-->atac_20
  atac_20-->atac_21[tenx-atacseq-pipeline <br/> 21_run_assemble_atac_outputs.R]
  atac_21-->atac_30[tenx-atacseq-pipeline <br/> 30_run_archr_atac_labeling.R]
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
```