```
graph TD

subgraph Reference
  seurat_ref[/Seurat Celltype Reference/]
  seurat_gates[/Seurat Gate Assignments/]
  seurat_ref-->seurat_gates
  lambert_tfs[/Lambert Human TFs/]
end

subgraph Lab Results
  lab_assemble[/Assemble from HISE/]
  lab_data[Lab Data]
  lab_visual[/Data visualization/]
  lab_corr[/Correlation analysis/]
  lab_assemble-->lab_data
  lab_data-->lab_visual
  lab_data-->lab_corr
end

subgraph Olink
  olink_assemble[/Retrieve data from HISE/]
  olink_matrix[Olink Matrices]
  olink_assemble-->olink_matrix
end

subgraph Flow Cytometry
  flow_count_assemble[/Assemble gate<br/>count matrices/]
  flow_gate_matrix[Gate matrices]
  flow_count_norm[/Normalize by CBC/]
  flow_abs_matrix[Abs. gate matrices]
  flow_cd45_norm[/Normalize to %CD45/]
  flow_cd45_matrix[%CD45 gate matrices]
  flow_seurat_group[/Grouping per Seurat type/]
  flow_seurat_fracs[%CD45 per Seurat type]
  lab_data-->flow_count_norm
  flow_count_assemble-->flow_gate_matrix
  flow_gate_matrix-->flow_count_norm
  flow_count_norm-->flow_abs_matrix
  flow_gate_matrix-->flow_cd45_norm
  flow_cd45_norm-->flow_cd45_matrix
  flow_cd45_matrix-->flow_seurat_group
  seurat_gates-->flow_seurat_group
  flow_seurat_group-->flow_seurat_fracs
end

subgraph scRNA-seq
  rna_cache_hise[/Retrieve data from HISE/]
  rna_sample_h5[Sample .h5 files]
  rna_scrublet[/Score doublets with scrublet/]
  rna_scrublet_res[Scrublet results]
  rna_label[/Label Seurat types/]
  rna_label_res[Labeling results]
  rna_compare_labels[/Compare labels to Flow/]
  rna_subject_assemble[/Assemble data per subject/]
  rna_subject[Data per subject]
  rna_summary_assemble[/Summarize expression per<br/>subject+visit+type/]
  rna_summary[Summarized expression data]
  rna_deg_test[/DEGene tests per<br/>subject+type<br/>vs Pre-Treatment/]
  rna_deg_res[DEG results]
  rna_pattern_assembly[/Assemble DEG patterns/]
  rna_aggregates[Cross-subject DEG patterns]
  rna_deg_go[/GO enrichment analysis/]
  rna_go_res[Enriched GO terms]
  rna_scenic_analysis[/SCENIC network analysis<br>per subject+type/]
  rna_scenic_results[SCENIC results]
  rna_connectome_analysis[/TODO<br>Connectome network analysis/]
  
  rna_cache_hise-->rna_sample_h5
  rna_sample_h5-->rna_scrublet
  rna_scrublet-->rna_scrublet_res
  rna_sample_h5-->rna_label
  seurat_ref-->rna_label
  rna_label-->rna_label_res
  rna_label_res-->rna_compare_labels
  flow_seurat_fracs-->rna_compare_labels
  rna_sample_h5-->rna_subject_assemble
  rna_scrublet_res-->rna_subject_assemble
  rna_label_res-->rna_subject_assemble
  rna_subject_assemble-->rna_subject
  rna_subject-->rna_summary_assemble
  rna_summary_assemble-->rna_summary
  
  rna_subject-->rna_deg_test
  rna_deg_test-->rna_deg_res
  
  rna_deg_res-->rna_pattern_assembly
  rna_pattern_assembly-->rna_aggregates
  
  rna_deg_res-->rna_deg_go
  rna_deg_go-->rna_go_res
  
  rna_subject-->rna_scenic_analysis
  lambert_tfs-->rna_scenic_analysis
  rna_scenic_analysis-->rna_scenic_results
  
  rna_subject-->rna_connectome_analysis
  olink_matrix-->rna_connectome_analysis
end

subgraph scATAC-seq
  atac_cache_hise[/Retrieve data from HISE/]
  atac_sample_arrow[Sample .arrow files]
  atac_label_seurat[/Label using Seurat reference/]
  atac_seurat_labels[Seurat labels]
  atac_label_visit[/Label using matched RNA/]
  atac_visit_labels[Visit labels]
  atac_compare_labels[/Compare labels to Flow/]
  atac_cache_hise-->atac_sample_arrow
  atac_sample_arrow-->atac_label_seurat
  seurat_ref-->atac_label_seurat
  atac_label_seurat-->atac_seurat_labels
  rna_label_res-->atac_label_visit
  atac_sample_arrow-->atac_label_visit
  atac_label_visit-->atac_visit_labels
  atac_seurat_labels-->atac_compare_labels
  atac_visit_labels-->atac_compare_labels
  flow_seurat_fracs-->atac_compare_labels
end




```