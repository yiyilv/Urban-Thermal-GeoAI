# Unsupervised Mapping of Urban Thermal Environments

Team project for the ESA ESRIN Science Hub Challenges 2026. The analysis explores whether multi-source Earth observation variables can reveal urban surface and thermal patterns across Milan and Monza-Brianza, Italy, without prescribing land-cover classes in advance.

**Team:** Thomas Martinoli · Yiyi Cen · Sara Reffinetti, Politecnico di Milano  
**Study period:** June–August 2021  
**Analysis grid:** 100 m, EPSG:32632

> **Reproducibility status:** This repository contains a cleaned analysis notebook. The source rasters and AOI are not included, and the complete preprocessing chain is not yet packaged. The notebook has not been rerun from a clean environment with the original data.

## Research question

Can distinct urban thermal environments be identified from Earth observation data without defining the classes in advance?

## Data and method

The team combined Sentinel-2 Level-2A indicators (NDVI, NDRE, NDBI, BSI, MNDWI, and Albedo), Copernicus Land Monitoring Service (CLMS) 2021 Tree Cover Density and Imperviousness Density, and Landsat 8 Collection 2 Level-2 land-surface temperature. The nine bands were aligned to a common 100 m grid.

Cells with invalid values were excluded. Water was masked using MNDWI > 0.2. The eight non-water features were clipped to their 1st–99th percentile ranges, scaled to 0–1, and reduced with PCA. The analysis retained enough components to explain at least 90% of the variance, then compared K-means solutions at k=4, 6, and 9. The clusters were interpreted from their feature profiles and spatial patterns and compared descriptively with Local Climate Zones (LCZ).

The cleaned notebook expects a prebuilt nine-band GeoTIFF and an AOI GeoJSON. It performs the analysis and LCZ comparison; it does not download or build all source rasters.

## Findings reported by the project Webstory

- 197,836 valid 100 m cells were reported for the study area.
- PC1 explained 76.8% of variance and PC2 explained 8.1%.
- The k=4, 6, and 9 solutions describe progressively finer partitions along a broad vegetation-to-built-up and warmer-surface gradient.
- The LCZ comparison is descriptive, not a supervised classification accuracy assessment.

The temperature profiles are normalized relative values, not degrees Celsius. Results cover one summer and one study area; they do not establish year-to-year or cross-city stability.

## My contribution

Yiyi Cen authored the final Webstory narrative, explaining the research question, workflow, figures, cluster profiles, and LCZ comparison. The project notes reviewed for this portfolio do not establish individual responsibility for preprocessing, modeling, or figure production; those tasks are described as team work.

## Run the analysis notebook

The original analysis environment recorded Python 3.13.14, NumPy 2.5.1, Rasterio 1.5.0, GeoPandas 1.1.4, and scikit-learn 1.9.0. Install the listed dependencies, put the files in the locations described in [`data/README.md`](data/README.md), then start Jupyter from the repository root and run [`notebooks/urban_thermal_analysis.ipynb`](notebooks/urban_thermal_analysis.ipynb).

Set `URBAN_THERMAL_DATA_DIR` if your input data live outside the repository's `data/` directory. Set `URBAN_THERMAL_OUTPUT_DIR` to choose a different output folder. Generated maps and aligned LCZ data are written under `outputs/` by default.

## Data, attribution, and licensing

No source raster or model weight is bundled. Cite the original products and state when Copernicus inputs have been modified or aggregated; product-specific guidance and exact source links are listed in [`data/README.md`](data/README.md).

The Zenodo LCZ record did not display a license in its Rights section during this review. The LCZ raster is therefore an external user-supplied input and is not redistributed here. The project has no code license because this is a team work and the code reuse terms have not been agreed in the reviewed materials. Do not infer a reuse license from the repository being publicly viewable.

## Project story and figure credits

The available story URL is an ESA narrative pull-request preview and may change. Original Webstory figure sources and team attribution are recorded in [`FIGURE-CREDITS.md`](FIGURE-CREDITS.md).

## Limitations

- One summer, one study area, and a 100 m analysis grid.
- LST profiles are relative normalized values, not physical temperature differences.
- The LCZ cross-tabulation is an external descriptive comparison, not model accuracy.
- The full Sentinel-2, CLMS, and Landsat preprocessing chain is not included in this analysis-only package.
