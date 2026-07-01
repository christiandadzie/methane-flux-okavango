# Methane Flux Prediction Across the Okavango Delta

This project uses global FLUXNET wetland tower data to train a Random Forest model predicting monthly methane (CH4) flux, then applies the model spatially to map seasonal emission patterns across the Okavango Delta — one of Africa's largest and most carbon-significant wetland ecosystems.

---

## Results

| Methane Flux Prediction | pH Raster |
|---|---|
| ![Predicted Methane Flux](images/methane_flux_prediction.jpg) | ![pH Raster](images/ph_raster.jpg) |

| Soil Organic Carbon | Mean Temperature |
|---|---|
| ![SOC Raster](images/soc_raster.jpg) | ![Temperature Raster](images/temperature_raster.jpg) |

---

## Project Structure

```
methane-flux-okavango/
├── data/
│   └── ChristianDadzie_MODELDATA.RDATA   # FLUXNET training dataset
├── Okavango.shp/                          # Okavango Delta boundary shapefile
├── Spatial Model Data/                    # Cropped raster inputs for spatial prediction
│   ├── Soil_Organic_Carbon_5cm_Okavango.tif
│   └── pH_5cm_Okavango.tif
├── MORSEDADZIE_RFMODEL.RDATA             # Saved trained Random Forest model
├── random_forest_model.Rmd               # Script 1: Train the RF model on FLUXNET data
├── spatial_prediction.Rmd                # Script 2: Apply model spatially across the Delta
└── images/                               # Output figures
```

---

## Workflow

**Script 1 — `random_forest_model.Rmd`**
Loads the FLUXNET CH4 dataset, cleans and bins predictors (soil organic carbon, temperature, pH), trains a Random Forest model, evaluates on a held-out test set, and saves the fitted model to `MORSEDADZIE_RFMODEL.RDATA`.

**Script 2 — `spatial_prediction.Rmd`**
Loads the saved model and three spatial raster layers (SOC, pH, temperature from TerraClimate), generates monthly CH4 flux predictions across the Okavango Delta for 2018–2021, then summarises wet-season and dry-season budgets with spatial means, sums, and standard errors.

---

## Dependencies

```r
install.packages(c("randomForest", "tidyverse", "GGally",
                   "sf", "terra", "climateR", "rmapshaper"))
```

---

## Data Sources

- **FLUXNET CH4** — Global wetland tower flux measurements  
- **TerraClimate** — Monthly temperature data downloaded via `climateR`  
- **SoilGrids** — Soil organic carbon and pH rasters clipped to the Okavango Delta  
- **Okavango Delta boundary** — Shapefile defining the area of interest
