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

{:.list-inline}
- Date: 8 Oct 2020
- Category: Illustration
