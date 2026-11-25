# FCS Cytometry Viewer — v5.28

A self-contained, single-file flow cytometry analysis tool. Open `fcs_viewer_v5.28.html` in any modern web browser and drag FCS files onto the drop zone — no installation, no account, no server, and no data ever leaves your machine.

**Designed for rapid bookending of batch data**: load an entire run at once, gate once, apply to all samples, and read a whole-batch table of common qualitative measures in minutes.

---

## Quick Start

1. Open `fcs_viewer_v5.28.html` in Chrome, Edge, Firefox, or another modern browser.
2. Drag one or more FCS files (or a whole folder's worth) onto the drop zone at the top.
3. Pick a sample from the dropdown, choose two channels, and start plotting.
4. Draw a gate, click **apply to all**, then open the **Batch Analysis** tab for the whole-run table.
5. Export results to CSV or Excel, or copy plots straight to the clipboard.

> Internet is only needed the first time per session for the Excel-export library (SheetJS, loaded from a CDN). Everything else works fully offline.

## Supported Files

- **FCS 2.0 and FCS 3.0** list-mode files, including multi-dataset files (`$NEXTDATA`)
- Data encodings: `$DATATYPE` I (binary integer), F (float), D (double float), both byte orders
- Channel names, labels, bit depths, ranges, and amplifier settings are read from the file
- Auxiliary files: instrument **log files** (Guava-style), **voltage/settings** exports (XML, JSON, or delimited text)

## The Four Tabs

### Scatter / Dot Plot
- Interactive two-parameter plots for any channel pair
- **Density shading** to resolve high-event regions
- Per-channel scaling: **linear, log, or biexponential** (auto-selected by default)
- Live statistics for the current gate: count, mean, median, SD, percentiles

### Histogram
- Single-parameter histograms with **multi-sample overlay**
- Per-sample color pickers, adjustable axis and legend sizing

### 3-Plot Gating
- Up to three linked bivariate panels on one screen for serial gating strategies
- **Box, lasso (free-form), and polygon** gates on each panel
- Shared controls and apply-to-all propagation

### Batch Analysis
- Runs the current gating/statistics over **every loaded file** at once
- Sortable whole-batch table: percent gated, event counts, fluorescence, cell density
- Per-sample control normalization and sticky offsets
- Export the full table or gated events to CSV/Excel

## Gating

- Draw **box, lasso, or polygon** gates directly on plots; events are assigned per-event (point-in-polygon)
- **Apply gate to all samples** in one click — the core batch operation
- Gates persist in browser local storage and reload with the same files
- Gate coordinates can be exported for reporting and reuse
- **Numeric cutoffs** (thresholds on a channel value) can be applied across all samples and panels — useful for counting-style assays and dilution series

## Metadata Reconciliation

FCS Viewer checks the conditions under which data were acquired, not just the data:

- **Plate positions** — auto-detected from filenames or FCS metadata; manual override available
- **Sample volumes** — auto-detected or entered, with unit selection
- **Cell density** — computed as events per volume, with warning states for inconsistent inputs
- **Flow rate** — computed from the FCS time parameter and cross-checked against the instrument log; disagreements are flagged
- **Voltages** — loaded from settings exports or extracted from FCS files; compared across samples with mismatch highlighting
- **Instrument logs** — matched to loaded samples by data/settings file name, with a visible warning when a log matches no sample

## Export

- **CSV and Excel (.xlsx)** export with selectable columns, scope (all events or gated events), and event caps
- Optional inclusion of gate coordinates, well positions, and voltage metadata in exports
- Batch result tables and batch gate exports (events passing gates)
- **Copy current plot — or all plots — to clipboard** for instant pasting into documents and slides

## Tips

- Use the sample **filter box** above the dropdown to quickly narrow a large plate to the wells of interest.
- Keep gates consistent across a batch by drawing once and using **apply to all**, then spot-checking outliers in the scatter tab.
- If flow-rate or voltage warnings appear, check the flagged samples before trusting batch percentages — those warnings usually indicate an acquisition problem, not a data problem.
- Gates live in browser local storage: use the same browser profile to keep them, and clear saved gates when starting a new experiment.

## Known Limitations (v5.28)

- No compensation / spillover correction — best for one- and two-color reporter and counting assays
- Transforms are linear/log/biexponential only (no logicle or hyperlog yet)
- Instrument log parsing is Guava-specific; other vendors' logs are not yet recognized
- No Gating-ML import/export; gate sharing is via coordinate export
- Figures export via clipboard (no vector SVG/PDF output yet)

## Version

**v5.28** — current release. See the paper *FCS Viewer: A Single-File Tool for Rapid Bookending Analysis of Flow Cytometry Batch Data* for design rationale, comparisons with Floreada.io and Omiq, and the development roadmap.
