# The onset of the 2026 El Niño: wind bursts, Kelvin waves and zonal advection

Analysis code for the study of the 2026 El Niño onset (July 2025 – September 2026) and its drought and fire impacts in Indonesia. The study uses open reanalysis and satellite data in Google Colab, Google Earth Engine and the Copernicus Marine Service.

- **Authors:** Muhammad Ghifari Shafa (ORCID [0009-0009-9693-7968](https://orcid.org/0009-0009-9693-7968)) and Farisya Isnaayu Khairunisa (ORCID [0009-0001-8107-1630](https://orcid.org/0009-0001-8107-1630)), Le-GIS, Jakarta, Indonesia
- **Paper:** Shafa, M.G. and Khairunisa, F.I., *Wind bursts, Kelvin waves and zonal advection: the onset of the 2026 El Niño and its drought and fire impacts in Indonesia, from reanalysis and satellite observations*. In preparation for the *International Journal of Climatology*.
- **Interactive summary:** https://le-gis.com/project/elnino/
- **Code:** https://github.com/layered-earth/enso2026-onset
- **Archived version:** [10.5281/zenodo.23981889](https://doi.org/10.5281/zenodo.23981889) (v1.0.0)

## Main results

| Finding | Value | Notebook |
| --- | --- | --- |
| Kelvin wave speed (satellite altimetry, crest tracking) | 2.5–3.2 m/s, median 3.0 m/s | 07 |
| Altimetric sea level vs GLORYS12 thermocline depth | r = 0.86 | 07 |
| ASCAT wind bursts vs ERA5 | r = 0.93 | 07 |
| Niño-3 warming, March–September 2026 | +4.0 °C | 06 |
| Zonal advective / thermocline feedback / advection by mean currents | +2.6 / +2.6 / +2.7 °C | 06 |
| Zonal advection from satellite data only | +2.4 °C | 06 |
| Indonesian rainfall, June–September 2026 (IMERG / CHIRPS) | −42% / −48% | 07 |
| MODIS fires, 1 June – 24 October 2026 | 15,251; 3.5× the 2001–2020 mean | 07 |
| Forced component of tropical-mean warming (regression, Supporting information) | +0.37 °C (0.28–0.46) | 04 |

## Notebooks

Run them in this order. Each notebook caches its downloads on Google Drive, so later runs are much faster.

| # | Notebook | What it does | Data and accounts | First run |
| --- | --- | --- | --- | --- |
| 01 | `01_indices_indonesia_rainfall.ipynb` | Niño indices from OISST and the Indonesian rainfall anomaly (CHIRPS) | Earth Engine | short |
| 02 | `02_trigger_wind_bursts_kelvin_waves.ipynb` | Detects westerly wind bursts, predicts Kelvin-wave arrivals, and builds the equatorial Hovmöller diagrams and the thermocline section | Earth Engine, Copernicus Marine | medium |
| 03 | `03_event_comparison_synthesis.ipynb` | Compares 1997, 2015, 2023 and 2026 (indices, thermocline, IOD, RONI) and exports `events_aligned.json` | Earth Engine, Copernicus Marine | medium |
| 04 | `04_ocean_physics_forcing.ipynb` | Stratification, thermocline-feedback strength, upwelling indices, forced background warming, and the 3D ocean data for the website | Earth Engine, Copernicus Marine | long |
| 06 | `06_mixed_layer_heat_budget.ipynb` | 0–50 m heat budget split into feedbacks, eddy heat flux, and the satellite check of zonal advection | Earth Engine, Copernicus Marine | long |
| 07 | `07_satellite_evidence_figures.ipynb` | Altimetry (Kelvin waves), ASCAT winds, IMERG vs CHIRPS rainfall, MODIS fires, paper Figures 1 and 4, and `Supplementary_Tables.xlsx` (Tables S1–S4) | Earth Engine, Copernicus Marine | 45–90 min |

Notebook 05 (a CMIP6 attribution attempt) is not included. The public cloud archive held too few suitable models for a robust result, and the paper does not use it.

### Figures in the paper

| Paper | File | Notebook |
| --- | --- | --- |
| Fig. 1 | `Fig1_sst_map` | 07 |
| Fig. 2 | `F_winds_scatterometer` | 07 |
| Fig. 3 | `F_altimetry_kelvin` | 07 |
| Fig. 4 | `Fig4_event_comparison` (needs `events_aligned.json` from 03) | 07 |
| Fig. 5 | `AB_feedback_budget` | 06 |
| Fig. 6 | `C_satellite_check` | 06 |
| Fig. 7 | `F_rainfall_imerg_chirps` | 07 |
| Fig. 8 | `F_fires` | 07 |
| Fig. S1 | `step5_forcing` | 04 |
| Table 2 | `AB_event_budget.csv` | 06 |
| Tables S1–S4 | `Supplementary_Tables.xlsx` | 07 (needs 06 first) |
| Text S1, Table S5 | `step5_forcing_validation.csv` | 04 |

## Setup

1. **Google Earth Engine:** register a Cloud project for Earth Engine (free for non-commercial use) and put its ID in the settings cell of each notebook (`PROJECT` or `EE_PROJECT = "YOUR-EE-PROJECT"`).
2. **Copernicus Marine:** create a free account at marine.copernicus.eu. The notebooks ask for your username and password once per session. Nothing is stored in the notebooks.
3. **Google Drive:** results and caches go to `MyDrive/le-gis_enso/` (`cache/` and `web/`). To use another folder, change `ROOT` in the settings cell.
4. Open the notebooks in Google Colab and run each from the top. The first cell installs the packages it needs. `requirements.txt` lists the versions used.

## Notes on method

- Heat budget: monthly tendencies use centred differences; the last available month uses a backward difference, so the observed change covers the same months as the budget terms.
- Fire counts: MODIS (Terra/Aqua) active fires, confidence ≥ 50%, 1 June to the latest available day of each year.

## Data

All data are openly available. Please cite the original providers:

- **ERA5** (ECMWF / Copernicus Climate Change Service; Hersbach et al., 2020): via Earth Engine
- **GLORYS12** reanalysis and global analysis/forecast (Copernicus Marine; Lellouche et al., 2021)
- **NOAA OISST v2.1** (Huang et al., 2021): via Earth Engine
- **DUACS L4 sea level** (Copernicus Marine; Pujol et al., 2016)
- **ASCAT L3 and blended L4 winds** (Copernicus Marine)
- **GlobCurrent surface currents** (Copernicus Marine, MULTIOBS_GLO_PHY_MYNRT_015_004; Rio et al., 2014)
- **CHIRPS v2.0** (Funk et al., 2015) and **GPM IMERG V07** (Huffman et al., 2023): via Earth Engine
- **MODIS active fires, NASA FIRMS** (Giglio et al., 2016): via Earth Engine
- **FAO GAUL 2015** administrative boundaries: via Earth Engine

Values for 2026 come from near-real-time products, which their providers revise when the reprocessed versions are released.

## Citation

If you use this code, please cite the paper and this repository (see `CITATION.cff`).

## License

Code: MIT License (see `LICENSE`). The data remain under their providers' licences.

## Acknowledgement

An AI assistant (Claude, Anthropic) helped write and test the analysis code. The authors checked all code and results.
