# DAQIQ WebGIS

Explainable GeoAI for Urban Retail Site Selection in Milan.

## Project files

- index.html: application interface
- styles.css: responsive layout and styling
- app.js: map controls and analytical presentation
- daqiq_logo.png: official DAQIQ logo
- data/phase2/gold_webgis_layer.geojson: active H3 layer, scores and SHAP values
- data/phase2/gold_webgis_summary.json: active dataset and methodology metadata

All local asset and data paths are relative for GitHub Pages project hosting.

## Run locally

Serve this directory with Live Server, or run:

    python -m http.server 8000

Then open http://localhost:8000. Opening index.html directly with file:// blocks
the data requests. Leaflet and OpenStreetMap tiles require an internet connection.

## Features

- H3 map with combined-score and suitability-tier colouring and metadata-driven legend
- Live suitability filters, minimum score, counts and Top 5/10/20 rankings
- Cell selection, separate AHP/RF/combined indicators and all supplied SHAP factors
- Entrepreneur and Thesis/Examiner views
- AHP-RF disagreement markers for rank_diff > 100 at zoom level 15 or above
- Differences overlay toggle, reset filters and clear selection
- Selection-only details overlay above the continuous map
- Methodology panel with supplied metrics, configuration and source credits

## Metadata limitations

The frontend reads the supplied Phase 2 metadata; missing fields retain the
existing fallback messages. The separate Validation AUC row expects
methodology.rf.validation_auc_reported. The existing Phase 1 summary AUC label
currently displays model_performance.rf_auc_validation from the active summary.
Consistency ratio, feature-level agreement and credits need the corresponding
methodology fields. Sensitivity and AHP-vs-SHAP tables remain original placeholders.

## Cleanup verification

Fourteen automated preservation check groups passed before removing the
development verification files and unused Phase 1 copies. All six runtime files
were checked for byte-for-byte integrity during cleanup. Full interactive browser
acceptance remains pending; the automated checks used DOM/Leaflet adapters.

JavaScript syntax can be checked with:

    node --check app.js
