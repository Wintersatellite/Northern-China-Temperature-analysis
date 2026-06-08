# How Fast Are Northern China's Cities Warming? (1960–2023)

A portfolio data project for **AAE 718 (Summer 2026), Project 03**. It measures annual
mean-temperature trends in four northern Chinese cities using ~64 years of daily station data.

**Read the report:** [`report.md`](report.md) (a PDF version is submitted to Canvas).

## Question

Northern China — the Northeast and the Inner Mongolian plateau — is high-latitude, continental,
and rapidly urbanizing, exactly where warming should be strongest. This project asks how much
four of its cities have actually warmed since 1960, and whether they warm at the same pace:
**Hohhot, Harbin, Changchun, and Shenyang.**

## Findings (short version)

- All four cities warmed over 1960–2023, averaging **+0.33 °C per decade (~2.1 °C total)** —
  faster than the global mean.
- Hohhot (+0.39), Harbin (+0.38), and Changchun (+0.35 °C/decade) warmed nearly twice as fast
  as heavily industrial **Shenyang (+0.18)**, whose suppressed trend is consistent with aerosol
  dimming.
- Most of the warming arrived after the late 1980s; the 1960s–mid-1980s were nearly flat.

## Data

- Source: NOAA **GHCN-Daily** via the **NCEI Access Data Service** (no API key required):
  `https://www.ncei.noaa.gov/access/services/data/v1`
- Stations (GHCN IDs): Hohhot `CHM00053463`, Harbin `CHM00050953`, Shenyang `CHM00054342`,
  Changchun `CHM00054161`. Variables: `TMAX`, `TMIN`, `TAVG` (metric / °C).
- Running the script downloads the data and writes one CSV per city into `data/`.

## How to run

```bash
pip install -r requirements.txt
python north_china_temp_trends.py
```

This fetches each station from NCEI, saves `data/<city>.csv`, prints the trend numbers, and
writes the three figures into `images/`. To confirm the station IDs and data coverage first,
uncomment `verify_station_ids()` at the bottom of the script.

## Repository layout

```
.
├── north_china_temp_trends.py   # fetch + analysis + figures
├── report.md                    # written report (research-paper style)
├── README.md
├── requirements.txt
├── .gitignore
├── data/                        # per-city CSVs (created when you run the script)
└── images/                      # cn_fig1–cn_fig3
```

## Method notes

Annual mean = average of daily mean temperature (reported TAVG, else (TMAX+TMIN)/2), keeping
only years with ≥330 valid days. Trends are OLS fits in °C/decade. Caveat: these are
city/airport stations, so part of the trend reflects local urban heat-island growth, not only
regional climate change.
