# Input data (not included in this repository)

Obtain the following inputs and replace the scripts' `/path/to/` placeholders with their locations.

1. Proof-of-concept (PoC) DKD Visium ST
   - GEO: GSE211785 (Abedini et al., Nat Genet 2024).
   - Used by analysis/03_PoC_DKD.Rmd.
   - The analysis uses raw Space Ranger outputs provided by the original study authors
     for six DKD samples: HK2529_ST, HK2844_ST, HK2873_ST, HK2877_ST,
     HK3035_ST, and HK3437_ST.
   - Each sample requires filtered_feature_bc_matrix.h5 and the corresponding spatial/
     directory. Set the sample-specific paths in SR_DIRS.
   - Spots that fail QC are removed before downstream analysis. Pseudobulk counts
     are aggregated from the raw Spatial counts.

2. KPMP DKD and HKD Visium ST (10x Space Ranger 'outs' per sample)
   - https://atlas.kpmp.org
   - Used by analysis/01_KPMP_DKD.Rmd and analysis/02_KPMP_HKD.Rmd.

3. KPMP single-cell RNA-seq reference atlas (KPMP_ref.h5ad)
   - Lake et al., Nature 2023; used for label-transfer deconvolution
     (MAC.M2 prediction score) in all cohorts.
