# cherry-blossom
Forecasts/projections for cherry blossom timing

## Methodology

Key paper: [Aono and Moriya (2003)](https://www.jstage.jst.go.jp/article/agrmet/59/2/59_2_165/_pdf/-char/ja)

- The basis for [Japan's forecast](https://sakura.weathermap.jp/en.php) is the "DTS" method
    - DTS = days at standard temperature
    - Buds grow at a certain rate per day when temperature is at the standard
    - Temperature-dependent growth rate follows an Arrhenius equation
    - Buds blossom when they hit a certain number of DTS
- [Another summary](https://blog.dataiku.com/predicting-the-bloom-of-sakura-with-dataiku-dss)
    - Compute a "start date" based on latitude, typical temperature, distance from ocean
        - "Endodormancy"
    - Start date is *later* if winter temperatures are higher (but *earlier* if spring temperatures are higher)
    - Use the Arrhenius equation
- [Simplified version](https://yuriko-schumacher.github.io/statistical-analysis-of-cherry-blossom-first-bloom-date/) is that blooms occurs after 400 or 600 cumulative daily degrees
    - This seems not-unreasonable, since the DTS approach looks pretty much like a linear interpolation
- Data sources are weather data and observation of sentinel trees ([link](https://www.scmp.com/lifestyle/travel-leisure/article/3215108/why-making-japans-cherry-blossom-forecasts-such-pressurised-job-trouble-those-get-it-wrong))
- ML people throw everything they can at the problem([link](https://rapidminer.com/blog/ksk-analytics-solution/))
    - Some evidence (see "dataiku" blog above) that temperature is the main driver (not precipitation or sunlight)
- Generally seems harder in Japan, where you're trying to predict peak bloom dates for many locations

## Data sources

- NOAA (really Aono et al.)
  - [https://www.ncei.noaa.gov/access/paleo-search/study/26430]
  - 1200 years of peak bloom dates and mean March temperatures
  - Kyoto
- NPS
  - [https://www.nps.gov/subjects/cherryblossom/bloom-watch.htm]
  - Stage dates since 2004 (and two earlier peak bloom dates)
  - Washington, DC
- Japan Meteorological Agency
  - [Kaggle scrape](https://www.kaggle.com/datasets/ryanglasnapp/japanese-cherry-blossom-data)
  - [Source data](https://www.data.jma.go.jp/sakura/data/index.html)

## Data files

- `scrape_nps.ipynb` produces:
  - `data/nps.csv`: stage dates
  - `data/nps_stages.csv`: order of the stages
- `scrape_noaa.ipynb` produces `data/noaa.csv`
