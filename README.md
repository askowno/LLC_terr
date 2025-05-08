## Land cover change and ecosystem condition analyses (terrestrial)

### National Biodiversity Assessment - South Africa

South African National Biodiversity Institute (SANBI)

May 2025

### Step 1: National land cover change data 

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
N[national mask] --_optional_step--> L;
L--> O(Summarise lc7_rall.csv or sa_lc7_rall.csv);
```

### Step 2: Supplementary land cover and ecosystem condition data 

Land cover and ecosystem condition products prepared by provincial or metropolitan environmental authorities and major region environmental programmes have high confidence estimates and, due to their more local focus and extensive error correction and validation steps. Where available these data are used in conjunction with national data sets to estimate remaining extent of selected ecosystem types and to estimate the extent (required for Criterion A) and severity of functional declines (required for Criterion D).

``` mermaid
flowchart LR

subgraph A1[Worflow]
    A[Western Cape LC] -- reclass in ARCPRO --> B(wc_lc3.tif) -- load to R terra --> K(Stack);
    C[Mpumalanga LC] -- reclass in ARCPRO --> D(mpl_lc3.tif) -- load to R terra --> K;
    E[KwaZulu-Natal LC] -- reclass in ARCPRO --> F(kzn_lc2.tif) -- load to R terra --> K --> L(CrossTab & summarise outputs/alt_sum.csv);
    G[City of Cape Town LC/Cond] -- reclass in ARCPRO --> H(coct_cond10.tif) -- load to R terra --> N(CrossTab & summarise outputs/coct_sum.csv);
    I[Nelson Mandela Metro Cond] -- reclass in ARCPRO --> J(nmb_lcdeg2.tif) -- load to R terra --> O(CrossTab & summarise outputs/nmb_sum.csv);
    P[STEP Cond] -- reclass in ARCPRO --> R_step(step_deg2.tif) -- load to R terra --> Q(CrossTab & summarise outputs/step_sum.csv);
    P1[Little Karoo Thompson Cond] -- reclass in ARCPRO --> R1_lk(littlekaroo_deg4.tif) -- load to R terra --> Q1(CrossTab & summarise outputs/lk_sum.csv);
    P2[Little Karoo Kirsten Cond] -- reclass in ARCPRO --> R2_lkk(lk_kirsten.tif) -- load to R terra --> Q2(CrossTab & summarise outputs/lkk_sum.csv);
    P3[Hardeveld Cond] -- reclass in ARCPRO --> R3_hv(hv_bell.tif) -- load to R terra --> Q3(CrossTab & summarise outputs/hv_sum.csv);
end


subgraph Y []
        M[National Vegetation Map 2024] --> L & N & O & Q & Q1 & Q2 & Q3;
