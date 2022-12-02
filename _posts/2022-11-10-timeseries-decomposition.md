---
layout: post
title: "Demistifying Timeseries Decomposition"
excerpt: "This post will simplify how time series decomposition work. This is not the exact breakdown of the package but it is a simplified version."
tags: [timeseries]
categories: [Timeseries Analysis]
share: true
comments: true
mathjax: true
---

<hr>

- [Background](#background)
- [Steps](#steps)
  - [Step 1 :: Detrending Time series](#step-1--detrending-time-series)
    - [Step 1.1 :: Find Approximate Trend](#step-11--find-approximate-trend)
    - [Step 1.2 :: Remove the approx. trend from the data](#step-12--remove-the-approx-trend-from-the-data)
  - [Step 2 :: Find Seasonality](#step-2--find-seasonality)
    - [Step 2.1 :: Group data](#step-21--group-data)
    - [Step 2.2 :: Fill the monthly values](#step-22--fill-the-monthly-values)
  - [Step 3 :: Find Trend](#step-3--find-trend)
    - [Step 3.1 :: De-seasonalise data](#step-31--de-seasonalise-data)
    - [Step 3.2 :: Calculate Trend](#step-32--calculate-trend)
  - [Step 4 :: Calculate Residual](#step-4--calculate-residual)
- [Conclusion](#conclusion)

<hr>

In this post we will see how time series decomposition work. This is not the original breakdown of the `statsmodels` seasonal decomposition instead this post will help to understand each and every component of the decomposition process.

Code Link :: [GitHub Repository](https://github.com/rehanguha/timeseries-decomposition)


## <a name='Background'></a>Background

Here we will use the below simple equation to break down the time series.

$$ TS = trend + seasonality + residual $$

We are assuming that the time sereis is built using only 3 components and i.e. `trend`, `seasonality`, `residual`.

In the following steps we will try to find each of the component of the time series. 

## <a name='Steps'></a>Steps

Below is the plot for the original time series data.

![](TSD_ts.png)
<center>Original Time Series data</center>

### <a name='Step1::DetrendingTimeseries'></a>Step 1 :: Detrending Time series

#### <a name='Step1.1::FindApproximateTrend'></a>Step 1.1 :: Find Approximate Trend 

In the time series data fit a $$n$$ degree polynomial. I went with $$n=2$$ as most of the trend lines are less degree polynomial. 

This will give us a trend line which is not the final one.

![](TSD_atrend.png)
<center>ApproximateTrend</center>

#### <a name='Step1.2::Removetheapprox.trendfromthedata'></a>Step 1.2 :: Remove the approx. trend from the data

Here we will simple substact the data with the approx trend.

$$detrended = TS - approxTrend$$

Now we are left with a detrended data.

![](TSD_detrend.png)
<center>Approximate De-Trended Time Series</center>


### <a name='Step2::FindSeasonality'></a>Step 2 :: Find Seasonality

#### <a name='Step2.1::Groupdata'></a>Step 2.1 :: Group data

Here we need to group the data as per required periods. I am going with 12 months seasonal period with this data. We will find average for all the months over all the years.

#### <a name='Step2.2::Fillthemonthlyvalues'></a>Step 2.2 :: Fill the monthly values

As we selected monthly periods we will have 12 records and 1 for each month. Now from the above step we fill the same monthly average value for all the years.

![](TSD_seasonality.png)
<center>Seasonality</center>

### <a name='Step3::FindTrend'></a>Step 3 :: Find Trend

#### <a name='Step3.1::De-seasonalisedata'></a>Step 3.1 :: De-seasonalise data

Now to find deseasonal data we can simply subtract the seasonality from the original data

$$deseasoned = TS - seasonality$$

![](TSD_deseasoned.png)
<center>De-Seasoned Time Series</center>

#### <a name='Step3.2::CalculateTrend'></a>Step 3.2 :: Calculate Trend

In the ablove deseasoned data fit a $$n$$ degree polynomial. I went with $$n=2$$ as most of the trend lines are less degree polynomial. 

This will give us the final trend line.

![](TSD_trend.png)
<center>Trend</center>

### <a name='Step4::CalculateResidual'></a>Step 4 :: Calculate Residual

We have all the components to calculate the residual now.

$$ residual = TS - seasonality - trend $$

![](TSD_residual.png)
<center>Residual</center>

## <a name='Conclusion'></a>Conclusion

We have successfully broken down a time series into three components namely `trend`, `seasonality` and `residual`.


![](TSD_trend.png)
<center>Trend</center>

![](TSD_seasonality.png)
<center>Seasonality</center>

![](TSD_residual.png)
<center>Residual</center>

The results may not exactly match with the current way of decomposing a time series using `statsmodels`.