# Data Quality Report — Dehradun–Mussoorie Landslide Risk Tool (Phase 2)

**Date Generated:** 2026-11-19  
**Study Corridor:** Dehradun–Mussoorie State Highway (SH-01; ~35 km PWD chainage / 30.01 km OSM driving length from Dehradun Clock Tower to Mussoorie Library Chowk) and alternate corridors (SH-79 Kimadi route, NH-707A/NH-507 Kempty–Yamuna Pul–Vikasnagar route, and Sahastradhara/Maldevta–Suwakholi approach).  
**Core Principle:** Strict evidence traceability and zero fabrication. Every record traces to a verified primary news, Uttarakhand PWD/ULMMC, OpenStreetMap/OSRM, ECMWF, NASA POWER, or IMD/WMO source. Unknown values are preserved as `null` (empty CSV cells).

---

## 1. Headline Quantitative Metrics

| Metric | Baseline (Phase 1) | Updated (Phase 2) | Net Change / Details |
|---|---:|---:|---|
| **Documented SH-01 Monsoon Events (2023–2026)** | 6 | **34** | **+28 additional verified events** (2023: 7, 2024: 8, 2025: 6, 2026: 13) |
| **Historical Road Closure / Disruption Records** | 5 | **33** | **+28 additional records** (`full_closure`: 23, `partial_closure`: 4, `one_way_traffic`: 3, `temporary_traffic_disruption`: 3; 1 off-roadway Jharipani subsidence event has no SH-01 closure) |
| **Records with Confirmed Durations** | ~3–4 approximate | **16 / 34 events** (`16 / 33` closures) | **17 closure records** with unreported exact durations strictly preserved as `null` |
| **Verified Geospatial Coordinates** | 0 / 7 | **20 / 21 features** (**6 / 7** original features) | 18 direct OSM/ULMMC/gazetteer verified on/near road + 2 PWD chainage-interpolated points on OSM SH-01 (`LOC-004` km 19, `LOC-010` km 21); **1 feature (`LOC-005` Hanuman Temple)** kept `null` at pinpoint level and linked to `SEG-SH01-05` |
| **Road Segments Defined & Linked** | 0 | **12 segments** | 100% of events (34/34), closures (33/33), and features (21/21) linked to a verified `road_segment_id` |
| **Historical Rainfall Observations Downloaded (Raw)** | 0 (inventory only) | **79,028 raw observations** | ECMWF IFS ~9 km: **45,216** hourly (3 cells × 4 seasons); ECMWF ERA5 0.25°: **15,072** hourly; NASA POWER MERRA-2: **15,264** hourly; IMD Dehradun WMO 42111: **932** GSOD daily (2023–2025) + **2,544** Ogimet SYNOP messages (2023–2026) |
| **Exported Event & Non-Event Rainfall Windows** | 0 | **232 summary rows** | **34 events + 24 comparable non-event monsoon dates** (13 high-rain non-events + 11 baseline monsoon non-events) × 4 downloaded sources; plus **10,948** hourly + monsoon daily station rows in `historical_rainfall_hourly_corridor.csv` |
| **Alternative Route Geometries Validated** | 0 lineworks | **5 GeoJSON LineStrings** | Main SH-01 (30.01 km), Kimadi SH-79 (40.69 km), Kempty–Yamuna Pul–Vikasnagar NH-707A/NH-507 (107.07 km), Kempty–Chadogi–Yamuna Pul–Vikasnagar (136.50 km), Sahastradhara approach (42.46 km) |

---

## 2. Task 1: Historical Incidents Expansion & Verification

