# Explainable Spatial AI for Urban Retail Site Selection
## An AHP–SHAP Audit with WebGIS Delivery in Milan

This repository contains the code, data-processing workflow, analytical outputs, and WebGIS developed for a master's thesis at **Politecnico di Milano**.

The project studies **café location suitability in the Municipality of Milan** by comparing two independent approaches:

- **AHP (Analytic Hierarchy Process):** an expert-driven multi-criteria suitability model.
- **Random Forest (RF):** a data-driven classifier trained on observed café-location patterns.

The key contribution is the use of **SHAP (SHapley Additive exPlanations)** to audit whether the feature importance learned by the Random Forest agrees with the weights assigned through AHP.

In simple terms, the thesis asks:

> **Do AHP and Random Forest identify the same places as suitable?**  
> **And do they agree on why those places are suitable?**

---

## Study Area and Spatial Unit

The analysis covers the **Municipality of Milan** using an **H3 Resolution 9 hexagonal grid**.

- Total candidate cells: **1,743**
- Viable cells after land-use filtering: **971**
- Canonical viability threshold: **20% overlap with acceptable urban land uses**
- Positive RF label: **at least 2 OSM-mapped cafés within a cell**

The viability mask is derived from **Copernicus Urban Atlas 2021** and removes areas where café-oriented ground-floor retail activity is not comparable to the target urban fabric.

---

## Data Sources

The workflow integrates open spatial data from:

- **OpenStreetMap (OSM):** cafés, POIs, streets, transit and urban-network information
- **Copernicus Urban Atlas 2021:** land-use classification and viability filtering
- **ISTAT 2021:** population data
- **VIIRS 2024:** night-light intensity as an activity-demand proxy

---

## Methodology

```text
Open spatial data
      ↓
Cleaning + spatial harmonisation
      ↓
H3 Resolution 9 grid
      ↓
Urban Atlas viability filter
      ↓
Spatial feature engineering
      ↓
 ┌───────────────┬─────────────────┐
 │      AHP      │  Random Forest  │
 │ Expert-driven │   Data-driven   │
 └───────┬───────┴────────┬────────┘
         │                │
         │              SHAP
         │                │
         └────── Audit ───┘
                  ↓
              WebGIS
```

### AHP layer

The AHP model uses four Level 1 clusters:

- **Accessibility:** 37.6%
- **Demand Potential:** 30.0%
- **Urban Context:** 25.3%
- **Competition:** 7.0%

The Level 1 pairwise-comparison matrix achieved a **Consistency Ratio of 0.0175**, well below the conventional 0.10 threshold.

### Random Forest layer

The Random Forest uses **13 engineered spatial features** and predicts the probability that an H3 cell belongs to the positive class.

The target represents **observed café co-presence**, not business profitability or survival.

### SHAP audit

SHAP explains the Random Forest and allows its learned feature-importance ranking to be compared with the AHP effective weights.

The formal feature-level comparison uses the **10 features shared by AHP and RF**.

---

## Main Results

### Random Forest performance

- Held-out validation **AUC: 0.9510**
- Accuracy: **0.8481**
- Recall: **0.9343**
- 5-fold cross-validation AUC: **0.9462 ± 0.0211**

### AHP vs Random Forest: cell level

The two scoring surfaces show a high raw Spearman correlation:

**ρ = 0.7937**

However, the permutation test indicates that this apparent similarity is **not distinguishable from agreement induced by shared spatial structure**.

### AHP vs SHAP: feature level

The feature rankings show no statistically meaningful agreement:

**ρ = -0.4073**  
**Permutation p = 0.2412**

AHP prioritises accessibility-related factors, while the Random Forest gives much greater importance to **local café density** and **POI diversity**.

The main conclusion is therefore not that one method is superior, but that the two approaches capture **different forms of knowledge** and are more useful as complementary decision-support layers.

---

## WebGIS

The project includes an interactive WebGIS for exploring suitability across Milan at the H3-cell level.

It allows users to inspect:

- AHP suitability scores
- Random Forest probabilities
- combined suitability information
- local SHAP explanations
- the features that most influenced each RF prediction

**Live application:** https://hafizwebuilder.github.io/DAQIQ/

The interface is intended as an **exploratory decision-support and research tool**, not as a predictive oracle for choosing a real business location.

---

## Reproducibility

The project follows a reproducibility-first workflow.

Key elements include:

- pinned Python dependencies in `requirements.txt`
- a **Bronze → Silver → Gold** geospatial data pipeline
- CRS and geometry validation
- explicit H3-ID consistency checks across final analytical layers
- fixed model random seeds
- notebook-based processing from ingestion to WebGIS delivery

Install dependencies with:

```bash
pip install -r requirements.txt
```

Then run the project notebooks in their numerical pipeline order.

---

## Important Limitations

This project should not be interpreted as a direct predictor of café profitability.

Important limitations include:

- OSM café presence is a **proxy**, not verified business survival, revenue, or footfall
- OSM completeness may vary spatially
- the analysis is cross-sectional and does not establish causality
- the `≥ 2 cafés` label favours already established café clusters
- AHP reflects a **single-analyst expert prior**
- Level 2 AHP sub-weights were directly assigned rather than independently pairwise-validated
- rent, operating costs, customer behaviour and real pedestrian-flow data are not included
- local café density creates a potential circularity concern, although model performance remains strong when it is removed

---

## Thesis

**Title:** *Explainable Spatial AI for Urban Retail Site Selection: An AHP–SHAP Audit with WebGIS Delivery in Milan*

**Authors:**
- Miguel Angel Avila Santos
- Hafizullah Sarwary

**Institution:** Politecnico di Milano  
**Academic Year:** 2025–2026

---

## Keywords

`Spatial AI` · `AHP` · `Random Forest` · `SHAP` · `WebGIS` · `H3` · `GeoAI` · `Retail Site Selection` · `Milan` · `Explainable AI`
