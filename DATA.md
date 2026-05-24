# Input data

The raw geodata is large and redistributed under the licences of its providers, so it is **not** included in this repository. Download the datasets below and place them under `./Data/` following the layout the notebooks expect. Intermediate outputs (e.g. the suitability GeoTIFF) are written to `./Sripts/Output/`.

All layers are reprojected to the **British National Grid (EPSG:27700)** inside the notebooks.

| Layer | Criterion | Source | Notes |
|---|---|---|---|
| Wind speed (150 m) | C1 | [Global Wind Atlas](https://globalwindatlas.info/) | GeoTIFF raster |
| Road network | C2 | [Geofabrik / OpenStreetMap](https://download.geofabrik.de/europe/great-britain.html) | `gis_osm_roads_free_1.shp` per nation |
| Transmission lines | C3 | National Grid / ENA open data | high-voltage line geometries (GeoJSON) |
| Land cover (urban) | C4 | [UKCEH Land Cover Map 2024](https://www.ceh.ac.uk/data/ukceh-land-cover-maps) | 10 m raster (GB + NI) |
| Terrain slope | C5 | SRTM (e.g. via [OpenTopography](https://opentopography.org/)) | derived slope raster |
| Protected areas | C6 | [JNCC](https://jncc.gov.uk/) SAC / SPA | GB + NI shapefiles |
| Grid congestion | C7 | DESNZ *Clean Power 2030* / Ofgem | regional score (1–5), set in notebook 01 |
| Existing wind & PV | exclusion | [DESNZ Renewable Energy Planning Database](https://www.gov.uk/government/collections/renewable-energy-planning-database-monthly-extract) | excluded with a 600 m buffer |
| UAS / aviation zones | exclusion | CAA UAS restriction-zone XML | partial exemptions (HIGHLANDS, RPAS CORRIDOR, NORTHERN COMPLEX) |

## Expected folder layout

```
Data/
├── Wind Speed/                 # GBR_wind-speed_150m*.tif
├── Road Network/<nation>-*.shp/gis_osm_roads_free_1.shp
├── Transmission Lines/         # *.geojson
├── Land use/                   # gblcm2024_10m.tif, nilcm2024_10m.tif
├── Slopes/                     # w001001.adf (GB), NI/*.tif
├── Protected Areas/            # GB SAC, GB SPA, NI SAC, NI SPA
├── UAS/                        # *.xml aviation restriction zones
├── Current Wind Mills/         # Current Wind mills.csv
└── Current PV/                 # *.geojson per region

Sripts/Output/                  # written by the notebooks (e.g. UK_Final_Suitability_Score.tif)
```

> The exact buffer distances, allowed land-use classes and regional congestion scores are defined at the top of `01_suitability_map.ipynb` and can be adjusted there.
