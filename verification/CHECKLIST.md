# DAQIQ preservation checklist
Recorded before frontend edits.
- Original Phase 2 paths, H3 IDs, GeoJSON, summary, scores, rankings and classifications.
- Dataset phase, study area, cell count and generation metadata.
- Leaflet canvas, OSM tiles/credits, bounds, zoom and pan.
- Combined-score and tier colours from metadata; dynamic legend and all explanations.
- HIGH/MEDIUM/LOW filters, score threshold, visible/disagreement counts.
- Top 5/10/20 ranking, empty results, click-to-select and bounds.
- Map click, hover, mouseout, selected outline; filtered selection clears.
- H3 ID, centroid, tier, divergence badge, separate AHP/RF/combined metrics.
- Top three signed factors and all 13 SHAP contributions.
- Entrepreneur and Examiner views and all examiner fields.
- Disagreement threshold >100, markers from zoom 15, tooltip/click.
- Complete methodology, metrics, credits, WGS84 and pending comparison tables.
- Modal open/close/backdrop/Escape; loading/empty/error states.
- Original data/CDN/tile connections.

Redesign acceptance:
- Exact daqiq_logo.jpeg, original proportions/colours, relative GitHub Pages path.
- Responsive access to all controls/content.
- Disagreement overlay toggle retains original rules.
- Reset filters and clear selection.

Browser checks pending: visual layout at desktop/tablet/mobile, real map gestures,
all control/selection flows, scrolling, SHAP bars, modal keyboard focus, legend expansion,
deployed GitHub Pages logo/data/CDN/tile loading.
No browser connected. Automated adapters do not establish full acceptance.

The user subsequently supplied updated Phase 2 summary metadata. Its explicitly
approved hash is recorded in approved-metadata.json; original dataset and logo
hashes remain protected. The original baseline remains unchanged.
