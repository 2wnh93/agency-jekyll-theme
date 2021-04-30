---
caption: #what displays in the portfolio grid:
  title: BlueSg Accessibility
  subtitle: Explores how accessible BlueSg are to residential areas
  thumbnail: assets/img/portfolio/bluesg/evcharge.jpeg

#what displays when the item is clicked:
title: BlueSg Accessibility
subtitle: Explore which residential area is most or least accessible to a BlueSg station and which proportion of residential areas are accessible to a BlueSg stations and which ones are not as accessible.
image: assets/img/portfolio/bluesg/evcharge.jpeg #main image, can be a link or a file in assets/img/portfolio
alt: image alt text

---

## Preamble

I've seen BlueSg cars around for a while a few years back and thought I wanted to give it a go, only to be disappointed that there aren't any charging stations near my home (ie. I would still have to take a bus and climb uphill after parking the BlueSg car), which would defeat the purpose of having the car.

So I got that idea out of my head, until recently, where I start to put a higher price on convenience (yes, public transport is not as convenient, especially when you stay on a hill and as I age, I value time and energy a lot more) and I also noticed more BlueSg stations around.

I then decided to do a more detailed study to **determine how accessible these stations are to the general population of Singapore** and explore the following questions:

- which residential block is *most* accessible to a BlueSg station
- which residential block is *least* accessible to a BlueSg station
- what proportion of residential areas are accessible to a BlueSg station and which ones are not as accessible.

## Extracting locations of all BlueSg charging stations in Singapore

I first webscrape from BlueSg website, to obtain the locations of BlueSg charging points around Singapore.

Once I've cleaned the data and do a sanity check on the number of BlueSg charging stations in my data, I then create a dataframe and proceed to visualise it on the map using *folium*.

![alt]({{ site.url }}{{ site.baseurl }}assets/img/portfolio/bluesg/chrgstnplot.jpeg)

A quick overview of the map shows that BlueSg charging stations are available in most parts of Singapore except for a few. For instance:

1. **Areas with higher proportion of private properties compared to HDBs** *eg. Bukit Timah/ Marine Parade/ East Coast/ Tanjong Katong*

Residents in such areas are generally more wealthy so we would expect residents here to have already owned at least a car. Therefore, not very practical for BlueSg to service such areas.


2. **Industrial areas** *eg. Tuas/ Gul/ Jurong Island*

Most employees working in Tuas would have owned a car for ease of travel and if not, most employers in deep industrial areas would have a shuttle bus service for its employees, hence, there does not seem to be a need for BlueSg to service these areas as well.

## Obtain locations of all residential blocks in Singapore (HDBs and private properties)

I downloaded the HDB property information csv file from data.gov.sg. and proceed to obtain just the information that I needed ie. the address, which comprise the blk no. and street name.

As it turns out, not all addresses were able to be geocoded by *geopy*, but fortunately, that's a small percentage. We got a good 83% of data to work on.

Now we move on to extract information on private residential areas. This is quite tricky as data.gov.sg does not have all addresses of private residential properties in Singapore. URA has a map of all residential properties but the interface is impossible to webscrape from.

Nevertheless, I managed to find a comprehensive website which has a list of all private residential properties in Singapore and proceed to webscrape from it.

It's got a pretty clean data, so there is not much processing needed.

Combining both HDB and private properties addresses, I then visualise this on the map.

![alt]({{ site.url }}{{ site.baseurl }}assets/img/portfolio/bluesg/residentialplot.jpeg)

## Compute haversine distances between BlueSg charging stations and residential blocks

Haversine distances are computed using `sklearn neighbours library`. With all distances between all charging stations and addresses, I can answer the questions above.

## Which residential area is the most accessible to a BlueSg charging station?

I sorted the dataframe based on distance.

Results:

![alt]({{ site.url }}{{ site.baseurl }}assets/img/portfolio/bluesg/mostaccessible.jpeg)

We see that 35A, Marine Crescent is most accessible to a BlueSg charging station at about 1.86 metres away from it.

We can also pick up the top 5 most accessible blocks to a BlueSg charging station.

These are the five most accessible blocks to a BlueSg charging station :

![alt]({{ site.url }}{{ site.baseurl }}assets/img/portfolio/bluesg/5mostaccessible.jpeg)

Let's look at this in a map.

![alt]({{ site.url }}{{ site.baseurl }}assets/img/portfolio/bluesg/5mostaccessibleplot.jpeg)

## Which residential area is the least accessible to a BlueSg charging station?

From the sorted data, we create a new dataframe which contain the minimum distance of a residential address to a charging station. The ones with the longest minimum distance from the charging station will be the least accessible.

![alt]({{ site.url }}{{ site.baseurl }}assets/img/portfolio/bluesg/leastaccessible5.png)

Most are at Changi Village area.

In a map,

![alt]({{ site.url }}{{ site.baseurl }}assets/img/portfolio/bluesg/leastaccessible5plot.png)

Red markers are the homes while the green markers are the nearest BlueSg charging stations. Changi Village does not seem very accessible even via public transport. It is likely that anyone who lives there or planning to travel to Changi Village, owns at least a car.

## Which residential area is accessible, within 200m, to a BlueSg charging station?

I slice the sorted dataframe to take in only those within 200m distances and then plot this in a map.

![alt]({{ site.url }}{{ site.baseurl }}assets/img/portfolio/bluesg/accessible200mplot1.png)

Seems like it is pretty spread out across Singapore. However, there are still not many residential areas that are accessible to a BlueSg charging station.

If we zoom into one location, say Whampoa area, we can see a charging station (in Teal marker) servicing residential areas (in Red marker) which are within 200m.

![alt]({{ site.url }}{{ site.baseurl }}assets/img/portfolio/bluesg/accessible200mplot2.png)

## Overall Review

While there is a good spread of BlueSg charging stations all around Singapore, there aren't many that are accessible (ie. within 200m) to most residential areas, including mine. Therefore, I would not consider subscribing to one, unless the convenience of having a car greatly outweigh the inaccesibility costs (ie. using public transport to go home) and inconvenience costs.

<u>Other considerations</u>

It is possible that BlueSg stations that are not within accessible distance to residential areas serve as merely a transporting vehicle from one place to another depending on one's lifestyle.

Also, while I define accessibility as 200m, others may deem a walking distance of 600m as accessible for them, and therefore, a BlueSg station I deem as inaccessible might be deemed as accessible to them.  

{:.list-inline}
- Date: 05 Oct 2020
- Category: webscraping, haversine Distance, pandas, sklearn
