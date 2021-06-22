---
title: TRUST4 testing
category: processing
tags:
- TCR/BCR
- scRNA-seq
---

Testing the TRUST4 program from Shirley Liu's lab.  

Github:  
https://github.com/liulab-dfci/TRUST4  

Paper:  
https://www.nature.com/articles/s41592-021-01142-2

### Install TRUST4
```
cd /shared/apps
git clone https://github.com/liulab-dfci/TRUST4.git
cd TRUST4
make
```

### Build genome reference

#### cellranger 3.0.0
```
perl /shared/apps/TRUST4/BuildDatabaseFa.pl \
  /shared/apps/refdata-cellranger-GRCh38-3.0.0/fasta/genome.fa \
  /shared/apps/refdata-cellranger-GRCh38-3.0.0/genes/genes.gtf \
  /shared/apps/TRUST4/human_vdjc.list \
  > refdata-cellranger-GRCh38-3.0.0_bcrtcr.fa
```

#### cellranger-arc 
zcat /shared/apps/refdata-cellranger-arc-GRCh38-2020-A-2.0.0/genes/genes.gtf.gz \
  > genes.gtf
```
perl /shared/apps/TRUST4/BuildDatabaseFa.pl \
  /shared/apps/refdata-cellranger-arc-GRCh38-2020-A-2.0.0/fasta/genome.fa \
  genes.gtf \
  /shared/apps/TRUST4/human_vdjc.list \
  > refdata-cellranger-arc-GRCh38-2020-A-2.0.0_bcrtcr.fa
```

### Retrieve IMGT reference
```
perl /shared/apps/TRUST4/BuildImgtAnnot.pl \
  Homo_sapien\
  > Homo-sapiens_IMGT+C.fa
```

### cellranger: Run TRUST4 starting with a BAM file
```
outs_path=/mnt/x066-rna/X066-RP1C1W1/outs

zcat ${outs_path}/filtered_feature_bc_matrix/barcodes.tsv.gz \
  | sed 's/-1//g' \
  > aligned_barcodes.txt

/shared/apps/TRUST4/run-trust4 \
  -b ${outs_path}/possorted_bam.bam \
  -f refdata-cellranger-GRCh38-3.0.0_bcrtcr.fa \
  --ref Homo-sapiens_IMGT+C.fa \
  --barcode CB \
  --barcodeWhitelist aligned_barcodes.txt \
  -t 16 \
  -o X066-MP0C1W3
```

### arc: Run TRUST4 starting with a BAM file
```
outs_path=/mnt/x066-multiome/X066-Well3/outs

zcat ${outs_path}/filtered_feature_bc_matrix/barcodes.tsv.gz \
  | sed 's/-1//g' \
  > aligned_barcodes.txt

/shared/apps/TRUST4/run-trust4 \
  -b ${outs_path}/gex_possorted_bam.bam \
  -f refdata-cellranger-arc-GRCh38-2020-A-2.0.0_bcrtcr.fa \
  --ref Homo-sapiens_IMGT+C.fa \
  --barcode CR \
  --barcodeWhitelist aligned_barcodes.txt \
  -t 16 \
  -o X066-MP0C1W3
```

