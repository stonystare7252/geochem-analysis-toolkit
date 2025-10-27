
# Soil Geochemical Analysis & Mapping Pipeline

[![DOI](https://zenodo.org/badge/1084092410.svg)](https://doi.org/10.5281/zenodo.17454503)

This repository provides a **Jupyter Notebook workflow** for analyzing soil geochemical data and generating anomaly maps with sigma-based contour levels. The pipeline includes **unit standardization**, **robust variability metrics**, **element selection**, and a **cartographic module** for interpolation, smoothing, contour extraction, and export to **SHP** and **PNG**.

> **Note:** No raw geochemical data is included due to confidentiality. You must provide your own dataset and update the input path in the notebook.

---

## ✅ Key Features
- Unit conversion to **ppm** and column renaming for clarity.
- Robust variability metrics:
  - **Robust CV** (MAD/median)
  - **SD(log x)** for positive values
  - **Aitchison variance** on CLR-transformed data
- Element ranking and integrated selection.
- Correlation-based expansion of selected elements.
- Anomaly thresholds in log-space (μ + 2σ) and 95th percentile.
- Full mapping pipeline:
  - Winsorization in log-space
  - Convex hull + buffer (+200 m) with soft boundary
  - Grid interpolation (cubic/linear fallback) and Gaussian smoothing (~60 m)
  - Sigma-level generation and rounding
  - Polygon extraction with holes preserved
  - Geometric rounding + Chaikin smoothing
  - Export to **ESRI Shapefile** and **PNG maps**

---

## 🔒 Data Privacy & Input Configuration
This repository does **NOT** include any proprietary datasets.

To run the pipeline:
1. Prepare your own soil assay CSV with:
   - Coordinates: `x`, `y` (projected CRS, meters)
   - Element columns: e.g., `Cu_ppm`, `Au_ppb`, `Al_pct`
2. Place the file under `./data/raw/` or any preferred location.
3. Update the path in the first block:
   ```python
   DATA_DIR = Path("C:/YourFolder")
   INPUT_CSV = Path("./data/raw/your_dataset.csv")
4. Define mineralization types and associated elements in Block 13 (optional).
5. Define list of elements and rounding steps for plotting/export in Block 15.
6. Set coordinate system in Block 16
7. Adjust other parameters in Config (buffer size, smoothing radius, grid size).
8. Ensure output directories exist (created automatically if missing)
