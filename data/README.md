# Input data (not included in this repository)

Download the following and point the scripts' `/path/to/` paths here.

1. Susztak/Abedini DKD Visium ST
   - GEO: GSE211785  (Abedini et al., Nat Genet 2024)
   - Used by analysis/03_Susztak_Lab_DKD.Rmd (Seurat object HK.ST.NG.rds in the
     original analysis; six DKD samples: HK2529, HK2844, HK2873, HK2877, HK3035, HK3437).

2. KPMP DKD and HKD Visium ST (10x Space Ranger 'outs' per sample)
   - https://atlas.kpmp.org
   - Used by analysis/01_KPMP_DKD.Rmd and analysis/02_KPMP_HKD.Rmd.

3. KPMP single-cell RNA-seq reference atlas (KPMP_ref.h5ad)
   - Lake et al., Nature 2023; used for label-transfer deconvolution
     (MAC.M2 prediction score) in all cohorts.
