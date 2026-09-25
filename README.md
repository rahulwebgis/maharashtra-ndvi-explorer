# Maharashtra NDVI Explorer

A browser-only WebGIS for vegetation and drought monitoring over Maharashtra. It computes NDVI from **Sentinel-2 L2A (10 m)** and **Landsat 8/9 Collection 2 Level-2 (30 m)**, streamed live from Microsoft Planetary Computer. It needs no login, no API key and no server.

## Features
- Date A / Date B calendar showing which days have imagery over your area, with a cloud-cover limit
- NDVI or true-colour map tiles with a chosen colour ramp and scale, plus swipe compare
- **District → Taluka → Village** area selection from built-in boundaries: 36 districts, 351 talukas and 45,316 villages with LGD codes. Village files load one district at a time. Users can replace any layer with their own zipped Shapefile or GeoJSON
- Draw a polygon, rectangle or circle, or import your own boundary
- Pixel analysis reads the image files directly and masks cloud:
  - Sentinel-2 cloud and shadow classes (SCL 3, 8, 9, 10)
  - Landsat cloud, dilated-cloud and shadow flags (QA_PIXEL bits 1, 3, 4)
- Dashboard: mean, median and P5–P95 NDVI, clear and cloud %, vegetation classes, histogram, and ΔNDVI loss / stable / gain
- Table and map of NDVI change for each taluka or village
- Exports:
  - Float32 GeoTIFFs of A, B and ΔNDVI in WGS84, with .tfw and .prj files
  - Stats CSV and sub-area GeoJSON
  - Map PNG and a print layout as PDF, PNG or JPG

## Publish on GitHub Pages
1. Create a repository, for example `maharashtra-ndvi-explorer`, and upload `index.html`, `README.md` and the whole `data/` folder with the same structure (38 files, none over 5 MB).
2. Go to Settings → Pages → Deploy from branch → `main` / root.
3. Open `https://<username>.github.io/maharashtra-ndvi-explorer/`.

## Data
- Copernicus Sentinel-2 L2A (ESA) and USGS Landsat Collection 2 Level-2, via Microsoft Planetary Computer
- Boundaries: `data/districts.geojson`, `data/talukas.geojson` and `data/villages/<district>.geojson`, converted from MH_DISTRICT, MH_TALUKA and MH_VILLAGE (reprojected from EPSG:3857 to WGS84 and lightly simplified).
- If the `data/` folder is missing, districts fall back to Census 2011 ([udit-001/india-maps-data](https://github.com/udit-001/india-maps-data)).
- To test locally, run `python -m http.server` in the folder. Browsers block loading the `data/` files when you open `index.html` directly from disk.

Map created by Rahul Gawai.
