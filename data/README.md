# Input data

Place inputs under this directory, or set URBAN_THERMAL_DATA_DIR to a separate data root. Large source data are intentionally not committed.

## Required analysis inputs

```text
data/
├── aoi/
│   └── AOI_Milan_Monza.geojson
├── processed/
│   └── FEATURES_JJA2021_100m_AOI_Milan_Monza.tif
└── external/
    └── lcz_filter_v1.tif
```

The feature stack must be a nine-band GeoTIFF in this order, with matching band descriptions:

1. NDVI
2. NDRE
3. NDBI
4. BSI
5. MNDWI
6. ALBEDO
7. TCD
8. Imperviousness
9. LST

The stack must use a 100 m grid in EPSG:32632 and align with the AOI. The notebook uses the first existing filename in processed/; the _bbox variant is also accepted. The AOI must be supplied in GeoJSON format.

The LCZ input is the lcz_filter_v1.tif reference product from [Zenodo record 6364594](https://doi.org/10.5281/zenodo.6364594). The record describes a global 100 m LCZ map, but its Rights section did not expose a license during this review. Check the record's current terms before downloading or redistributing it. Do not commit the 1.4 GB global raster; the notebook reads only the study-area window and writes an aligned local derivative to outputs/maps/.

## Original product sources and attribution

- [Copernicus Sentinel-2 Level-2A](https://documentation.dataspace.copernicus.eu/Data/Sentinel2.html). When communicating modified derivatives, use the Copernicus notice “Contains modified Copernicus Sentinel data 2021.”
- [CLMS Tree Cover Density 2021, 10 m](https://land.copernicus.eu/en/products/high-resolution-layer-forests-and-tree-cover/tree-cover-density-2021-raster-10-m-100-m-europe-yearly), DOI [10.2909/e677441e-fb94-431c-b4f9-304f10e4dfd8](https://doi.org/10.2909/e677441e-fb94-431c-b4f9-304f10e4dfd8).
- [CLMS Imperviousness Density 2021, 10 m](https://land.copernicus.eu/en/products/high-resolution-layer-imperviousness/imperviousness-density-2021), DOI [10.2909/34ef6334-d432-4041-a3da-67e156d6501d](https://doi.org/10.2909/34ef6334-d432-4041-a3da-67e156d6501d).
- [USGS Landsat 8 Collection 2 Level-2 Surface Temperature](https://www.usgs.gov/landsat-missions/landsat-collection-2-surface-temperature), DOI [10.5066/P9OGBGM6](https://doi.org/10.5066/P9OGBGM6). USGS identifies Landsat products as public domain; retain source citation.
- [Global Local Climate Zone map](https://doi.org/10.5281/zenodo.6364594), Demuzere et al. (2022). Do not redistribute until its current license is confirmed.

CLMS requires users who distribute or communicate its data or derived products to identify the source and state when the data were adapted. Do not imply official EU endorsement.
