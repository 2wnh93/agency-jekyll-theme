---
caption:
  title: Covid19 Impact on Stock Performance
  subtitle: Explore how Covid19 affected stock performance for various industries
  thumbnail: assets/img/portfolio/covid19onstock/header.jpeg

title: Covid19 Impact on Stock Performance
subtitle: Explore how Covid19 affected stock performance for various industries - Technology, Aviation, Healthcare, Energy (Oil) and Energy (Alternative)
image: assets/img/portfolio/covid19onstock/header.jpeg

---

## Preamble

As economies around the world are suffering from the impact of Covid-19, various industries are affected in different ways. Aviation companies are struggling as countries close their borders under lockdown, while pharmaceutical companies are taking centre stage in the race towards treatment approval. Also, Tech companies seem to be doing well.

In this project, we will look at the **impact of Covid-19 on a basket of stocks in each of the following industries**:
* Technology
* Aviation
* Healthcare
* Energy - Oil
* Energy - Alternative

After importing the necessary libraries, I've selected 5 stocks for each industry below:

```python
stockset = {
    'tech': ['TSLA', 'AAPL', 'GOOG', 'AMZN', 'ZM'],
    'avia': ['AAL', 'UAL', 'LUV', 'DAL', 'JBLU'],
    'phar': ['PFE', 'JNJ', 'GSK', 'MRNA', 'BNTX'],
    'fuel': ['TNK', 'TRMD', 'TALO', 'HMLP', 'WLL'],
    'alte': ['BEP', 'FSLR', 'NEE', 'CSIQ', 'JKS']
}
```
Extracted data from `Yahoo Finance` for prices of each stock.

## T E C H

Plot daily closing stock price movements for each selected tech stock.

![](assets/img/portfolio/covid19onstock/Techstock.jpeg)

The **overall upward trend** shows that the Tech stocks above are pretty resilient as we can see that most have rebounded from a drop in Mar-20, upwards from Apr-20 onwards.

Looking at returns from beginning of 2020 to date..

![](assets/img/portfolio/covid19onstock/techreturns2020.png)

Looking at how much the stocks multiplied from the beginning of 2020 up to date, we see that **both TSLA and ZM outperformed the basket of stocks** with stock prices at 4.94x and 7.02x, respectively, compared to the start of 2020. The average increase in stock prices for the basket of stocks is about 3.25x.

Possible reasons...

<u>TSLA</u>

Tesla is one of a kind. Its innovation rate is superior to any other companies and its technology is further ahead from others in a field that has little to no competition. The rally in 2020 could be contributed by confidence in the Company as it outperformed its earnings forecast in Q4'19. At the current price, it seems like investors is aware of how much potential Tesla has for growth in future.

<u>ZM</u>

Zoom is a video conferencing company whose role is ever more important since Covid-19 as people around the world work from home and practice social distancing (therefore no face-to-face meetings) to curb the spread of the virus. It will take some time before life gets back to 'normal'. Meanwhile, adjusting to a 'new normal' includes using Zoom to communicate with one another while practising social distancing in a bid to curb the virus.  

![](assets/img/portfolio/covid19onstock/techdailyreturns.png)

From the graph above, the lowest daily return for each Tech stock (except TSLA) was in Mar-20 period. Subsequently there were no lower % daily returns.

Outliers..

<u>TSLA - Lowest daily return in Sep'20 of -0.2%</u>

Tesla's dip in Sep-20 was after Battery Day likely from lower investor confidence when Musk announced delay in high-volume production with cheaper Tesla cars to 2022.

<u>ZM - Highest daily return in Sep'20 of 0.4%</u>

Zoom's stock price reached a record high at 1-Sep-20 following its impressive Q2 results (Y-o-Y growth rate of 458%. *Source: Yahoo News*)

## A I R L I N E

Plot daily closing stock price movements for each selected airline stock.

![](assets/img/portfolio/covid19onstock/airlinestock.png)

There is a huge contrast from these results compared to Tech stocks performance. There is no rebound, with a general downtrend from the beginning of 2020 to date.

There is a slight uptick in Jun-20 probably from lockdown restrictions easing and those visiting family and friends boosted interstate air travels.

Looking at returns from beginning 2020 to date..

![](assets/img/portfolio/covid19onstock/aviareturns2020.png)

Airline stocks have not been performing ever since Covid-19 hit in Mar-20, with all of the stocks above valued at less than the stock price at the beginning of 2020.

Apart from interstates, the borders will probably not open so soon except for travel between selected countries which have the virus under control. It is hard to rebound this period, when the main revenue stream is pretty much non-existent during this period.

![](assets/img/portfolio/covid19onstock/airlinedailyreturns.png)

From the graph above, the lowest daily return for each Airline stock was in Mar-20 period, as expected. Subsequently there were no lower % daily returns.

Outliers...

