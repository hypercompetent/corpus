### ATAC (unhashed) workflow
```
graph TD

  cellranger-atac-->fragments.tsv.gz
  cellranger-atac-->singlecell.csv
  cellranger-atac-->summary.csv
  fragments.tsv.gz-->01_crossplatform_preprocessing
  singlecell.csv-->01_crossplatform_preprocessing
  reference-regions-->01_crossplatform_preprocessing
  01_crossplatform_preprocessing-->reference_counts.tsv.gz
  01_crossplatform_preprocessing-->fragment_widths.tsv.gz
  01_crossplatform_preprocessing-->saturation_counts.tsv.gz
  reference_counts.tsv.gz-->02_atac_qc
  fragment_widths.tsv.gz-->02_atac_qc
  saturation_counts.tsv.gz-->02_atac_qc
  singlecell.csv-->02_atac_qc
  summary.csv-->02_atac_qc
  02_atac_qc-->all_metadata.csv.gz
  02_atac_qc-->filtered_metadata.csv.gz
  filtered_metadata.csv.gz-->10_filter_fragments
  fragments.tsv.gz-->10_filter_fragments
  10_filter_fragments-->filtered_fragments.tsv.gz
  filtered_metadata.csv.gz-->20_crossplatform_postprocessing
  filtered_fragments.tsv.gz-->20_crossplatform_postprocessing
  reference-regions-->20_crossplatform_postprocessing
  20_crossplatform_postprocessing-->reference_sparse_matrix.tsv.gz
  20_crossplatform_postprocessing-->window_sparse_matrix.tsv.gz
  reference_sparse_matrix.tsv.gz-->21_atac_out
  window_sparse_matrix.tsv.gz-->21_atac_out
  filtered_metadata.csv.gz-->21_atac_out
  filtered_fragments.tsv.gz-->21_atac_out
  21_atac_out-->archr.arrow
  21_atac_out-->reference.h5
  21_atac_out-->window.h5
  
```