- **Baseline Preservation:** All 6 baseline `event_id` values (`DM-2024-0701-JPB`, `DM-2024-0726-GAL`, `DM-2024-0717-GAL`, `DM-2024-0717-SHM`, `DM-2025-0916-SH01-KM19`, `DM-2026-0711-HAN`) were preserved verbatim, verified against primary articles/broadcasts, and enriched with coordinates, road segments, secondary corroborating URLs, staged reopening details, and multi-source rainfall windows.
- **Additional Events Found (+28):**
  - **2023 Monsoon (+7):** `DM-2023-0701-JPB` (JP Bend debris/runoff), `DM-2023-0705-SH01` (multi-spot SH-01 debris), `DM-2023-0722-JPB` (JP Bend two trees + live HT wire), `DM-2023-0722-SH01` (multi-spot debris & Big Bend embankment), `DM-2023-0807-SH01` (SH-01 debris closure), `DM-2023-0810-GCK` (Gandhi Chowk–Kincraig embankment subsidence), `DM-2023-0922-MSL` (Masonic Lodge retaining wall collapse).
  - **2024 Monsoon (+4):** `DM-2024-0621-GAL` (Galogi Power House landslide), `DM-2024-0719-GAL` (Galogi Dhar retaining wall collapse & 6–7 day bus/heavy-vehicle ban), `DM-2024-0731-KOL` (~2 km below Kolukhet nighttime landslide), `DM-2024-0801-GAL` (Galogi gabion wall collapse & 5-day renewed bus ban; single-lane >40 days).
  - **2025 Monsoon (+5):** `DM-2025-0629-MAL` (Malsi Zoo culvert retaining wall collapse), `DM-2025-0629-GAL` (Galogi landslide), `DM-2025-0918-SHM` (technical safety halt on newly erected Shiv Mandir Bailey bridge), `DM-2025-0922-GAL` (Galogi massive landslide), `DM-2025-0923-JHP` (Jharipani toll/trek route land subsidence).
  - **2026 Monsoon (+12):** `DM-2026-0720-PWB` (Pani Wala Bend km 21 subsidence & ~24h full shutdown), `DM-2026-0722-PWB` (Pani Wala Bend tree fall 02:30–07:00), `DM-2026-0722-KOL` (~1 km ahead of Kolukhet landslide), `DM-2026-0728-HAN` (Hanuman Temple boulder fall), `DM-2026-0728-PWB` (Pani Wala Bend landslide burying restaurant 2nd time), `DM-2026-0812-PWB` (Pani Wala Bend mudslide & 2–10 km slush jam), `DM-2026-0822-PWB` (Pani Wala Bend repeat subsidence & 8–10 day heavy-vehicle ban), `DM-2026-0830-PWB` (Pani Wala Bend km 21 & Pahari Terrace slides), `DM-2026-0831-PWB` (Pani Wala Bend narrowed to 8-ft strip), `DM-2026-0831-GAL` (Galogi ~17:00 major landslide), `DM-2026-0901-PWB` (Pani Wala Bend partial carriageway washout), `DM-2026-1007-PWB` (Pani Wala Bend–Maggi Point hillside collapse).
- **Deduplication & Strict Exclusion of Misdated/Non-SH-01 Articles:**
  - Duplicate syndicated TOI URLs (e.g., `112204350.cms` and `112204363.cms`) were consolidated into single events.
  - Pre-monsoon events (e.g., Mar 31 & Apr 26, 2023 Library Chowk/Mall Road; May 28–29, 2026 storm), non-SH-01 town/feeder-road incidents (e.g., Almas/Lvakhal NH-707A on Jul 8, 2026; Tehri Road Woodstock School slides; Mall Road internal collapses), and older-year false positives frequently misattributed by search engines (Aug 2020, Aug 2021, Jul 2022) were explicitly audited by embedded article timestamps and excluded from SH-01 monsoon counts.

---

## 3. Task 2: Geospatial Coordinates & Road Verification

