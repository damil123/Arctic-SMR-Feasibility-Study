# Arctic SMR Feasibility Study

**Author:** Damil Randhawa

A data-driven feasibility analysis of Small Modular Reactors (SMRs) for remote Arctic and Subarctic communities in Canada, evaluating whether nuclear microreactors can replace diesel generation as the primary energy source.

## Summary

Remote communities across Canada's Arctic rely almost entirely on diesel generators for electricity — an expensive, carbon-intensive, and logistically fragile energy supply chain. This project pulls real data from three government sources to quantify the energy gap that renewables cannot fill and evaluates whether SMRs offer a viable alternative.

### Key Findings

- **Renewables fall critically short year-round.** NASA climate data for central Arctic Canada (68°N) shows that solar and wind combined never exceed 6% of baseline demand in any month. All 12 months flag as "nuclear critical" under a 40% renewable reliability threshold.
- **Arctic diesel communities consume a median of 12.9 kWh per person per day**, derived from 53 diesel-powered communities in Nunavut, NWT, and Yukon after excluding industrial mine sites.
- **Tiered SMR sizing** matches reactor capacity to community scale — micro (0.5 MW / $30M) for small settlements like Resolute (pop. 183), small (2 MW / $75M) for mid-size towns like Inuvik (pop. 3,137), and standard (5 MW / $150M) for larger centres like Whitehorse (pop. 28,201).
- **SMRs are cost-competitive with diesel over a 20-year horizon** for most communities, with levelized costs of energy (LCOE) ranging from $327–$588/MWh for SMR versus a uniform $675/MWh for diesel at $2.50/L delivered.
- **Resolute remains a challenging case** — its tiny population means even the smallest microreactor is oversized, pushing LCOE to ~$1,878/MWh. Shared regional infrastructure or multi-community microgrids could address this.

## Data Sources & APIs

| Source | What It Provides | Access Method |
|--------|-----------------|---------------|
| **NASA POWER API** | Monthly solar irradiance (ALLSKY_SFC_SW_DWN), wind speed (WS10M), and temperature (T2M) for 2015–2024 | REST API — JSON format, `https://power.larc.nasa.gov/api/temporal/monthly/point` |
| **Statistics Canada Census 2021** | Population counts by census subdivision (Table 98-10-0002) | CSV zip download, `https://www150.statcan.gc.ca/n1/tbl/csv/98100002-eng.zip` |
| **NRCan Remote Communities Energy Database (RCED)** | Diesel generation capacity, annual fossil fuel generation (MWh), population, and fuel type for 276 remote communities | ArcGIS REST API query, `https://geoappext.nrcan.gc.ca/arcgis/rest/services/FGP/remote_communities_2018_en/MapServer/0/query` |

## Communities Analyzed

| Community | Province | Population | Zone | Reactor Class |
|-----------|----------|-----------|------|---------------|
| Iqaluit | NU | 7,429 | High Arctic | Standard (5 MW) x2 |
| Inuvik | NT | 3,137 | High Arctic | Small (2 MW) |
| Resolute | NU | 183 | High Arctic | Micro (0.5 MW) |
| Yellowknife | NT | 20,340 | Subarctic | Standard (5 MW) x4 |
| Whitehorse | YT | 28,201 | Subarctic | Standard (5 MW) x5 |

## Methodology

1. **Climate data collection** — Pulled 10 years of monthly solar, wind, and temperature data from NASA POWER for a central Arctic reference point (68°N, 110°W).
2. **Renewable Energy Reliability Score (RERS)** — Calculated monthly renewable generation potential using standard panel efficiency (18%) and turbine coefficients, expressed as a fraction of a 1 MW baseline.
3. **Demand baseline** — Derived per-capita energy consumption from NRCan's RCED, filtering to 53 diesel-dependent communities in northern territories. Used the median (12.9 kWh/person/day) to avoid skew from industrial outliers.
4. **Population matching** — Merged 2021 Census population data with community coordinates and RCED demand baselines.
5. **Reactor sizing** — Calculated the nuclear gap (baseline demand minus winter renewable output) with a 1.3x safety margin, then matched each community to an appropriately sized SMR tier.
6. **Cost comparison** — Computed 20-year total cost and LCOE for both diesel ($2.50/L, 270 L/MWh) and SMR (capital + $30/MWh O&M) scenarios.

## Visualizations

All charts are saved to the `charts/` folder at 300 DPI:

| File | Description | Slide |
|------|-------------|-------|
| `01_community_map.png` | Geographic map of 5 communities, sized by population, colored by zone | The Problem |
| `02_monthly_rers.png` | 12-month RERS bar chart showing renewable shortfall vs nuclear threshold | The Renewable Gap |
| `03_demand_nuclear_gap.png` | Horizontal bars comparing annual demand vs nuclear gap per community | Energy Demand |
| `04_cost_comparison.png` | Grouped bars — diesel vs SMR 20-year cost with payback annotations | Cost Showdown |
| `05_lcoe_comparison.png` | LCOE comparison with Canadian grid average reference line | Unit Economics |
| `06_summary_table.png` | Dashboard table summarizing all metrics across communities | Recommendation |

## Assumptions & Limitations

- **SMR costs are estimates** — capital costs ($30M–$150M per unit) are based on publicly available projections for microreactor designs (e.g., BWXT, Ultra Safe Nuclear MMR). Actual costs will depend on regulatory approval, construction logistics, and first-of-a-kind premiums.
- **Diesel price of $2.50/L** is conservative for fly-in Arctic communities, where delivered fuel can reach $3–4/L. Higher diesel prices strengthen the SMR case.
- **RCED data is from 2018** — community generation figures may have changed, but the overall pattern of diesel dependence in remote Arctic communities remains consistent.
- **Single climate reference point** — NASA POWER data was pulled for one central Arctic location (68°N, 110°W). Individual communities would have slightly different solar/wind profiles, though the overall Arctic renewable shortfall pattern holds across all sites.
- **The analysis does not account for** transmission infrastructure, regulatory/licensing timelines, community consultation requirements, waste management costs, or decommissioning.

## Tech Stack

- Python 3, Jupyter Notebook
- pandas, matplotlib, numpy
- requests (API calls)
- Data: NASA POWER API, Statistics Canada, NRCan RCED (ArcGIS REST)

## License

This project is for academic and research purposes.
