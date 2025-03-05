## Land cover change and ecosystem condition analyses (terrestrial)

### National Biodiversity Assessment - South Africa

South African National Biodiversity Institute (SANBI)

February 2025

### National Land Cover Change

Land cover change spatial analysis for the 2025 National Biodiversity Assessment is based on the cross-tabulation of land cover change data and maps of potential vegetation (terrestrial ecosystem types).

##### Input data:

1.  National Land Cover 7 class version (prepared by SANBI) for 1990, 2014, 2018, 2020 and 2022 (based on National Land Cover products served by the Department of Forestry Fisheries and the Environment).

2.  National Vegetation Map 2024 version, vector data (ESRI file geodatabase) released in January 2025 by SANBI (Dayaram et al., 2019; Mucina and Rutherford 2006).

The ecosystem data (vegetation types) and the NLC data for each time point were cross tabulated in R terra and then summarised. Two versions of this analysis were developed. a) Including South Africa, Lesotho and Eswatini [LC_change_7class_veg24.qmd](LC_change_7class_veg24.qmd) for use in Red List of Ecosystems assessments - these require full ecosystem extent; b) South Africa only [LC_change_7class_veg24_SAonly.qmd](LC_change_7class_veg24_SAonly.qmd) for the Ecosystem Area Index and national statistics - these require only the South African extent of each ecosystem type

The outputs of these analyses ([outputs/sa_lc7_rall.csv](outputs/sa_lc7_rall.csv) and [outputs/lc7_rall.csv](outputs/lc7_rall.csv)) form the basis of workflows in the RLE_terr and EAI_terr Repos.

``` mermaid
flowchart LR
A[NLC 1990 DFFE]--reclass in ARCPRO--> B(nlc1990_7class.tif) --load to R terra--> K(Stack); 
C[NLC 2014 DFFE]--reclass in ARCPRO--> D(nlc2014_7class.tif) --load to R terra--> K(Stack); 
E[NLC 2018 DFFE]--reclass in ARCPRO--> F(nlc2018_7class,tif) --load to R terra--> K(Stack);
G[NLC 2020 DFFE]--reclass in ARCPRO--> H(nlc2020_7class.tif) --load to R terra--> K(Stack);
I[NLC 2022 DFFE]--reclass in ARCPRO--> J(nlc2022_7class.tif) --load to R terra--> K(Stack);
K--> L(Cross-tabulate);
M[National Vegetation Map 2024] --load and make raster --> L;
N[national mask] --optional_step--> L;
L--> N(Summarise lc7_rall.csv or sa_lc7_rall.csv);
```

### Supplementary land cover and ecosystem condition data from conservation authorities and regional programmes

Land cover and ecosystem condition products prepared by provincial or metropolitan environmental authorities and major region environmental programmes have high confidence estimates and, due to their more local focus and extensive error correction and validation steps. Where available these data are used in conjunction with national data sets to estimate remaining extent of selected ecosystem types and to estimate the extent (required for Criterion A) and severity of functional declines (required for Criterion D).

#### Alternative Western Cape, Mpumalanga and KwaZulu-Natal land cover

[WC_KZN_MPL_LC.qmd](WC_KZN_MPL_LC.qmd)

1.  Western Cape Provincial Land Cover (Cape Nature, 2022). Data supplied in ESRI GRID format, converted to a TIFF in ARCGIS PRO, 10 m data (UTM34S) resampled to match 20m and Albers Equal Area national land cover grid. Reclassified to match the NLC classes.

2.  KwaZulu-Natal Provincial Land Cover (Ezemvelo KZN Wildlife, 2017). Data supplied in ESRI gdb format, converted to a TIFF in ARCGIS PRO, 20 m data (UTM35S) resampled to match 20m and Albers Equal Area national land cover grid. Reclassified to match the NLC classes.

3.  Mpumalanga Provincial Land Cover (MPTA, 2017). Data supplied in ESRI gdb format, converted to a TIFF in ARCGIS PRO, 20 m data (UTM35S) resampled to match 20m and Albers Equal Area national land cover grid. Reclassified to match the NLC classes.

4.  National Land Cover (7 class version prepared by SANBI) 2022.

5.  National Vegetation Map 2024 version, vector data (ESRI file geodatabase) January 2025 curated by SANBI (Dayaram et al., 2019; Mucina and Rutherford 2006).