- **SH-01 Chainage Datum Validation:** Using OpenStreetMap/OSRM pure SH-01 road geometry from Dehradun Clock Tower (`30.324465, 78.041914`) to Mussoorie Library Chowk (`30.460006, 78.066517`, length `30.01 km`), the official **Uttarakhand Landslide Mitigation & Management Center (ULMMC)** coordinates for **Galogi km 25** (`30.422478, 78.072431`, `30°25'20.92"N, 78°04'20.75"E`) fall **33.3 m** from the OSM SH-01 centerline at `19.88 km` from Clock Tower, establishing a PWD datum offset of **`+5.12 km`** (placing Library Chowk at `est_PWD_km = 35.15 km`, matching the official 35 km highway length to within 150 m).
- **Verified Coordinates (20 / 21 features):**
  - **18 Direct Verified Points:** Verified directly via OpenStreetMap Overpass nodes (`Kuthal Gate` 0.0 m, `Kolukhet` 9.7 m, `Bhatta` 16.1 m, `Kincraig` 25.6 m, `Library Chowk` 0.0 m, `Barlowganj` 195.5 m / 6.2 m on diversion, `Jharipani Trek` 471.3 m, `Kimadi` 3.5 m on SH-79, `Sahastradhara` 14.6 m, `Kempty Fall` 5.8 m, `Chadogi` 45.0 m, `Yamuna Pul` 31.7 m, `Vikasnagar` 8.5 m), official ULMMC government coordinates (`Galogi km 25` 33.3 m), or credible gazetteers verified against OSM SH-01 (`Shiv Mandir / Prakasheshwar Mahadev` 18.0 m, `JP Bend` 20.6 m, `Malsi Deer Park` 52.4 m, `Masonic Lodge` 288.0 m near OSM `Picture Palace`).
  - **2 Chainage-Interpolated Points on OSM SH-01 (`±500 m` accuracy):** `LOC-004` (**SH-01 km 19**, `30.412419, 78.080491`, interpolated 6.0 km downhill of ULMMC km 25 -> 1.32 km uphill above Shiv Mandir, matching 2025 reports of the collapsed bridge above Shiv Mandir) and `LOC-010` (**Pani Wala Bend km 21**, `30.420110, 78.077851`, interpolated 4.0 km downhill of ULMMC km 25 -> 1.47 km downhill of Kolukhet).
  - **1 Intentionally Ungeocoded Pinpoint (`LOC-005` — near Hanuman Temple beyond Galogi):** No verified OSM POI or public GPS coordinate exists for this roadside shrine beyond Galogi Power House. Coordinates are kept `null` rather than invented; both events at this landmark (`DM-2026-0711-HAN`, `DM-2026-0728-HAN`) are linked to verified road segment `SEG-SH01-05` (`Galogi km 25 to Bhatta km 28.9`).

---

## 4. Task 3: Road Closure Improvements & Confirmed Durations

- **Standardized Closure Taxonomy:** Every roadway-impacting record in `historical_road_closures.csv` (33 records) is classified into one of four mutually exclusive categories:
  - `full_closure`: **23 records** (complete traffic halt on both sides).
  - `partial_closure`: **4 records** (e.g., heavy vehicles/buses banned or diverted while light vehicles pass).
  - `one_way_traffic`: **3 records** (single-lane alternating movement due to carriageway subsidence/narrowing without confirmed full halt).
  - `temporary_traffic_disruption`: **3 records** (intermittent debris cleared continuously without sustained full closure).
- **Separate Partial vs. Full Reopening:** `partial_reopening_time_local` and `full_reopening_time_local` are separated in both `historical_landslide_events.csv` and `historical_road_closures.csv`. Notably, multi-week single-lane bottlenecks (Galogi Jul–Aug 2024; Shiv Mandir Bailey bridge Sep 2025–Apr 2026; Pani Wala Bend Jul–Sep 2026) no longer conflate light-vehicle partial reopening with full two-way highway restoration.
- **Confirmed Durations vs. Nulls:** **16 of 33 closure records** have confirmed numeric durations in `confirmed_duration_hours` (ranging from `1.0` hr to `144.0` hrs for heavy-vehicle bans; `38.0` hrs for the Sep 16–17, 2025 full closure). The remaining **17 closure records** with unreported exact hours are preserved strictly as `null` (empty string) in both `closure_duration` and `confirmed_duration_hours` (removing baseline text placeholders such as `"exact duration unavailable"`).

