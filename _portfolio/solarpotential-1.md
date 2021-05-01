---
caption: #what displays in the portfolio grid:
  title: Solar Energy Potential (Part 1)
  subtitle: Clustering of European Countries for streamlined analysis of solar energy potential
  thumbnail: assets/img/portfolio/solar/solar.png

#what displays when the item is clicked:
title: Solar Energy Potential (Part 1)
subtitle: Apply clustering algorithms on 29 European countries and perform data exploration
image: assets/img/portfolio/solar/solar.png #main image, can be a link or a file in assets/img/portfolio

---

## Preamble

Demand for energy is increasing, and is one of the main reasons for integration of **solar energy** into the electric grids or networks. Based on existing technologies, solar energy (compared to other renewable energy options) provides the greatest potential for deployment in Singapore [1].

One of the challenges with integrating solar energy, into the grid network is that its power generation is intermittent and uncontrollable. Therefore, predicting future solar power generation is important, since the grid must dispatch generators to satisfy demand as generation varies [2].

## Objective

The project objective is to predict potential solar power generation most accurately, based on historical data. In evaluating the accuracy of models, I refer to the root mean squared error (RMSE) and the mean absolute error (MAE).

The RMSE is the root average of the total squared forecast error values. The mean squared error penalizes larger errors so when root is applied, it transforms the value back into the original units of the predictions. We want to achieve as small an RMSE value as possible as it shows that the model's predictions are closer to the true values.

The MAE is the average magnitude of errors in a set of predictions, without considering direction (ie. negative or positive). Similarly, a better model would have lower MAE.

## Analysis and Findings
---

### Data Cleaning
---

Both datasets comprise 50 years' worth of solar generation data of European countries by country and by NUTS 2 system. The values in both datasets reflect the hourly estimates of the area's solar energy potential from 1986 to 2015. The same kind of data is collected, just that the one for NUTS 2 system collect solar energy potential of different regions of a country so this dataset has more data to work with for a particular country.

A `time` column was added to both datasets to track which hours of the day would the area's energy potential be higher than others. We would expect there to be a spike in the afternoon hours. There may also be seasonality across the years, so the `month` and `week` will also be tracked.

The pandas profiling report generated for the datasets, showed the following:
- there are no missing values
- data for each country is heavily right-skewed (ie. there a lot more instances where no solar energy is generated)
- there is high correlation between the countries, which is expected since they are pretty close together, and so will have similar exposure to the sun. Based on this, I could simplify the analysis by clustering the countries, and perform analysis on just one country in each cluster.
- there are no negative values, so there is a remote likelihood of erroneous data collected

Further data exploration will be done after clustering the countries.

### Clustering
---

First I want to visualize the average energy potential of each countries across the years (Figure 1).

![](assets/img/portfolio/solar/avg-solar-by-country.png)

*Figure 1: Average Energy Potential by Country for 1968 to 2015*

We see that the regions with greater solar energy potential are at the lower regions, closer to the Equator. This makes sense since the sun's rays strike the Earth's surface most directly at the Equator. The colour gradient is also consistent from bottom up which also shows high correlation between neighbouring countries from similar levels of exposure to the sun.

I use `KMeans` to cluster the countries, and chose a range of 2 to 10 clusters. Based on this, using the elbow method and based on the distortion score, decide which is the optimal number of clusters.

Distortion score is the sum of squared distances from each point to its assigned center (ie. sum of squared errors). The elbow method seeks to identify a point as number of clusters increase, where the distortion score start to flatten, forming the elbow. This is then determined to be the ideal number of clusters for the data (Figure 2).

![](assets/img/portfolio/solar/distortion-score.JPG)

*Figure 2: Distortion score elbow for KMeans clusters 2 to 10*

From here, we see that 5 clusters is ideal. The elbow method mostly serves as a guide, and should be considered alongside **silhouette score**. **Silhouette score** considers both the average intra-cluster distance and average inter-cluster distance. A score close to 1 means that the clusters are well apart from each other and clearly distinguished. Figure 3 shows the the silhouette scores and distribution of data points across the clusters for 4 clusters, 5 clusters, and 6 clusters.

![](assets/img/portfolio/solar/silhouette-scores.JPG)

*Figure 3: Silhouette scores for clusters 4 to 6*

We'd want to lookout for a few things:

1. Positive silhouette coefficient values

A negative silhouette coefficient value means that the sample (in this case, the country), is better off assigned to another cluster. Based on the plots above, 6 clusters and 7 clusters are suboptimal.