*The ecosystem data (vegetation types), NLC, WC, KZN and MPL data were cross tabulated and then summarised to assess Criterion A3 of the IUCN RLE.* Results [outputs/alt_sum.csv](outputs/alt_sum.csv)

#### City of Cape Town land cover and ecosystem condition

[CoCT_LC_Condition.qmd](CoCT_LC_Condition.qmd)

City of Cape Town Biodiversity Network (CoCT, 2024). Data supplied in ESRI gdb format, converted to a TIFF in ARCGIS PRO, unprojected vector data rasterized and to match 20m and Albers Equal Area national land cover grid. Reclassified to match the NLC 7class, with severely degraded areas (referred to as "poor" condition in source data) given value = 8 and estimated to have severity of \>80%. Impacts occurred more than 50 years ago.

*The ecosystem data (vegetation types), and NLC and CoCT data were cross tabulated and then summarised to assess Criterion A3 and D3 of the IUCN RLE.* Results [outputs/coct_sum.csv](outputs/coct_sum.csv)

#### Nelson Mandela Bay Metro land cover and ecosystem condition

[NMB_Condition.qmd](NMB_Condition.qmd)

Nelson Mandela Bay degradation data (Stewart et al., 2015) (prepared in ARCGIS PRO, 8 = severely degraded class from NMB degradation, 4 = builtup, 0 = unknown). Class 8 (degradation) is estimated to be equivalent to 80% severity on RLE Criterion D - factors include overgrazing / browsing, fuel wood collection, bush clearing (to promote grazing), resulting in severe reduction in natural tree or shrub cover, changes in species composition (palatable species usually dominant have been lost), increase in bare ground fraction (with soil loss). Impacts occurred more than 50 years ago.

*The ecosystem data (vegetation types), and NLC and NMB data were cross tabulated and then summarised to assess Criterion A3 and D3 of the IUCN RLE.* Results [outputs/nmb_sum.csv](outputs/nmb_sum.csv)

#### Subtropical Ecosystem Project thicket ecosystem condition

[STEP_Condition.qmd](STEP_Condition.qmd)

Sub Tropical Ecosystem Project (STEP) Thicket degradation layer (Lloyd et al., 2002) (prepared in ARCGIS PRO, 8 = severely degraded class from STEP.) This class is estimated to be equivalent to 80% severity on RLE Criterion D - factors include overgrazing / browsing resulting in severe reduction in shrub canopy cover, changes in species composition (loss of P. afra and other palatable species usually dominant), increase in bare ground fraction (with soil loss). Impacts occurred more than 50 years ago, and subtropical thicket does not recover naturally over time - rather it enters a alternative stable state - an arid shrubland dominated by Asteraceae typical of the Nama Karoo biome.

*The ecosystem data (vegetation types), and NLC and STEP data were cross tabulated and then summarised to assess Criterion D3 of the IUCN RLE.* Results [outputs/step_sum.csv](outputs/step_sum.csv)

#### Little Karoo ecosystem ecosystem condition

[LK_Condition.qmd](LK_Condition.qmd)

1.  Little Karoo degradation map developed in 2009 (Thompson et al., 2009). The severely degraded class from this data is estimated to be equivalent to 80% severity on RLE Criterion D - factors include overgrazing / browsing resulting in severe reduction in shrub canopy cover, changes in species composition (loss of palatable species usually dominant), increase in bare ground fraction (with soil loss). Most impacts occurred more than 50 years ago, and in this arid region the shrubland does not recover naturally over time - rather it enters an alternative stable state - bare ground with annual grass and herbs following rainfall events - limited perennial cover).

2.  Note - SANBI recieved detailed information and supplementary assessment testimony from Cape Nature (Annalize Schutte Vlok) and independant botanist Jan Vlok for Vegetation unit (SKv11) Eastern Little Karoo. the assessment was based on extensive field surveys and aerial photographs. Severely overgrazed / browsed / trampled areas (severity of \> 80%), with evidence (aerial photos) that the degradation occurred in the last 50 years (Criterion D1). The supplementary data and information demonstrates that the degree of biotic disruption and loss of cover severely impairs the ability of he ELK vegetation to naturally regenerate. **The supplementary assessment (2020) resulted in an RLE status of Endangered (D1) for ELK.** Further data available from SANBI.

*The ecosystem data (vegetation types), and NLC and Little Karoo data were cross tabulated and then summarised to assess Criterion A3 and D3 of the IUCN RLE.* Results for Little Karoo [outputs/lk_sum.csv](outputs/lk_sum.csv).