---

## 5. Task 4: Downloaded Historical Rainfall Observations

- **Total Raw Observations Downloaded:** **79,028 observations** across four independent datasets covering all four monsoon seasons (2023–2026):
  1. **ECMWF IFS (~9 km / ~0.09°, Open-Meteo `models=ecmwf_ifs`):** **45,216 hourly observations** (3,768 hrs/season × 4 seasons × 3 distinct corridor grid cells: Lower `(30.4042, 78.0634)`, Mid `(30.4745, 78.0494)`, Upper `(30.4745, 78.1551)`). 100% complete (`0` nulls). Primary hourly source for event & non-event 1h/3h/6h/24h/72h windows.
  2. **ECMWF ERA5 Reanalysis (0.25° / ~25 km, Open-Meteo `models=era5`):** **15,072 unique hourly observations** (grid `(30.5000, 78.0000)` covering the corridor). 100% complete (`0` nulls).
  3. **NASA POWER MERRA-2 (`PRECTOTCORR`, v2.10.5, 0.5° × 0.625°):** **15,264 hourly observations** (3,816 hrs/season × 4 seasons at `(30.4225, 78.0724)`). 100% complete.
  4. **IMD Surface Synoptic Station Dehradun (WMO 42111, `30.3167°N, 78.0333°E`, 682 m):** **932 valid daily observations** from NOAA NCEI GSOD (2023–2025) + **2,544 raw 3-hourly SYNOP messages** from Ogimet (2023–2026), yielding **522 monsoon daily 24h station totals** exported in `historical_rainfall_hourly_corridor.csv` and covering **34/34 (100%)** historical events and **22/24** non-event controls. Cross-validation of Ogimet 03:00 UTC `6RRR/` totals against NOAA GSOD on 2023 peak days matched identically (`124.0`, `175.0`, `99.0/99.1`, `81.0` mm).
- **Hydrological Signal (ECMWF IFS 9 km, `historical_rainfall_event_windows.csv`):**
  - **34 Historical Events:** median 24h = `12.6 mm`, median 72h = `42.4 mm`, max 24h = `119.5 mm`, max 72h = `200.8 mm`.
  - **11 Baseline Monsoon Non-Events:** median 24h = `2.7 mm`, median 72h = `12.1 mm`, max 24h = `35.9 mm`, max 72h = `39.6 mm`.
  - **13 High-Rain Non-Events:** median 24h = `28.6 mm`, median 72h = `70.3 mm`, max 24h = `76.4 mm`, max 72h = `113.7 mm` (demonstrating that antecedent slope weakening, localized convective cloudbursts below 9 km resolution, and road-cut instability interact with rainfall totals).

---

## 6. Task 5: Alternative Routes Validation

No alternative route is labeled "safe" for monsoon conditions:
- **Kimadi–Lambhidhar–Cart Mackenzie Route (`SH-79` / `RT-ALT-KIMADI`):** OSM/OSRM connectivity verified (`40.69 km`, `3,411` vertices), **but rated `unsafe_unreliable_do_not_label_safe`**. Official PWD Master Plan Project 81 confirms **22 of 24 hill km are single-lane with "very poor" surface**; TOI (Aug 14 & Aug 31, 2026) confirms lack of crash barriers, heavy-vehicle unsuitability, and **documented monsoon closures across all four years (2023, 2024, 2025, 2026)**, including >24-hour closures simultaneous with SH-01 shutdowns on Jul 21–23, 2026 and Sep 16, 2025.
- **Kempty–Yamuna Pul–Vikasnagar Route (`NH-707A / NH-507 / NH-7`, `RT-ALT-KEMPTY-NH507` & `RT-ALT-KEMPTY-CHADOGI`):** OSM/OSRM connectivity verified (`107.07 km` direct via NH-707A/NH-507; `136.50 km` if detouring through local Chadogi hamlet in Tehri Garhwal). Structurally the only highway-class corridor rated for heavy vehicles in fair weather, **but rated `unverified_monsoon_safety_active_landslide_zones`** due to documented washouts/collapses at Kempty Falls (Sep 2025), Gandhi Chowk NH-707A (Feb 2026), Dimta Band NH-707A (Aug 20, 2026), Sarigad NH-507 (May 27, 2026), Lakhwar Dam (Jul 13–16, 2026), and Juddo NH-507 (Jul 28, 2026).
- **Sahastradhara Approach (`RT-CAND-SAHASTRADHARA`):** **Confirmed NOT a direct paved bypass to Mussoorie.** OSRM routes `42.46 km` via Nagal/Mussoorie Bypass, and official PWD Master Plan Project 17 confirms that **7.00 of 8.70 km on the eastern Maldevta–Suwakholi link is unmetalled (*kuchha*)**, with severe flash-flood/washout damage in Aug 2023, Sep 2025 (192 mm cloudburst), and Jul 2026.

