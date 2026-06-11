# GWR analysis of kidney spatial transcriptomics

Analysis and figure-generation code for:

**"Applying Spatial Statistics to Spatial Transcriptomics Reveals Local M2-like
Macrophage–Fibrosis Association in Diabetic Kidney Disease"**
Terakawa K, Kawaguchi H, Nangaku M, Mimura I.

This repository contains the R code used to (1) apply geographically weighted
regression (GWR) to Visium spatial transcriptomics across three kidney cohorts
and (2) generate all main and supplementary figures and tables.

## Repository structure

```
analysis/   Per-cohort analysis pipelines (QC -> deconvolution -> fibrosis score
            -> GWR -> pseudobulk DEG). Each script saves DEG result CSVs.
  01_KPMP_DKD_primary.Rmd    Primary cohort (KPMP DKD)
  02_KPMP_HKD.Rmd            Cross-disease cohort (KPMP HKD)
  03_Susztak_DKD_PoC.Rmd     Proof-of-concept cohort (Susztak/Abedini DKD)

figures/    Figure and enrichment code (reads the saved analysis outputs)
  Fig1B_cohort_flow.Rmd      Cohort/sample flow diagram (Figure 1B)
  spatial_plots.Rmd          Per-spot M2/fibrosis/GWR/high-coupling maps
                             (Figures 2-3, 5 and Supplementary Figures S1-S5)
  volcano_plots.Rmd          Pseudobulk DEG volcano plots (Figures 2 and 4A)
  GO_GSEA_enrichment.Rmd     GO BP and GSEA Hallmark (Figure 4B-D;
                             Supplementary Tables S4-S5)
  Table2_HKD_genes.Rmd       KPMP HKD DEG table (Table 2)

data/       Place input data here (not distributed; see data/README.md)
```

## Data sources

Raw data are publicly available and must be downloaded separately:

- **Susztak/Abedini DKD Visium ST** — GEO: GSE211785 (Abedini et al., Nat Genet 2024).
- **KPMP DKD and HKD Visium ST** — Kidney Precision Medicine Project (KPMP)
  repository, https://atlas.kpmp.org .
- **KPMP single-cell RNA-seq reference atlas** — used for label transfer
  (provided as `KPMP_ref.h5ad`; Lake et al., Nature 2023).

## Setup (paths)

All file paths in the scripts use the placeholder prefix `/path/to/`.
Before running, replace `/path/to/` with the location of your local project
directory, which should contain the downloaded inputs (under `data/`) and a
writable output location.

## Run order

1. Run the scripts in `analysis/` (any cohort order). Each produces the
   high-coupling vs. reference DEG tables (`EdgeR_HighCoupling_vs_Reference_*.csv`).
2. Run the scripts in `figures/`, which read the saved analysis outputs to
   produce the figures and enrichment tables.

## Key parameters (identical across cohorts)

- QC: median nFeature_Spatial >= 500, median mitochondrial % <= 25,
  >= 100 spots/sample; spot-level nFeature > 500 and mito % < 25.
- Fibrosis score: AddModuleScore over a fixed 29-gene myofibroblast set
  (defined once and applied to all cohorts).
- GWR: `Fibrosis_Score ~ M2_Mac_fraction + log10(UMI+1)`, adaptive bandwidth
  (AIC), bisquare kernel; high-coupling = positive M2 coefficient with
  BH-adjusted p < 0.05.
- DEG: edgeR paired design `~ SampleID + Condition`, quasi-likelihood F-test,
  FDR < 0.05; samples with >= 20 high-coupling and >= 20 reference spots.

## Software

R 4.4.2. Key packages: Seurat v5, GWmodel, edgeR, clusterProfiler, fgsea,
msigdbr, BPCells, org.Hs.eg.db, enrichplot, ggplot2.
See `SESSIONINFO.txt` for the full environment (paste your `sessionInfo()` output).

## License

See `LICENSE` (add a license before publication; MIT is recommended for code).

## Citation

If you use this code, please cite the paper above. Archived release DOI: [Zenodo DOI to be added].
