# Flood-Risk-Assessment-MCDA.
An end-to-end geospatial pipeline for Multi-Criteria Flood Susceptibility Mapping in the Southern Region of Malawi. Developed using QGIS and the Analytic Hierarchy Process (AHP), this project integrates a 15-parameter matrix (DEM, LULC, TWI, NDVI) to model, analyze, and visualize high-impact regional flood vulnerability zones.

# Multi-Criteria Flood Susceptibility Mapping using AHP & QGIS
### 📍 Study Area: Southern Region of Malawi

## 📌 Project Overview
Flood events pose significant risks to human life, infrastructure, and the environment, making accurate assessment and mitigation strategies crucial. This repository contains an end-to-end geospatial intelligence pipeline designed to model, classify, and visualize regional flood vulnerability. 

By leveraging **QGIS** and Multi-Criteria Decision Analysis (MCDA) via the **Analytic Hierarchy Process (AHP)**, this study evaluates **15 distinct environmental, hydrological, and anthropogenic parameters**. The final output serves as a robust Spatial Decision Support System (SDSS) framework to drive evidence-based land use planning, emergency response strategies, and community resilience initiatives.

---

## 🗺️ Data Matrix & Preprocessing Pipeline

All layers were harmonized, clipped to the Southern Region boundary, resampled to uniform resolutions, and reprojected into the local projected coordinate system (**WGS 84 / UTM Zone 36S**) to preserve absolute distance and area properties.

| # | Parameter Dataset | Data Source | Spatial Resolution / Format | Primary Extraction Workflow |
| :--- | :--- | :--- | :--- | :--- |
| **1** | **Rainfall** | CHIRPS (2022)[cite: 2] | 4 km Raster[cite: 2] | Sourced & preprocessed via Google Earth Engine script blocks[cite: 2]. |
| **2** | **DEM** | SRTM USGS[cite: 2] | 30 m Raster[cite: 2] | Sourced from USGS Earth Explorer for topographic base boundaries[cite: 2]. |
| **3** | **Slope** | SRTM USGS[cite: 2] | 30 m Raster[cite: 2] | Extracted directly from base DEM via the QGIS Slope Tool[cite: 2]. |
| **4** | **Distance from Streams** | HOT OSM / AmeriGEOSS[cite: 2] | Polyline Shapefile[cite: 2] | Evaluated via Euclidean Distance tool using 5-tier proximity rings[cite: 2]. |
| **5** | **Distance from Roads** | DIVA-GIS[cite: 2] | Polyline Shapefile[cite: 2] | Processed using Euclidean Distance in kilometers across 5-tier buffers[cite: 2]. |
| **6** | **LULC Map** | Sentinel-2 Imagery[cite: 2] | 10 m Raster | Generated via Supervised Classification (Water, Forest, Agri, Veg, Built)[cite: 2]. |
| **7** | **TWI** | Derived from SRTM DEM[cite: 2] | 30 m Raster[cite: 2] | Modeled out of slope and upstream catchment accumulation dynamics[cite: 2]. |
| **8** | **Soil Type** | FAO GeoNetwork[cite: 2] | Polygon Shapefile[cite: 2] | Masked using study area boundaries and cross-referenced with FAO taxonomy[cite: 2]. |
| **9** | **NDVI** | Landsat-8 (USGS)[cite: 2] | 30 m Raster[cite: 2] | Computed using Red and NIR surface reflectance channels (Scale: -1 to 1)[cite: 2]. |
| **10** | **Drainage Density** | Hydrological DEM derivative[cite: 2] | 30 m Raster[cite: 2] | Computed via stream order extraction chained to Line Density tools[cite: 2]. |
| **11** | **Lineament Density** | Structural DEM derivative[cite: 2] | 30 m Raster[cite: 2] | Derived using multi-directional hillshades to calculate lineament vectors[cite: 2]. |

---

## 📊 AHP Criteria Weights & Influence Matrix

The mathematical relative importance of each parameter was determined using a Pairwise Comparison Matrix. The resulting weights are based on the principal eigenvector of the decision matrix. 

A rigorous validation check returned a **Consistency Ratio (CR) of 9.8%**. Because this falls safely below the maximum allowable threshold of **10% ($\le 0.10$)**, the matrix judgments are mathematically sound and reliable.

```text
       [ AHP PRIORITY RANKS & INFLUENCE COEFFICIENTS ]
       
 🥇 Topographic Wetness Index (TWI) ── 14.3%  ■■■■■■■■■■■■■■■
 🥈 Digital Elevation Model (DEM) ──── 14.1%  ■■■■■■■■■■■■■■
 🥉 NDVI (Vegetation Density) ──────── 11.0%  ■■■■■■■■■■■
 🏅 Distance from Streams ──────────── 10.1%  ■■■■■■■■■■
 🏅 Drainage Density ─────────────────  9.9%  ■■■■■■■■■
 🏅 Lineament Density ────────────────  7.3%  ■■■■■■■
 🏅 Rainfall Dynamics ────────────────  7.2%  ■■■■■■■
 🏅 Slope Runoff Velocity ────────────  7.1%  ■■■■■■■
 🏅 Soil Type Permeability ───────────  7.1%  ■■■■■■■
 🏅 Distance from Roads ──────────────  6.2%  ■■■■■■
 🏅 Land Use / Land Cover (LULC) ─────  5.7%  ■■■■■■
─────────────────────────────────────────────────────────────
 TOTAL INFLUENCE VALUE                100.0%