---

## 7. Missing Information

1. **Pinpoint Coordinates for `LOC-005` (Hanuman Temple beyond Galogi):** No verified OSM or official GPS point exists; kept `null` and linked to `SEG-SH01-05`.
2. **Exact Clock Start/Reopening Times & Durations:** 17 of 33 road closures lack exact published start or reopening clock hours (kept `null` in `confirmed_duration_hours`). Where event clock hour was unreported (13 of 34 events), rainfall windows use calendar-day peak 1h/3h/6h and end-of-day 24h/72h (`window_anchor_type = event_day_peak_and_eod`).
3. **Hill-Slope Rain Gauge Observations (Mussoorie / Galogi):** No public IMD station data was accessible for Mussoorie (`WMO 42112` returned HTTP 404 in GSOD) or any mid-slope PWD/ARG gauge at Galogi/Kolukhet; Dehradun WMO 42111 sits on the valley floor (`682 m`), under-representing localized hill cloudbursts (e.g., Sep 16, 2025: 28 mm at Dehradun WMO 42111 vs. 192 mm reported at Sahastradhara).
4. **IMD Dehradun Station Data on 2 Non-Event Control Dates:** `NE-2025-1010` (2025-10-10) and `NE-2026-0620` (2026-06-20) fall outside GSOD 2025 coverage and the Ogimet SYNOP months downloaded (all 34 historical events have 100% IMD WMO 42111 coverage, and those 2 dates have 100% hourly ECMWF IFS, ERA5, and NASA POWER coverage).
5. **Exact Chadogi Local Road Restrictions:** While Chadogi (`LOC-019`) connectivity is verified on OSM, no official PWD load-limit or width bulletin specific to the local Tehri Kempty–Chadogi link was found.
6. **Sub-Hourly Peak Intensities:** Available downloaded model datasets are hourly (60-minute); 15-minute or 30-minute cloudburst intensities (such as IMERG V07 half-hourly) could not be downloaded without NASA Earthdata authentication.

---

## 8. Conflicting Reports & Resolutions

