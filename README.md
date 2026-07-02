# Mapping Methane Across the Okavango Delta

Wetlands are the largest natural source of methane on Earth, but measuring emissions across vast, remote landscapes at scale is not practical. This project asks whether a model trained on global flux data can predict where and when methane is released across one of Africa's most significant wetland ecosystems.

*Lead analyst: Christian Dadzie | Environmental Data Science, Yale School of the Environment, Fall 2024 | Group project with Dylan Morse*

![Predicted monthly methane flux across the Okavango Delta. Warmer colors indicate higher predicted emissions.](images/methane_flux_prediction.jpg)

*Predicted monthly methane flux across the Okavango Delta. Warmer colors indicate higher predicted emissions.*

---

## The Question

Where is methane being released across the Okavango Delta, and do emissions peak in the wet season or the dry season?

---

## The Approach

The project has two parts. First, a Random Forest model was trained on monthly flux observations from the global FLUXNET network, a system of measurement towers deployed across wetland ecosystems worldwide. The model uses three predictors: soil organic carbon, air temperature, and soil pH, each of which influences the microbial activity that drives methane production.

Once trained, the model was applied spatially across the Okavango Delta using raster layers derived from global soil and climate datasets. This produced monthly maps of predicted methane flux across the full extent of the delta for a three-year period (2019 to 2021), chosen to avoid strong El Nino and La Nina cycles that could distort seasonal patterns.

---

## What the Data Shows

We expected wet season emissions to be higher. The literature consistently supports this, and intuition follows: more water, more anaerobic decomposition, more methane.

The model disagreed. Dry season flux was higher in every year of the study period.

| Year | Wet Season Total Flux (GT) | Dry Season Total Flux (GT) |
|------|---------------------------|---------------------------|
| 2019 | 0.263 | 0.332 |
| 2020 | 0.258 | 0.335 |
| 2021 | ... | ... |

The explanation lies in pH. Permanently flooded areas in the Okavango have high soil organic carbon, which should support methane production. But they also have low, acidic pH, which inhibits the microbial processes that produce methane. Seasonal floodplains, by contrast, have more moderate pH and become active methane sources when flooded in the dry season. pH, not organic carbon, was the dominant driver in the model.

---

## Data and Tools

R, randomForest, terra, sf, tidyverse

| Dataset | Source |
|---------|--------|
| Methane Flux Observations | FLUXNET CH4 Network |
| Soil Organic Carbon | SoilGrids (ISRIC) |
| Air Temperature | TerraClimate |
| Soil pH | SoilGrids (ISRIC) |
| Okavango Boundary | Gumbricht (2019) via ArcGIS |
