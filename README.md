# Clothing Sales Time Series

## Introduction
Consumer companies that miss financial expectations will often times blame bad weather for decreasing consumer spend. I set out to use time series in order to assess if there is modeling evidence to back up these claims of weather dependence in retail spend. I used monthly clothing spend from 1992–present, as clothing is especially susceptible to fluctuations in temperature due to the seasonal nature of how consumers purchase it as well as how retailers stock clothing. I used monthly US retail clothing spend data from FRED Economic Data for my time series and contiguous United States percentage area experiencing anomalously cold or warm weatherfrom the National Oceanic and Atmospheric Administration website for use as an exogenous variable.  I compared SARIMA model performance to SARIMAX model performance with exogenous weather data in order to determine the impact of weather on retail clothing sales.  While both SARIMA (RMSE: 395) and SARIMAX (RMSE: 394) outperformed the baseline Persistence model (RMSE: 3,689), SARIMAX did not outperform SARIMA by enough to rule out test set sampling error as the cause of the slight difference in performance.

## Obtain Data

I obtained monthly US retail clothing spend data in csv form from FRED Economic Data, which in turn had sourced the data from the US Census Monthly Retail Trade report. I also obtained contiguous United States percentage area experiencing anomalously cold or warm weather through a scrape of the National Oceanic and Atmospheric Administration website for use as an exogenous variable in the time series modeling.  I merged the two sources together on the month to create my unscrubbed data source.

## Scrub Data

<a href="url"><img src="https://github.com/blantj/clothing_sales_time_series/blob/main/Images/df_info.png" align="middle" height="250" width="300" ></a>

The first thing that I did to scrub the retail clothing sales time series dataset was remove all 2020 data to eliminate anomalous datapoints resulting from covid. A df.info() overview of the data demonstrated that there were no missing datapoints or data types in need of updating. The final post-scrubbing dataset included 336 monthly datapoints from 1/1992–12/2019 across the Sales time series data and Proportion of Days With Unfavorable Weather exogenous variable. The df also included Month and Year variables that would only be used for EDA.

## Explore Data

<a href="url"><img src="https://github.com/blantj/clothing_sales_time_series/blob/main/Images/time_series_chart.png" align="middle" height="250" width="300" ></a>

From 1992 to 2019, mean monthly clothing sales was 11,838 with a standard deviation of 3,889. Retail clothing sales showed consistent trends across the 28 years with the mean growing by approximately 4% each year. There was also consistent 12 month seasonality with sales peaking at an average of 18 billion dollars during the December holiday season, followed by a dip in January to a low of an 8 billion dollar average.

<a href="url"><img src="https://github.com/blantj/clothing_sales_time_series/blob/main/Images/acf.png" align="middle" height="250" width="300" ></a>

The monthly retail clothing spend autocorrelation function based on 12 month differencing revealed 9 possible statistically significant auto-correlated lags for possible use in MA modeling.

<a href="url"><img src="https://github.com/blantj/clothing_sales_time_series/blob/main/Images/pacf.png" align="middle" height="250" width="300" ></a>

The partial autocorrelation function for monthly retail clothing spend based on 12 month differencing revealed 3 statistically significant partially auto-correlated lags for possible use in AR modeling.

## Model Data

<a href="url"><img src="https://github.com/blantj/clothing_sales_time_series/blob/main/Images/model_performance.png" align="middle" height="150" width="450" ></a>

Both SARIMA (RMSE: 395) and SARIMAX (RMSE: 394) significantly outperformed the baseline model (RMSE: 3,689). They both also performed favorably relative to the dataset standard deviation of 3,889. While SARIMAX slightly outperformed SARIMA in trms of RMSE (394 vs. 395) and MAE (294 vs. 304), the difference was not large enough to say that anomolous weather is a meaningful contributor to modeling retail clothing sales.

## Analyze Results

As was the case with evaluation metric performance, the charts of predicted vs. actual monthly retail sales for the test set were very similar for the SARIMA and SARIMAX models. This reinforces the idea that while SARIMAX slightly outperformed SARIMA, it is impossible to say whether this is due to random error or SARIMAX being a better model. Based on the results of my time series modeling, I am unable to confirm whether public company management is correct to blame poor consumer consumer facing performance on anomalous weather.


# Github Files
[Scrape.ipynb](https://github.com/blantj/clothing_sales_time_series/blob/main/Scrape.ipynb) :  Scrape weather data from NOAA

[modeling.ipynb](https://github.com/blantj/clothing_sales_time_series/blob/main/modeling.ipynb) :  Monthly retail clothing sales time series modeling

# Sources
NOAA: https://www.ncdc.noaa.gov/temp-and-precip/uspa/warm-cold/1

FRED: https://fred.stlouisfed.org/series/MRTSSM4481USN