| Event / Record | Conflicting Claims Across Sources | Resolution / Dataset Treatment |
|---|---|---|
| **`DM-2025-0916-SH01-KM19` / `CL-2025-0916-SH01`** (Sep 16, 2025 Shiv Mandir bridge collapse & multi-point crisis) | (a) PWD Sep 16 bulletin projected reopening **Sep 21** (~5 days); (b) TOI Sep 17 22:45 said light-vehicle reopening was *planned* ~21:00; (c) ANI & ETV Bharat on **Sep 19** reported Bailey bridge constructed "on Friday". | **Resolved:** PWD's Sep 16 projection preceded emergency Rishikesh Bailey bridge assembly. On-site *Navbharat Times* (23:34 IST Sep 17), *Dainik Jagran* (Sep 18), and *Garhwal Post* (Sep 19) confirm **actual partial reopening for light vehicles occurred 2025-09-17 at 21:00 IST** (`38.0` hrs from PWD 06:58 log; brief safety halt morning of Sep 18 until >11:00). ANI/ETV Sep 19 items were delayed wire dispatches. Large passenger vehicles reopened conditionally (06:00–21:00) on **Oct 17, 2025**; two-way traffic at Shiv Mandir was not restored until a 2nd parallel Bailey bridge opened **Apr 24, 2026**. |
| **`DM-2024-0726-GAL` / `CL-2024-0726-GAL`** (Jul 26, 2024 Galogi slide) | *TOI* (Jul 28) reported road reopened **"almost an hour"** (~21:00 IST); same-night *ETV Bharat Hindi* (22:56 IST Jul 26) reported **~2 hours** (~22:00 IST) because the PWD JCB operator was absent and SDM Dr. Deepak Saini summoned a 2nd JCB. | **Documented & midpoint recorded (`1.5` hr):** Both sources cited; range `1–2 hours` and operational explanation preserved in `notes` and `reopening_conflict_status`. |
| **`DM-2026-0711-HAN` / `CL-2026-0711-HAN`** (Jul 11–12, 2026 Hanuman Temple boulder fall) | *DD News Uttarakhand* (uploaded Jul 12 13:21 IST) reported **2 hours** blockage; *Garhwal Post* (dateline Jul 12, pub Jul 15) reported **~1 hour** and used "late Sunday night" wording under a Jul 12 dateline. | **Documented & midpoint recorded (`1.5` hr):** Cross-verified as same Jul 11–12 overnight event; both durations and dateline discrepancy explicitly flagged. |
| **`DM-2024-0719-GAL`** (Jul 19, 2024 Galogi heavy-vehicle ban) | *Dainik Jagran* & *Live Hindustan* cited initial ban until **Jul 24**, whereas *ETV Bharat* cited **Jul 23**. | **Resolved:** Actual partial reopening (for vehicles ≤9 tonnes) was independently confirmed by *Dainik Jagran* on **Jul 26 morning** (`144.0` hrs from Jul 20 14:00 full bus enforcement). |
| **`DM-2023-0922-MSL`** (Sep 22, 2023 Masonic Lodge slide) | *TOI* opening sentence said "over an hour" vs. headline "for an hr" and PWD EE quote "within an hour"; *ETV Bharat* said "about 1 hour" and named adjacent Mussoorie Girls Inter College. | **Resolved (`1.0` hr):** Consistent across 3 independent outlets at ~1 hour (08:00–09:00 IST). |
| **`DM-2024-0731-KOL`** (Jul 31, 2024 Kolukhet slide) | *TOI* placed the slide **"about 2 km below Kolhukhet"** (~3h closure), while *ABP Live* (Aug 2) described a hillside collapse **"above Kolhukhet"**. | **Documented:** Primary TOI location retained; directional phrasing discrepancy noted. |
| **`DM-2026-0812-PWB`** (Aug 12, 2026 Pani Wala Bend mudslide) | *TOI* reported **2–3 km** queues on each side vs. *NDTV / Curly Tales* citing **up to 10 km** traffic jam. | **Documented:** Range `2–10 km` noted; actual two-way restoration confirmed on Aug 13 by PWD AAE in *TOI* Aug 14. |
| **Galogi 2023 Treatment Budget** (context) | *ETV Bharat* (Aug 11, 2023) cited **₹22.75 crore** vs. *TOI* (Jan 16, 2024) citing **₹21.75 crore** (and later ULMMC project portal listing **₹30.07 crore**). | Noted as administrative revision across project stages; does not affect event timing. |

---

## 9. Sources That Could Not Be Accessed