<u>JBLU - Highest daily return in end Mar'20 of 0.37%</u>

Jet Blue had high daily returns in end Mar-20 was after the Trump Administration passed and enacted the Coronavirus Aid, Relief and Economic Security (CARES) Act, which sets aside $25 billion in payroll support for airline employees through to 30-Sep-20. This news probably brought more investor confidence. (*Source: JetBlue Airways, Investor Relations*)

<u>AAL - Highest daily return in Jun'20 of 0.41%</u>

American Airline's stock had the highest daily return in Jun-20 following an expectation that flights would continue from Jul-20 onwards. The airline said to be increasing its capacity in July compared to past months, due to improving booking trends.

## H E A L T H C A R E

Plot daily closing stock price movements for each selected healthcare stock.

![](assets/img/portfolio/covid19onstock/healthstock.png)

I would expect healthcare companies to be doing well this period since Covid-19 would result in heavy demand from this sector. However, I see some mixed effects of Covid-19 on these healthcare stocks. JNJ, MRNA and BNTX seem to have an overall upward trend from the beginning of 2020 to date, while PFE and GSK is not doing as well.

Looking at returns from beginning 2020 to date..

![](assets/img/portfolio/covid19onstock/pharreturns2020.png)

Both the MRNA and BNTX stocks has surpassed the average performance of this basket of stocks with returns 3.72x and 2.59x of the beginning of 2020. The stocks grew at an average of 1.83x since the beginning of 2020.  

![](assets/img/portfolio/covid19onstock/phardailyreturns.png)

BNTX had the highest daily return in Mar-20 of 0.6% before it dropped to a -0.4% return subsequently, suggesting that investors who bought the stock are going long on BNTX.

<u>BNTX - Highest daily return in Mar'20 of 0.6%</u>

BNTX stock price soared from investor enthusiasm as BioNTech announced its partnership with pharmaceutical giant Pfizer(PFE) to develop and distribute a vaccine to immunize people against Covid-19. The companies expect BioNTech's Covid-19 mRNA vaccine candidate, BNT162, to enter clinical testing by end of Apr-20. (*Source: BioNTech, Press Release*)

## O I L & G A S

Plot daily closing stock price movements for each selected oil & gas stock.

![](assets/img/portfolio/covid19onstock/oilstock.png)

From here, there is a clear general downtrend except for WLL stock which rose above every other stock here in Sep-20. In Mar-20 however, all stocks here declined except for TNK, which rose during the month.

<u>TNK</u>

While oil prices crashed in Mar-20, Teekay Tanker's stock price rose during the month. Teekay Tankers is a tanker operator. The increase was brought about by ultracheap oil due to lower oil prices from increase in supply. Production increase has increased tanker demand.

Looking at returns from beginning 2020 to date..

![](assets/img/portfolio/covid19onstock/fuelreturns2020.png)

Generally the stocks did not do well from the beginning of 2020 to date, worsened by Covid-19.

WLL stock ended at 2.6x of the stock price from the beginning of 2020, coming mainly from a sharp increase in Sep-20. However, this is from a restructuring done after WLL filed for bankruptcy early in 2020.

![](assets/img/portfolio/covid19onstock/oilrtns2.png)

As expected, the lowest daily returns of the stocks are in Mar-20, from Covid-19 impact.

WLL stock had some high daily returns from Mar-20 to Jun-20, which probably has to do with its restructuring process. Apart from that, the rest of the stocks hover around the average daily returns.

## A L T E R N A T I V E  E N E R G Y

Plot daily closing stock price movements for each selected oil & gas stock.

![](assets/img/portfolio/covid19onstock/altstock.png)

Compared to oil and gas stocks above, the alternative energy stocks here have a general upward trend to date, with a slight drop in Mar-20.

Looking at returns from beginning 2020 to date...

![](assets/img/portfolio/covid19onstock/altreturns2020.png)

In spite of the impact of Covid-19 in Mar-20, the alternative energy stocks above performed better subsequently.

![](assets/img/portfolio/covid19onstock/altreturns.png)

JKS stock had the lowest daily return in Mar-20 of -0.29%.

<u>JKS - Lowest daily return in Mar-20 of -0.29%</u>

JinkoSolar Holding Co. Ltd. is one of the largest and most innovtive solar module manufacturers. The drop in daily returns was probably becayse it's Q4 earnings missed analysts' estimates.

## Overall Review

It appears that all industries are adversely affected by Covid-19, however, they rebound differently afterwards.

Tech and Alternative Energy rebounded higher than early 2020. Oil and gas and Airline industry will take longer to rebound from effects of Covid-19. Healthcare industry, will be one whose stock value is dependent on which company is able to first commercialise a vaccine.

{:.list-inline}
- Date: 8 Oct 2020
- Category: Yahoo Finance API, data extraction, data exploration, data analysis
