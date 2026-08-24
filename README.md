<!-- BEFORE YOU PUBLISH — quick checklist (this comment block is invisible on GitHub): 1. Replace every [BRACKETED] placeholder. 2. Fill in the Findings section with your real numbers — don't ship it empty. 3. Add 2–3 exported maps to /maps and update the image links. 4. Set your GitHub handle in the contact + any links. 5. Confirm the license you want (MIT is a safe default for a portfolio). 6. Delete this comment block last, once everything checks out. -->
Baldwin County Civic GIS — Development Pressure & Social Vulnerability

A spatial analysis of how development pressure and social vulnerability overlap in Baldwin County, Alabama. Built from open federal and state datasets using QGIS, Python, and SQL, with a reproducible, documented workflow.

Status: [Complete / In progress] · Author: Jacob Harvison · Focus: civic & environmental spatial analysis

Overview

This project asks a simple question with real local stakes: where does new development pressure land relative to the communities least equipped to absorb its impacts?

To look at it spatially, I integrated two independent public datasets — a social vulnerability index and demographic data — and joined them to census geographies so the layers could be compared on common ground. A proposed planned-unit development footprint was digitized and added as a case study in siting.

The goal was not just a map but a repeatable pipeline: every layer is sourced, every transformation is scripted or documented, and the analysis can be regenerated from the raw downloads.

Study Area

Baldwin County, Alabama — [briefly note the specific corridor/area of focus, e.g. the CR-13 / Daphne area]. Analysis performed in EPSG:26916 (NAD83 / UTM zone 16N) for accurate distance and area measurement.

Data Sources
Layer	Source	Vintage	Notes
Social Vulnerability Index (SVI)	CDC/ATSDR	2022	Census-tract level; RPL_THEMES used for the overall percentile
Demographic composition	U.S. Census ACS (table B02001)	[year]	Joined at block-group level; percent-composition fields derived
Census geographies	U.S. Census TIGER/Line	[year]	Tracts and block groups
Zoning reference	[source / county]	[year]	Georeferenced raster used for context
Pedestrian network	OpenStreetMap	[pull date]	Sidewalks / paths for accessibility context
Proposed development footprint	Manually digitized from [source]	—	~[134]-acre proposed PUD

This table doubles as the project's data dictionary — keep it accurate and current.

Methods
Acquisition. Downloaded each dataset from its authoritative source (links above) into data/raw/.
Cleaning & standardization. Reprojected all layers to EPSG:26916, validated geometries, and standardized join keys (GEOID).
Integration. Joined ACS demographic fields and SVI scores to census block groups / tracts on GEOID.
Derived measures. Calculated [e.g. percent-composition fields — list what you actually computed].
Cartography. Produced choropleth maps of SVI and demographic composition with the development footprint overlaid.
QA/QC. Checked join completeness (no dropped GEOIDs), verified CRS consistency, and confirmed totals against published Census/ATSDR figures.

The scripted portions live in scripts/; the interactive cartography and georeferencing were done in the QGIS project in qgis/.

Key Outputs

Show Image [One-line caption: what this map shows and the takeaway.]

Show Image [One-line caption.]

Findings

Fill this in with your real results — this section is what a reviewer reads first. Keep it factual and measured; let the data speak.

[Finding 1 — e.g. how SVI is distributed across the study corridor.]
[Finding 2 — e.g. how the proposed development footprint relates to vulnerable block groups.]
[Finding 3 — any notable spatial pattern or absence of one.]

Limitations. [Note honest caveats: ecological-inference limits of tract/block-group analysis, ACS margins of error, digitization uncertainty on the footprint, etc.]

Reproduce It
bash
# clone and set up
git clone https://github.com/jacobharvison/baldwin-county-civic-gis.git
cd baldwin-county-civic-gis
python -m venv .venv && source .venv/bin/activate
pip install -r requirements.txt

# run the analysis pipeline
python scripts/build_analysis.py

Large raw datasets are not committed; see the source links above (or data/raw/README.md) for download instructions.

Repository structure
baldwin-county-civic-gis/
├── README.md
├── requirements.txt
├── data/
│   ├── raw/          # source downloads (git-ignored; see download notes)
│   └── processed/    # cleaned, reprojected, joined outputs
├── scripts/          # Python: acquisition, cleaning, joins, QA/QC
├── qgis/             # QGIS project + styles
├── maps/             # exported figures (PNG)
└── docs/
    └── methods.md    # extended methodology
Tech Stack

GIS: QGIS · Language: Python (geopandas, pandas, shapely), SQL Data: U.S. Census / ACS, CDC/ATSDR SVI, OpenStreetMap, TIGER/Line Practices: EPSG:26916 analysis CRS, GEOID joins, version control, documented QA/QC

License

[MIT] — see LICENSE. Data remain subject to their original providers' terms.

Contact

Jacob Harvison · Jacobharvison327@gmail.com · github.com/jacobharvison
