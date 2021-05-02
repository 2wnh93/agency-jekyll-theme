---
caption: #what displays in the portfolio grid:
  title: Solar Energy Potential (Part 2)
  subtitle: Predicting solar energy potential of Spain using various forecasting models
  thumbnail: assets/img/portfolio/solar/solar.png

#what displays when the item is clicked:
title: Solar Energy Potential (Part 2)
subtitle: Apply tree regressors, fbprophet and neural networks to predict solar energy potential of Spain
image: assets/img/portfolio/solar/solar.png #main image, can be a link or a file in assets/img/portfolio

---

### Modelling with linear regression, tree algorithms and fbprophet
---

#### Preprocessing

I split the data such that the last month in the dataset (ie. December 2015) will be the test set, and all 9 years 11 months earlier will be what the model will train on. December 2015 data is the holdout set, from which I will determine how well the model generalises.

#### Baseline Model

Before running the data on any algorithms, I first set out the **baseline model** from which we will benchmark against how other model performs.

I determine the baseline model to be the **mean** of past solar energy potential, since this is most basic estimate.

Plotting the true values against baseline predictions (Figure 12), we see that the model does recognise seasonality but did not really identify more complex patterns.

![](assets/img/portfolio/solar/baseline-predictions.JPG)

*Figure 12: Baseline predictions against true values of test set*

Results of model based no RMSE and MAE as evaluation metrics, below :

| Model | RMSE | MAE |
| :-----: | :--: | :---: |
| Baseline | 0.0524 | 0.0258 |


#### Models Considered : Linear Regression, Random Forest Regressor, K Neighbours Regressor and XG Boost Regressor.

I ran the train set on these models considered, and results of training set are tabled below :

| Model | RMSE | MAE |
| :-----: | :--: | :---: |
| Baseline | 0.0524 | 0.0258 |
| Linear Regression | 0.0532 | 0.0283 |
| Random Forest | 0.0542 | 0.0268 |
| K Neighbors | 0.0622 | 0.0313 |
| XG Boost | 0.0554 | 0.0346 |


From here, sadly, none of the models did better than baseline. The closest is linear regression. It could be that other models are too complex for forecasting with just a few features, such that linear regression did the best. It is also likely that tree regressors may not be suitable for forecasting, especially to recognise seasonality.

In view of the above results, I explored other models to try and achieve something better than baseline.

#### Modelling with fbprophet

FB prophet is a powerful library and has hyperparameters that can tune seasonality, so I figured this model could probably perform much better than those considered earlier.

After tuning its hyperparameters, indeed, it did perform slightly better than earlier models.

![](assets/img/portfolio/solar/fbprophet-predictions.JPG)

*Figure 13: FB Prophet predictions against true values of test set*

From Figure 13 above, we see that the predictions are closer to the true values compared to baseline model. Looking at the evaluation metrics :

| Model | RMSE | MAE |
| :-----: | :--: | :---: |
| Baseline | 0.0524 | 0.0258 |
| Linear Regression | 0.0532 | 0.0283 |
| Random Forest | 0.0542 | 0.0268 |
| K Neighbors | 0.0622 | 0.0313 |
| XG Boost | 0.0554 | 0.0346 |
| FB Prophet | 0.0491 | 0.0293 |


FB Prophet had the best score amongst other models! I then try to beat that score using neural networks.

#### Modelling with neural networks

First, I used a simple recurrent neural network (RNN) to predict. RNN is a class of neural networks powerful for modeling *sequence* data like time series or natural language. RNNs have a sense memory which helps in keeping track of what happened earlier in the sequential data, that helps them *gain context and identifying correlations and patterns* [3].

Running the simple RNN, it performed slightly better than fbprophet.

![](assets/img/portfolio/solar/rnn-predictions.JPG)
*Figure 14: RNN predictions against true values of test set*

While fbprophet was able to capture seasonality, it is likely that taking into consideration the solar energy potential in the previous hour is equally or more important for the model to predict.

I also attempted to predict with Long Short-Term Memory (LSTM). LSTMs includes a "memory cell" that can maintain information in memory for long periods of time. A set of gates is used to control when information enters the memory, when it's output and when it's forgotten [4].

From Figure 15, it did just slightly better than RNN, which makes sense since the model would be also be able to account for seasonality.

![](assets/img/portfolio/solar/lstm-predictions.JPG)
*Figure 15: LSTM predictions against true values of test set*

### Conclusion and Recommendation

Here's a summary of results of predictions :

| Model | RMSE | MAE |
| :-----: | :--: | :---: |
| Baseline | 0.0524 | 0.0258 |
| Linear Regression | 0.0532 | 0.0283 |
| Random Forest | 0.0542 | 0.0268 |
| K Neighbors | 0.0622 | 0.0313 |
| XG Boost | 0.0554 | 0.0346 |
| FB Prophet | 0.0491 | 0.0293 |
| RNN | 0.0381 | 0.0197 |
| LSTM | 0.0353 | 0.0173 |


LSTM is most accurate in predicting solar energy potential and this model appear to be stable to help with more effective grid management.

Apart from effective grid management, we would also be able to predict which hours of the day where more energy is generated or where energy is least generated, and subsequently advice consumers times of the day where it's best to reduce energy consumption.

### Further Development

While data is based on regions in Spain, it is possible to scale this upwards to states or continents.

In the local context, it is possible to measure solar irradiance in various parts of Singapore. From here, areas with most sunlight could be identified, and solar panel placement could be made more efficient.

### Challenges and Limitations

The project has attempted to predict solar energy potential based on historical data assuming ideal conditions.

There are other uncontrollable factors that may affect solar efficiency. Factors that affect efficiency of cells include higher temperatures, cloud cover or storms, and high humidity. These present some external limitations to Singapore's ability to generate significant quantities of electricity from renewable energy sources.

## References

[1] Energy Market Authority (EMA) "Intermittency Pricing Mechanism for Intermittent Generation Sources in the National Electricity Market of Singapore" [Online Document], 2018. https://www.ema.gov.sg/cmsmedia/Final%20Determination%20Paper%20-%20Intermittency%20Pricing%20Mechanism%20vf.pdf [Accessed: 22 April 2021]

[2] N. Sharma, P. Sharma, D. Irwin and P. Shenoy "Predicting Solar Generation from Weather Forecasts Using Machine Learning" [Online Document], 2011. http://www.ecs.umass.edu/~irwin/smartgridcomm.pdf [Accessed: 22 April 2021]

[3] K.Kohli "Recurrent Neural Networks (RNN's) and Time Series Forecasting" [Online Article], 2020. https://medium.com/analytics-vidhya/recurrent-neural-networks-rnns-and-time-series-forecasting-d9ea933426b3 [Accessed: 26 April 2021]

[4] J. Chung, C. Gulcehre, K. Cho, Y. Bengio "Empirical Evaluation of Gated Recurrent Neural Networks on Sequence Modeling" [Online Paper], 2014.

{:.list-inline}
- Date: 26 Apr 2021
- Category: neural networks, rnn, lstm, fbprophet
