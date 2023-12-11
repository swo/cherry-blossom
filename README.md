# cherry-blossom
Forecasts/projections for cherry blossom timing

## Methodology

### Basic approach

After blossoming in the spring, cherry trees enter dormancy in autumn. The dormant period ends when a certain number of cold days have passed. The tree, sensing that winter is ending, begins growing buds, which grow faster when temperatures are warmer. Thus, higher winter temperatures and cooler spring temperatures both contribute to later blossom dates.

The Japanese cherry blossom [forecasts](https://sakura.weathermap.jp/en.php) are based on the "DTS" method of [Aono and Moriya (2003)](https://www.jstage.jst.go.jp/article/agrmet/59/2/59_2_165/_pdf/-char/ja).

In this model, endodormancy ends on a certain date $D_\mathrm{me}$:

$$
D_\mathrm{me} = 136.765 - 7.689 \phi + 0.133 \phi^2 - 1.307 \ln L + 0.144 T_F + 0.285 T_F^2
$$,

where $\phi$ is the latitude ($\degree$ N), $L$ is the distance from the nearest coast (km), and $T_F$ is the average temperature during January, February, and March. Aono & Moriya Table 2 shows these values as between day of year 30 and 50, which is somewhere in February.

After dormancy is over, the buds grow at a standard rate per day, when the air temperature is at a standard value. A day at a higher temperature constitutes more than one day transformed to standard temperature (DTS), and a colder day constitues less than one DTS, according to the Arrhenius equation:

$$
t_i = \exp \left\{ \frac{E_a(T_i - T_s)}{R T_i T_s} \right\},
$$

where $t_i$ is the DTS for day $i$, $T_i$ is the air temperature, $T_s$ is the standard temperature, and $E_a$ and $R$ are constants.

Buds blossom after a certain number of DTS.

### Model adapation

I only consider a single location, so $D_\mathrm{me}$ will depend only on winter temperatures. Biological data suggests that cherry trees require temperatures of between 32 and 50 $\degree$ F to exit endodormancy.

I also linearize the DTS computation. If $T_i - T_s$ is small compared to a certain combination of $E_a$, $R$, and $T_i T_s$, then:

$$
t_i = A + B T_i + \mathcal{O}(T_i^2),
$$

where $A$ and $B$ are constants to be fit. E.g., [another modeler](https://yuriko-schumacher.github.io/statistical-analysis-of-cherry-blossom-first-bloom-date/) used an empirical approach, concluding that blooms occurs after 400 or 600 cumulative daily degrees during spring.

### Model statement



### Alternative approaches

More [sophisticated forecasts](https://www.scmp.com/lifestyle/travel-leisure/article/3215108/why-making-japans-cherry-blossom-forecasts-such-pressurised-job-trouble-those-get-it-wrong) in Japan account for weather data as well as observational data from sentinel trees.

There are [some](https://rapidminer.com/blog/ksk-analytics-solution/) accounts from machine learning approach concluding that temperature is the main driver of blossom date, not precipitation or sunlight.

## Data sources

### Washington, DC

- NPS
  - [https://www.nps.gov/subjects/cherryblossom/bloom-watch.htm]
  - Stage dates since 2004 (and two earlier peak bloom dates)

### Japan

- Japan Meteorological Agency
  - [Kaggle scrape](https://www.kaggle.com/datasets/ryanglasnapp/japanese-cherry-blossom-data)
  - [Source data](https://www.data.jma.go.jp/sakura/data/index.html)
- Aono et al.
  - [https://www.ncei.noaa.gov/access/paleo-search/study/26430]
  - 1200 years of peak bloom dates and mean March temperatures
  - Kyoto

## Data files

- `scrape_nps.ipynb` produces:
  - `data/nps.csv`: stage dates
  - `data/nps_stages.csv`: order of the stages
- `scrape_aono.ipynb` produces `data/aono.csv`