| Source | Endpoint / Access Attempted | Exact Error / Blocker | Phase-2 Mitigation |
|---|---|---|---|
| **NASA GPM IMERG V07B** (`GPM_3IMERGHH.07`) | `https://gpm1.gesdisc.eosdis.nasa.gov/opendap/GPM_L3/GPM_3IMERGHH.07/` & `https://jsimpsonhttps.pps.eosdis.nasa.gov/imerg/` | GES DISC directory returned `HTTP 200`, but data subset redirected `HTTP 302` to `urs.earthdata.nasa.gov` (NASA Earthdata Login required); NASA PPS returned `HTTP 401 Unauthorized`; ClimateSERV API returned `HTTP 404`; NOAA CoastWatch ERDDAP timed out. | Downloaded ECMWF IFS (~9 km hourly), ECMWF ERA5 (0.25° hourly), and NASA POWER MERRA-2 (hourly) instead. |
| **Copernicus CDS ERA5-Land Direct & Open-Meteo `era5_land`** | `https://cds.climate.copernicus.eu/` & `https://archive-api.open-meteo.com/v1/archive?models=era5_land` | Direct Copernicus CDS API requires personal API credentials; Open-Meteo `models=era5_land` returned `HTTP 200` with **`0/3768` non-null precipitation values** (Open-Meteo pairs ERA5 `0.25°` precipitation in `era5_seamless`). | Downloaded native **ECMWF ERA5 (`models=era5`)** AND **ECMWF IFS (`models=ecmwf_ifs`, ~9 km)** hourly precipitation with 100% completeness. |
| **IMD Pune 0.25° Gridded Rainfall (`RF25`)** | `POST https://www.imdpune.gov.in/cmpg/Griddata/RF25.php` & `HEAD .../RF25/indYYYY_rfp25.nc` | Server returned `HTTP 200` (`CDF\x01` NetCDF-3 header) but forcibly reset TCP connections mid-stream (`curl exit 56` / `IncompleteRead`) after `5.01 MB` (2023), `3.33 MB` (2024), and `0.46 MB` (2025) of ~25 MB files; direct static HEAD requests timed out. | Discarded truncated binary files; downloaded official **IMD Dehradun Station WMO 42111** ground observations (NOAA GSOD + Ogimet SYNOP) instead. |
| **NOAA GSOD Mussoorie (WMO 42112) & 2026 Dehradun** | `https://noaa-gsod-pds.s3.amazonaws.com/{2023..2026}/42112099999.csv` & `.../2026/42111099999.csv` | Returned `HTTP 404 Not Found` (Mussoorie WMO 42112 not archived in GSOD S3; 2026 Dehradun not yet published; NCEI primary server returned `HTTP 503`). | Used AWS S3 GSOD 2023–2025 for Dehradun WMO 42111 and **Ogimet WMO FM-12 SYNOP** for Sep 2025 and 2026 Dehradun WMO 42111. |
| **Ogimet SYNOP `2024_06_07a` block** | `https://www.ogimet.com/cgi-bin/getsynop?block=42111&begin=202406150000...` | Returned `HTTP 501` under rate throttling during retry. | Covered 100% by downloaded **NOAA GSOD 2024** for Dehradun WMO 42111. |

---

## 10. Deliverables Manifest (All Schemas Preserved)

1. `historical_landslide_events.csv` — 34 events (all 19 baseline columns retained + 13 Phase-2 columns).
2. `historical_road_closures.csv` — 33 closures (all 12 baseline columns retained + 7 Phase-2 columns).
3. `geographical_coordinates.csv` — 21 features (all 9 baseline columns retained + 6 Phase-2 columns).
4. `rainfall_data_source_inventory.csv` — 8 sources (all 8 baseline columns retained + 4 Phase-2 columns).
5. `alternative_route_source_inventory.csv` — 3 routes (all 7 baseline columns retained + 9 Phase-2 columns).
6. `historical_rainfall_event_windows.csv` — 232 multi-source 1h/3h/6h/24h/72h event & non-event rainfall rows.
7. `historical_rainfall_hourly_corridor.csv` — 10,948 actual downloaded hourly (event/control 72h windows) + monsoon daily IMD station observations.
8. `road_segments.csv` — 12 corridor & alternate-route segment definitions.
9. `alternative_routes_geometry.geojson` — Verified OpenStreetMap/OSRM LineString GeoJSON FeatureCollection (5 routes).
10. `data_quality_report.md` — This report.
