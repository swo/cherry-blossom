# cherry-blossom
Forecasts/projections for cherry blossom timing

## Data sources

- NOAA
  - [https://www.ncei.noaa.gov/access/paleo-search/study/26430]
  - 1200 years of peak bloom dates and mean March temperatures
  - Kyoto
- NPS
  - [https://www.nps.gov/subjects/cherryblossom/bloom-watch.htm]
  - Stage dates since 2004 (and two earlier peak bloom dates)
  - Washington, DC

## Data files

- `scrape_nps.ipynb` produces:
  - `data/nps.csv`: stage dates
  - `data/nps_stages.csv`: order of the stages
- `scrape_noaa.ipynb` produces `data/noaa.csv`