end
```

### 

#### i) Alternative Western Cape, Mpumalanga and KwaZulu-Natal land cover

[WC_KZN_MPL_LC.qmd](WC_KZN_MPL_LC.qmd)

1.  Western Cape Provincial Land Cover (supplied by Cape Nature, 2022). Data supplied in ESRI GRID format, converted to a TIFF in ARCGIS PRO, 10 m data (UTM34S) resampled to match 20m and Albers Equal Area national land cover grid. Reclassified to match the NLC classes.

2.  KwaZulu-Natal Provincial Land Cover (supplied by Ezemvelo KZN Wildlife, 2017). Data supplied in ESRI gdb format, converted to a TIFF in ARCGIS PRO, 20 m data (UTM35S) resampled to match 20m and Albers Equal Area national land cover grid. Reclassified to match the NLC classes.

3.  Mpumalanga Provincial Land Cover (supplied by MPTA, 2017). Data supplied in ESRI gdb format, converted to a TIFF in ARCGIS PRO, 20 m data (UTM35S) resampled to match 20m and Albers Equal Area national land cover grid. Reclassified to match the NLC classes.

4.  National Land Cover (7 class version prepared by SANBI) 2022.

5.  National Vegetation Map 2024 version, vector data (ESRI file geodatabase) January 2025 curated by SANBI (Dayaram et al., 2019; Mucina and Rutherford 2006).

*The ecosystem data (vegetation types), NLC, WC, KZN and MPL data were cross tabulated and then summarised to assess Criterion A3 of the IUCN RLE.* Results [outputs/alt_sum.csv](outputs/alt_sum.csv)

#### ii) City of Cape Town land cover and ecosystem condition

[CoCT_LC_Condition.qmd](CoCT_LC_Condition.qmd)

City of Cape Town Biodiversity Network (supplied by CoCT, 2024). Data supplied in ESRI gdb format, converted to a TIFF in ARCGIS PRO, unprojected vector data rasterized and to match 20m and Albers Equal Area national land cover grid. Reclassified to match the NLC 7class, with severely degraded areas (referred to as "poor" condition in source data) given value = 8 and estimated to have severity of \>80%. Impacts occurred more than 50 years ago.

*The ecosystem data (vegetation types), and NLC and CoCT data were cross tabulated and then summarised to assess Criterion A3 and D3 of the IUCN RLE.* Results [outputs/coct_sum.csv](outputs/coct_sum.csv)

#### iii) Nelson Mandela Bay Metro land cover and ecosystem condition

[NMB_Condition.qmd](NMB_Condition.qmd)

Nelson Mandela Bay degradation data (supplied by Stewart et al., 2015) (prepared in ARCGIS PRO, 8 = severely degraded class from NMB degradation, 4 = builtup, 0 = unknown). Class 8 (degradation) is estimated to be equivalent to 80% severity on RLE Criterion D - factors include overgrazing / browsing, fuel wood collection, bush clearing (to promote grazing), resulting in severe reduction in natural tree or shrub cover, changes in species composition (palatable species usually dominant have been lost), increase in bare ground fraction (with soil loss). Impacts occurred more than 50 years ago.

*The ecosystem data (vegetation types), and NLC and NMB data were cross tabulated and then summarised to assess Criterion A3 and D3 of the IUCN RLE.* Results [outputs/nmb_sum.csv](outputs/nmb_sum.csv)

#### iv) Subtropical Ecosystem Project (STEP) thicket ecosystem condition

[STEP_Condition.qmd](STEP_Condition.qmd)

Sub Tropical Ecosystem Project (STEP) Thicket degradation layer ([Lloyd et al., 2002](https://www.researchgate.net/profile/Anthony-Palmer-6/publication/229078462_Patterns_of_Transformation_and_Degradation_in_the_Thicket_Biome_South_Africa/links/0c960525fad8d20b86000000/Patterns-of-Transformation-and-Degradation-in-the-Thicket-Biome-South-Africa.pdf)) (prepared in ARCGIS PRO, 8 = severely degraded class from STEP.) This class is estimated to be equivalent to 80% severity on RLE Criterion D - factors include overgrazing / browsing resulting in severe reduction in shrub canopy cover, changes in species composition (loss of P. afra and other palatable species usually dominant), increase in bare ground fraction (with soil loss). Impacts occurred more than 50 years ago, and subtropical thicket does not recover naturally over time - rather it enters a alternative stable state - an arid shrubland dominated by Asteraceae typical of the Nama Karoo biome.

*The ecosystem data (vegetation types), and NLC and STEP data were cross tabulated and then summarised to assess Criterion D3 of the IUCN RLE.* Results [outputs/step_sum.csv](outputs/step_sum.csv)

#### v) Little Karoo ecosystem condition (Thompson)

[LK_Condition.qmd](LK_Condition.qmd)

Little Karoo degradation map developed in 2009 ([Thompson et al., 2009](https://doi.org/10.1007/s00267-008-9228-x)). The severely degraded class from this data is estimated to be equivalent to 80% severity on RLE Criterion D - factors include overgrazing / browsing resulting in severe reduction in shrub canopy cover, changes in species composition (loss of palatable species usually dominant), increase in bare ground fraction (with soil loss). Most impacts occurred more than 50 years ago, and in this arid region the shrubland does not recover naturally over time - rather it enters an alternative stable state - bare ground with annual grass and herbs following rainfall events - limited perennial cover).

*The ecosystem data (vegetation types), and NLC and Little Karoo data were cross tabulated and then summarised to assess Criterion D1 and D3 of the IUCN RLE.* Results for Little Karoo [outputs/lk_sum.csv](outputs/lk_sum.csv).

#### vi) Hardeveld degradation study and ecosystem condition 

[Hardeveld_Condition.qmd](Hardeveld_Condition.qmd)

The Hardeveld Bioregion degradation map developed in 2021 ([Bell, et al. 2021](https://doi.org/10.1002/ldr.3900)). The severely degraded class (degradation archetype = Well Below Average) was estimated to be equivalent to 80% severity on RLE Criterion D - factors include overgrazing / browsing resulting in severe reduction in shrub canopy cover, changes in species composition (loss of palatable species usually dominant), increase in bare ground fraction (with soil loss). Most impacts occurred more than 50 years ago, and in this arid region the perrenial shrub cover recover readily, rather it enters an alternative stable state - bare ground with annual grass and herbs following rainfall events).

*The ecosystem data (vegetation types), and NLC and Hardeveld data were cross tabulated and then summarised to assess Criterion D3 of the IUCN RLE.* Results for Hardeveld [outputs/hv_sum.csv](outputs/hv_sum.csv).

#### vii) Little Karoo degradation study and ecosystem condition (Kirsten)

[LittleKaroo_Kirsten_Condition.qmd](LittleKaroo_Kirsten_Condition.qmd)

The Little kroo degradation map developed in 2023 ([Kirsten, et al. 2023](https://doi.org/10.1016/j.jaridenv.2023.105066)). The severely degraded class (degradation archetype = Well Below Average) was estimated to be equivalent to 80% severity on RLE Criterion D - factors include overgrazing / browsing resulting in severe reduction in shrub canopy cover, changes in species composition (loss of palatable species usually dominant), increase in bare ground fraction (with soil loss). Most impacts occurred more than 50 years ago, and in this arid region the perrenial shrub cover recover readily, rather it enters an alternative stable state - bare ground with annual grass and herbs following rainfall events).

*The ecosystem data (vegetation types), and NLC and Little Karoo (Kirsten) data were cross tabulated and then summarised to assess Criterion D3 of the IUCN RLE.* Results for Little Karoo (Kirsten data) [outputs/lkk_sum.csv](outputs/lkk_sum.csv).

#### viii) Miscelaneous expert inputs on ecosystem condition for specific vegetation units

1.  Supplementary assessment testimony from Cape Nature (Annalize Schutte Vlok) and independant botanist Jan Vlok for the vegetation unit (SKv11) Eastern Little Karoo. The assessment was based on extensive field surveys and historical aerial photographs. Severely overgrazed / browsed / trampled areas (severity of \> 80%), with evidence that the degradation occurred in the last 50 years (Criterion D1). The supplementary data and information demonstrates that the degree of biotic disruption and loss of cover severely impairs the ability of he ELK vegetation to naturally regenerate. **The supplementary assessment (2020) resulted in an RLE status of Endangered (D1) for ELK.** Further data available from SANBI.

2.  Supplementary longterm field data and testimony from Jurgens and XXX on Richterveld vegetation units (REF), provided the basis for assessments of X Y Z