2. Silhouette score for clusters above the average silhouette score

6 clusters and 7 clusters have clusters below the average silhouette score so we'll just consider 3-5 clusters.

3. Thickness of the silhouette plots

Between 3, 4 and 5 clusters, the plot with 5 clusters have a more uniform cluster thickness than the rest. Therefore, 5 clusters is probably indeed the most optimal.

Looking at the intercluster distances for clusters 4 to 6 in Figure 4, from cluster 6, there seem to be too many overlapping regions. Cluster 5 too showed some overlaps.

![](assets/img/portfolio/solar/intercluster-distance.JPG)

*Figure 4: Intercluster distance for clusters 4 to 6*

However, we bear in mind that it is not essential that we get exact distinct clusters since the purpose of clustering is mainly for eaasier analysis and would not affect prediction of solar energy potential for the countries.

Based on this, we will go forward with 5 clusters using KMeans clustering.

I applied the cluster labels, and these are the countries in the different clusters (Figure 5):

![](assets/img/portfolio/solar/countries-by-cluster.JPG)

*Figure 5: Countries in respective clusters*

I then proceed to explore the data by looking at one country in each cluster :

![](assets/img/portfolio/solar/country-in-cluster.JPG)

*Figure 6: Selected country in each cluster*

### Data Exploration
---

Considering the voluminous data, I decided to just look at 10 years' worth of data to explore. I did a sanity check on the data points, firstly that there are no negative values, and secondly, that there are no values greater than 1 (since values are in %). None were noted. So I proceeded with the exploration.

First I look at how solar energy potential changes within a day (24 hours) (Figure 7).

![](assets/img/portfolio/solar/24h-by-country.JPG)

*Figure 7: Hourly solar energy potential for each country*

From here, we see that :

- There is only energy potential between 0600H and about 1700H, which is daylight period. Logically, this means no energy potential during nighttime.
- **Croatia** has the highest energy potential while **Norway** and **Finland** has the lowest energy potential.
- **Spain** has the "fattest" curve, which means that it has most hours exposed to sun, compared to other countries.
- The peak across all countries here are at the noon hour.

Next I consider the distribution of solar energy potential within the daylight hours (Figure 8).

![](assets/img/portfolio/solar/24h-distr-by-ctry.JPG)

*Figure 8: Distribution of hourly solar energy potential for each country*

Based on this,

- **Norway** and **Finland**'s peak is very close to 0% energy potential. This suggests that it is not wise for these countries to rely heavily on solar energy for power.
- The rest of the countries have pretty even distribution from 0% enery potential to about 0.6%, with peaks ranging from 0.3% to 0.5% energy potential.
- Spain seems to have the most area exposed which translates to greater energy potential. This corroborates with earlier analysis where Spain has the most hours exposed to sun, compared to other countries here.

Thirdly, I look at potential seasonality over the years, since these countries have seasons (ie. summer, autumn, winter and spring). Winter has shorter daylight hours, so I would expect months that coincide with winter season would show the lowest energy potential to other parts of the year, and this pattern would repeat every year.

Using just **Spain's** data, I plot the 10-year graph of energy potential to view seasonality (Figure 9).

![](assets/img/portfolio/solar/spain-seasonality-year.JPG)

*Figure 9: Spain's yearly seasonality of energy potential*

We see that:

- There is obvious seasonality across the years, where there are peaks and troughs at relatively consistent times of the year.
- This consistency may make it easier for prediction models to predict solar energy generation in future.

I plot the Spain's data using the NUTS 2 dataset, and had the same seasonality trend within the year. I went to look into the trend within months of a year, to confirm the seasons for Spain, that affect energy potential (Figure 10).

![](assets/img/portfolio/solar/spain-month-seasonality.JPG)

*Figure 10: Spain's seasonality of energy potential, by months*

Looking at how energy potential changes within a year, for Spain, hottest months of the year are between **April to August**, during spring and summer. The coldest months (with lack of sunlight) are from **December to March**, which is winter season.

Using the NUTS dataset, we also see the same trend for different regions of Spain (Figure 11).

![](assets/img/portfolio/solar/nuts-spain-month-seasonality.JPG)

*Figure 11: Spain's seasonality of energy potential, by months (NUTS2 system)*

Now that we've understood the seasonality in data, I proceed to <ins>forecast solar energy potential in Spain</ins> in Part 2.

{:.list-inline}
- Date: 26 Apr 2021
- Category: kmeans, silhouette score, distortion score, seasonality
