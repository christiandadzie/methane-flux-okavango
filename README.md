# Mapping Methane Across the Okavango Delta

Wetlands are among the largest natural sources of methane on Earth, yet we still have limited tools for estimating how much they actually emit, and when. This project set out to change that, at least for one extraordinary place. The Okavango Delta in Botswana is a vast inland wetland that floods seasonally, shifts between wet and dry phases, and sits at the heart of one of the most biodiverse ecosystems in Africa. It is also one of the least studied in terms of greenhouse gas emissions.

*Lead analyst: Christian Dadzie | Environmental Data Science, Yale School of the Environment, Fall 2024 | Group project with Dylan Morse*

---

## The Question

Can a machine learning model trained on global wetland data predict spatial and seasonal patterns of methane flux across the Okavango Delta, and if so, what do those patterns reveal about wet versus dry season emissions?

---

## The Approach

We trained a Random Forest model on FLUXNET CH4 data: a global dataset of methane flux measurements from eddy covariance towers installed at wetland sites around the world. The model learned relationships between methane emissions and three environmental drivers: soil organic carbon content, soil pH, and mean air temperature.

Once trained, we applied the model spatially, feeding it raster layers of each predictor variable cropped and aligned to the Okavango Delta boundary. This produced monthly predictions of methane flux (in g C m-2 month-1) across every pixel of the Delta from December 2018 through November 2021, covering three full seasonal cycles.

We then grouped predictions into wet seasons (December through April) and dry seasons (May through November) for each year, and computed spatial sums, means, and standard errors to estimate the Delta's total seasonal methane budget.

![Predicted monthly methane flux across the Okavango Delta. Warmer colors indicate higher predicted emissions.](images/methane_flux_prediction.jpg)

---

## What the Data Showed

Methane emissions from the Okavango Delta vary meaningfully by season. Dry seasons consistently produced slightly higher total flux estimates than wet seasons, a pattern that may reflect higher soil temperatures and organic matter decomposition rates during drier months, even as inundation extent decreases.

| Year | Wet Season Total Flux (GT C) | Dry Season Total Flux (GT C) |
|------|-------------------------------|-------------------------------|
| 2019 | 0.263 | 0.332 |
| 2020 | 0.258 | 0.335 |
| 2021 | 0.261 | 0.329 |

The spatial pattern was also consistent across years: emissions were highest in the permanently flooded inner Delta and lowest at the drier margins, reflecting the strong role of soil organic carbon and temperature in driving flux predictions.

---

## Input Raster Layers

The three spatial predictors used in the model:

| Soil Organic Carbon | Soil pH (Categorized) | Mean Air Temperature |
|---|---|---|
| ![SOC Raster](images/soc_raster.jpg) | ![pH Raster](images/ph_raster.jpg) | ![Temperature Raster](images/temperature_raster.jpg) |

---

## Data and Tools

| Component | Source |
|-----------|--------|
| Methane flux training data | FLUXNET CH4 global wetland tower dataset |
| Soil organic carbon (0-5 cm) | SoilGrids (ISRIC World Soil Information) |
| Soil pH (0-5 cm, categorized) | SoilGrids |
| Air temperature (monthly) | TerraClimate via `climateR` |
| Delta boundary | Okavango Delta shapefile |
| Modeling | Random Forest (`randomForest`) |
| Spatial processing | `terra`, `sf`, `rmapshaper` |
| Analysis environment | R (R Markdown) |

---

## Project Structure

```
methane-flux-okavango/
├── data/
│   └── ChristianDadzie_MODELDATA.RDATA   # FLUXNET training dataset
├── Okavango.shp/                          # Okavango Delta boundary
├── Spatial Model Data/                    # Cropped raster inputs
├── MORSEDADZIE_RFMODEL.RDATA             # Saved trained RF model
├── random_forest_model.Rmd               # Script 1: Model training
├── spatial_prediction.Rmd                # Script 2: Spatial application
└── images/                               # Output figures
```
