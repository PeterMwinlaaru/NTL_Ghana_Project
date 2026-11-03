<p align="right"><a href="methodology.fr.md">Français</a></p>

# Methodology — Ghana (2014–2025)

## Data and cleaning

VIIRS DNB monthly (VCMSLCFG) and annual VNL V2, harmonised DMSP–VIIRS, daily Black Marble, GHSL/WorldPop, Sentinel-5P NO₂/SO₂, MODIS LST, World Bank. Cleaning: pixels valid if cf_cvg ≥ 2, unit-month kept if ≥ 80% of pixels observed, spikes replaced, background and gas flares masked.

## 📈 Use case 1 — Time dynamics

- **Question** — Is activity accelerating or slowing down, net of seasonality?
- **Data** — VIIRS VCMSLCFG (monthly), VIIRS VNL V2 (annual), Harmonised DMSP–VIIRS (Li et al., 2020)
- **Method** — Robust STL (period 12) on log(sum of lights); Theil–Sen slope and Mann–Kendall test on annual composites; anomaly and break detection.
- **Validation** — Trend significance (Mann–Kendall) and monthly/annual consistency (**p-value = < 0.0001**)
- **Uncertainty** — 95% CI of annual growth: +15.7% to +18.5%
- **Limits** — Cloud cover and short summer nights; light is not value added.
- **Status** — `experimental` · Confidence: high
- **References** — Cleveland et al. (1990) STL; Sen (1968); Elvidge et al. (2017).
- **Dashboard page** — [`#time`](https://PeterMwinlaaru.github.io/NTL_Ghana_Project/?country=GHA#time)

**Results of this run**

- `F02` Between 2014 and 2025, night-time light in Ghana changed by +17.1% per year (95% CI: +15.7% to +18.5%). Over the last 12 months, the seasonally adjusted level is +28.3% relative to the previous 12 months. (confidence high: significant trend (p < 0.01; n = 12))
- `F75` Validation: Trend significance (Mann–Kendall) and monthly/annual consistency (p-value = < 0.0001). Uncertainty: 95% CI of annual growth: +15.7% to +18.5% Limitations: Cloud cover and short summer nights; light is not value added. Status: experimental statistic; confidence high.

## 🗺️ Use case 2 — Regional growth and convergence

- **Question** — Which regions take off, which fall behind?
- **Data** — VIIRS VNL V2, GHSL / WorldPop, Sentinel-5P NO₂
- **Method** — Robust growth per unit (Theil–Sen, Mann–Kendall), growth/stagnation/decline classes, β- and σ-convergence, Herfindahl index.
- **Validation** — Rank correlation with tropospheric NO₂ (independent source) (**Spearman ρ = 0.25**)
- **Uncertainty** — Class assigned only if |slope| ≥ threshold and p < α; CI of β (robust errors).
- **Limits** — Small units: noise and light blooming between neighbours.
- **Status** — `experimental` · Confidence: medium
- **References** — Barro & Sala-i-Martin (1992) convergence; Henderson, Storeygard & Weil (2012).
- **Dashboard page** — [`#regions`](https://PeterMwinlaaru.github.io/NTL_Ghana_Project/?country=GHA#regions)

**Results of this run**

- `F03` Of 260 ADM2 units, 260 show significant growth, 0 are stagnating and 0 are declining. Light remains concentrated: Greater Accra Region accounts for 28% of national light. (confidence medium: classification of 260 units, threshold ±1%/yr and p < 0.10)
- `F04` Across ADM2 units, light per capita converges: the least-lit units are catching up. (confidence medium: β = −0.043 [−0.050; −0.035], n = 256)
- `F24` Greater Accra Region (ADM1, 2025): share of national light 27.5%, annual growth +14.3% (CI +13.3% to +15.7%, class Growth), light per capita 0.816, population 0.28 M, in the dark 3%, estimated GDP (experimental) 21.83 bn USD.
- `F25` Ashanti Region (ADM1, 2025): share of national light 18.7%, annual growth +16.9% (CI +16.0% to +18.3%, class Growth), light per capita 0.406, population 0.38 M, in the dark 1%, estimated GDP (experimental) 14.81 bn USD.

## 💹 Use case 3 — Light–GDP relationship

- **Question** — Can growth be estimated before its release, and regional GDP?
- **Data** — VIIRS, Real GDP (World Bank, WDI)
- **Method** — log(light) ~ log(GDP) in levels and growth, OLS with HAC errors; out-of-sample nowcast; regional GDP = national GDP allocated pro rata of light.
- **Validation** — Out-of-sample tracking of official growth (**correlation / MAE (pp) = -0.43 / 2.6**)
- **Uncertainty** — 95% CI of the elasticity: 3.34 to 3.67; 80% and 95% prediction intervals.
- **Limits** — Short annual sample; regional GDP is an experimental statistic to be checked against regional accounts.
- **Status** — `experimental` · Confidence: medium
- **References** — Henderson et al. (2012) AER; Chen & Nordhaus (2011) PNAS; Gibson et al. (2021) JDE.
- **Dashboard page** — [`#time`](https://PeterMwinlaaru.github.io/NTL_Ghana_Project/?country=GHA#time)

**Results of this run**

- `F05` The elasticity of light with respect to real GDP is 3.51 in levels (95% CI: 3.34 to 3.67, R² = 0.98, 12 years) and 0.25 in growth rates (CI: −2.07 to 2.56). Out of sample, light growth tracks GDP growth with a correlation of −0.43 (mean absolute error: 2.6 percentage points of growth). (confidence medium: clear relationship but only 12 years)
- `F43` Light–real GDP elasticity in levels: β = 3.51 (95% CI 3.34 to 3.67, R² = 0.98, n = 12, confidence medium: clear relationship but only 12 years). +1% GDP ↔ +β% light.
- `F44` Light–real GDP elasticity in growth rates: β = 0.25 (95% CI -2.07 to 2.56, R² = 0.00, n = 11, confidence low: n = 11, not significant (p = 0.83)). +1% GDP ↔ +β% light.
- `F45` Light–real GDP elasticity in long DMSP–VIIRS series: β = 0.93 (95% CI 0.71 to 1.16, R² = 0.92, n = 30, confidence high: n = 30, p < 0.01, narrow CI). +1% GDP ↔ +β% light.

## ⚡ Use case 4 — Shocks and resilience

- **Question** — How deep was a shock, and how fast the recovery?
- **Data** — VIIRS (monthly), Black Marble VNP46A2 (daily), event catalogue
- **Method** — Gap to the pre-shock level on the seasonally adjusted series; structural breaks; daily Black Marble index.
- **Validation** — Does the trough exceed ordinary variability? (**trough (main shock) = 3.2% — no**)
- **Uncertainty** — Pre-shock month-to-month variability (robust SD); unexplained breaks flagged.
- **Limits** — Shocks hitting poorly lit activities (agriculture, daytime services) are underestimated.
- **Status** — `experimental` · Confidence: low
- **References** — Román et al. (2018); Elvidge et al. (2020) COVID-19 lockdown lights.
- **Dashboard page** — [`#shocks`](https://PeterMwinlaaru.github.io/NTL_Ghana_Project/?country=GHA#shocks)

**Results of this run**

- `F06` The most pronounced shock in the seasonally adjusted series is “COVID-19”: trough of +3.2% (05/2020), return to the pre-shock level after 3 months. (confidence low: trough compared with pre-shock month-to-month variability)
- `F47` COVID-19 (2020-03-01 → 2021-06-30): trough of 3.2% on 2020-05-01, back to the pre-shock level after 3 months. Distinguishable from noise: no.
- `F48` Structural breaks: 2015-09-01 (42.2 %); 2020-11-01 (15.6 %); 2023-08-01 (-9.9 %); 2024-08-01 (27.8 %). Without a known event within ±6 months: 3.
- `F49` Hardest-hit regions (trough): Northern Region -33.3 % (covid19), Greater Accra Region -15.6 % (covid19), Volta Region -10.4 % (covid19), Oti Region -8.7 % (covid19), Savannah Region -8.1 % (covid19).

## ⚖️ Use case 5 — Inequality and electrification

- **Question** — Where do people without electricity live?
- **Data** — VIIRS VNL V2, GHSL / WorldPop, GHSL SMOD, electricity access (WDI)
- **Method** — Population-weighted Gini and Theil; population of inhabited pixels below the detection threshold; sensitivity to three thresholds; bootstrap CI of the Gini change.
- **Validation** — Gap with the World Bank electricity-access rate (**mean gap (pp) = 10.8**)
- **Uncertainty** — Range across radiance thresholds; bootstrap CI of the Gini.
- **Limits** — Proxy of outdoor lighting, not of connection: a connected but dimly lit household looks “in the dark”.
- **Status** — `experimental` · Confidence: medium
- **References** — Theil (1967); Falchetta et al. (2020) electricity access from lights.
- **Dashboard page** — [`#inequality`](https://PeterMwinlaaru.github.io/NTL_Ghana_Project/?country=GHA#inequality)

**Results of this run**

- `F07` The Gini coefficient of light per capita (ADM2) is 0.38 in 2025 (significant decrease since 2014). About 0.03 million people live in inhabited areas with no detectable light (2% of the inhabited population). (confidence medium: sensitive to the radiance threshold (from 0.03 to 0.06 M depending on the threshold); a proxy for outdoor lighting, not for grid connection)
- `F50` Gini of light per capita (ADM2): 0.470 in 2014 → 0.381 in 2025 (change -0.090, bootstrap CI -0.134 to -0.047). Theil T 0.258; between-region share 20%.
- `F51` People in inhabited areas without detectable light: 0.18 M (15%) in 2014 → 0.03 M (2%) in 2025. Urban/rural light-per-capita ratio 0.4. Proxy of electricity access, sensitive to the threshold.
- `F52` Average gap between the share of people in lit areas and the World Bank electricity-access rate: 10.8 points.

## 🏭 Use case 6 — Industrial zones

- **Question** — Where is industry, and is its activity growing?
- **Data** — VIIRS VNL V2, GHSL BUILT-S, Sentinel-5P NO₂/SO₂, MODIS MOD11A2, OpenStreetMap
- **Method** — Concordance of six signals per pixel (≥ 3 including light), 8-connected clusters, typology and confidence.
- **Validation** — Comparison with the reference list (OpenStreetMap) (**precision / recall / F1 = 17% / 31% / 0.22**)
- **Uncertainty** — Per-cluster confidence from the number of strong signals; isolated sites to verify.
- **Limits** — Sentinel-5P (≈ 5 km) and MODIS (1 km) resolution: signals describe a neighbourhood.
- **Status** — `experimental` · Confidence: low
- **References** — Elvidge et al. (2016) gas flares; Pesaresi et al. (2023) GHSL.
- **Dashboard page** — [`#industry`](https://PeterMwinlaaru.github.io/NTL_Ghana_Project/?country=GHA#industry)

**Results of this run**

- `F08` 210 industrial clusters detected from concordant satellite signals: 60 heavy industry, 13 business parks & logistics, 11 oil & gas sites and 126 isolated sites to verify. They emit 14.7% of national light (latest year); their light changes by +14.6% per year. Ashanti Region has the most industrial activity. (confidence low: precision 17% and recall 31% against the reference list)
- `F53` 210 industrial clusters (≥ 3 of 6 signals): Isolated site to verify 126, Heavy industry 60, Business park & logistics 13, Oil, gas & flares 11. Share of national light: 14.7%; annual growth +14.6%. Validation (OpenStreetMap): precision 17%, recall 31%.
- `F54` IND-001 — Isolated site to verify in Oforikrom Municipal (Ashanti Region) (599.205 km², 3 signals, confidence low); IND-002 — Heavy industry in Sagnerigu (Northern Region) (287.885 km², 4 signals, confidence medium); IND-004 — Isolated site to verify in Ho Municipal (Volta Region) (72.67 km², 3 signals, confidence low); IND-003 — Heavy industry in Bolgatanga Municipal (Upper East Region) (74.605 km², 4 signals, confidence medium); IND-012 — Business park & logistics in Kpone Katamanso (Greater Accra Region) (22.79 km², 3 signals, confidence low); IND-009 — Isolated site to verify in Yendi Municipal (Northern Region) (27.305 km², 3 signals, confidence low); IND-005 — Isolated site to verify in Asante Akim Central Municipal (Ashanti Region) (33.755 km², 3 signals, confidence low); IND-011 — Heavy industry in Wa Municipal (Upper West Region) (25.37 km², 3 signals, confidence low); IND-008 — Isolated site to verify in Sekyere East (Ashanti Region) (28.38 km², 3 signals, confidence low); IND-006 — Isolated site to verify in Hohoe Municipal (Volta Region) (30.96 km², 3 signals, confidence low)
- `F55` Ashanti Region: 37 industrial cluster(s), 780.7 km², 41.2% of the region's light.

## 🏖️ Use case 7 — Seasonal tourism

- **Question** — Which areas live from tourism, and how does the season evolve?
- **Data** — VIIRS (monthly), hotel nights or WDI arrivals
- **Method** — Summer excess net of comparable units at the same latitude; one-sided test; season index base 100; seasons overlapping Ramadan flagged.
- **Validation** — Correlation with hotel nights (**r = not available**)
- **Uncertainty** — p-value per unit; 2020–2021 excluded from the classification.
- **Limits** — Any summer activity (diaspora, second homes, festivals) is captured, not only tourism.
- **Status** — `experimental` · Confidence: low
- **References** — Seasonal light analyses of tourism, e.g. Hu et al. (2021).
- **Dashboard page** — [`#tourism`](https://PeterMwinlaaru.github.io/NTL_Ghana_Project/?country=GHA#tourism)

**Results of this run**

- `F09` 62 of 260 units show a net summer light excess of at least 10%: Sekyere Afram Plains North (Ashanti Region), Wa Municipal (Upper West Region), Ejura-sekyedumase (Ashanti Region), Ketu South (Volta Region). The median net excess reaches +26% in the most touristic zone. The season index (base 100 = 2019) falls to 44 in 2020 and stands at 286 in 2025. (confidence low: no hotel-night statistics to validate the indicator)
- `F68` 62 tourist zone(s) out of 260 ADM2 units (net summer excess ≥ 10%, peak months [7, 8]): Sekyere Afram Plains North (Ashanti Region) (+26%, confidence high), Wa Municipal (Upper West Region) (+26%, confidence high), Ejura-sekyedumase (Ashanti Region) (+25%, confidence high), Ketu South (Volta Region) (+22%, confidence high), Sagnerigu (Northern Region) (+22%, confidence high), Tema West Municipal (Greater Accra Region) (+22%, confidence high), Kpone Katamanso (Greater Accra Region) (+20%, confidence high), Atebubu Amantin (Bono East Region) (+20%, confidence high), Tamale Metropolitan (Northern Region) (+19%, confidence high), Weija Gbawe Municipal (Greater Accra Region) (+19%, confidence high).
- `F69` Season index (base 100 = 2019): 2014: 45, 2015: 44, 2016: 54, 2017: 79, 2018: 14, 2019: 100, 2020: 44, 2021: 33, 2022: 81, 2023: 307, 2024: 111, 2025: 286. Years when Ramadan overlaps the season: 2014, 2015, 2018, 2019, 2020, 2021, 2022, 2023.
- `F81` Validation: Correlation with hotel nights (r = not available). Uncertainty: p-value per unit; 2020–2021 excluded from the classification. Limitations: Any summer activity (diaspora, second homes, festivals) is captured, not only tourism. Status: experimental statistic; confidence low.

## 🏙️ Use case 8 — Urbanisation signals

- **Question** — Where do cities spread, where do villages get electrified, and where does population grow without light?
- **Data** — VIIRS VNL V2, GHSL GHS-POP / WorldPop, GHSL GHS-BUILT-S R2023A, urban population (WDI)
- **Method** — Lit area (pixels above the threshold) and population per unit; Theil–Sen growth rates; newly lit pixels (dark two years in a row at the start, lit two years in a row at the end), split between electrification of inhabited areas and new settlements; light/population typology.
- **Validation** — Rank correlation with GHSL built-up area growth (independent source) (**Spearman ρ = 0.55**)
- **Uncertainty** — Persistence required over two years to limit noise; ± 1 pp margin between growth rates before classifying.
- **Limits** — Light measures outdoor lighting, not urbanisation in the administrative sense; blooming widens cities; GHSL population is interpolated between epochs.
- **Status** — `experimental` · Confidence: medium
- **References** — Zhou et al. (2015) urban extent from lights; Pesaresi et al. (2023) GHSL; Min et al. (2013) village electrification.
- **Dashboard page** — [`#urban`](https://PeterMwinlaaru.github.io/NTL_Ghana_Project/?country=GHA#urban)

**Results of this run**

- `F70` National lit area: +17.1% per year; population: +2.1% per year. Classes (ADM2): Electrified urbanisation 223, Unlit growth 33, Balanced growth 2, Undetermined 1, Stable or declining 1.
- `F71` Between 2014 and 2025: 32,028 km² newly lit, of which 1,685 km² already inhabited (electrification, ≈ 131k people) and 30,343 km² of new settlements; 2 km² lost their light.
- `F72` Fastest lit-area expansion: East Gonja Municipal (Savannah Region) (+84.6%/yr), Yunyoo-nasuan (North East Region) (+47.0%/yr), Bongo (Upper East Region) (+44.2%/yr), Tempane (Upper East Region) (+44.0%/yr), Nanton (Northern Region) (+39.8%/yr), Krachi Nchumuru (Oti Region) (+38.3%/yr). Unlit growth (population faster than light): Adenta Municipal (Greater Accra Region), Ledzokuku Municipal (Greater Accra Region), La Dade-kotopon (Greater Accra Region), La-nkwantanang-madina (Greater Accra Region), Ga East (Greater Accra Region), Ayawaso West (Greater Accra Region), Ga Central Municipal (Greater Accra Region), Kwabre East (Ashanti Region).
- `F73` Spearman rank correlation between lit-area growth and GHSL built-up growth: 0.55 (p = 0.000, 260 units).

## General limits of night-time lights

- **What lights measure** — Upward radiance emitted around 01:30: agriculture, daytime trade, poorly lit services and the rural informal economy are poorly captured.
- **Saturation and blooming** — DMSP saturates in city centres (DN 63) and “blooms” beyond lit areas; VIIRS is much better, but blooming still inflates the lit area of cities.
- **Gas flares and isolated sites** — The automatic mask may remove isolated mines, ports or power plants, and miss small flares; candidates are exported for verification.
- **Clouds, seasons, moon** — Cloudy months are only partially observed; STL removes average seasonality but not an abnormal season (snow, late monsoon).
- **Product breaks** — DMSP and VIIRS are not directly comparable: the harmonised long series (Li et al., 2020) is a modelled product, to be read for trends only.
- **NTL–GDP elasticity** — Estimated on 10 to 30 annual observations: wide intervals, possible instability, a non-causal relationship that varies with the level of development.
- **Access to electricity** — “Inhabited without light” ≠ “not connected”: a connected household with low consumption is invisible; the indicator depends strongly on the radiance threshold and the population data.
- **Administrative boundaries** — geoBoundaries/GAUL may differ from official boundaries; small ADM2 units are sensitive to light spilling over from neighbouring units.
- **Industrial zones** — Detection relies on thresholds: a power plant, a port or a large shopping centre can meet the signals; a dimly lit factory without visible emissions is missed. Sentinel-5P (≈ 5 km) and MODIS (1 km) are coarser than VIIRS: NO₂/SO₂/heat signals describe a neighbourhood, not a building.
- **Summer tourism** — The summer excess captures any rise in summer light (second homes, diaspora visits, festivals, construction), not only tourism; at high latitudes, very short summer nights reduce VIIRS observations. Ramadan changes night-time activity: the summers concerned are flagged.
- **Urbanisation** — The lit area depends on the detection threshold and on light blooming around cities; a connected but dimly lit neighbourhood stays invisible. Population (GHSL/WorldPop) is modelled from censuses: its growth is not an independent observation, and years between two epochs are interpolated.


---
<sub>Generated by the notebook on 2026-11-03 · version 2.1.0</sub>
