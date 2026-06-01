---
author: "Kyle Jones"
date_published: "March 27, 2024"
date_exported_from_medium: "November 10, 2025"
canonical_link: "https://medium.com/@kyle-t-jones/visualizing-the-normal-distribution-with-python-and-matplotlib-c501e3c594f8"
---

# Visualizing the normal distribution with Python and Matplotlib This is a simple python project to show how to simulate a normal
distribution and plot it using Matplotlib.

### Visualizing the normal distribution with Python and Matplotlib
This is a simple python project to show how to simulate a normal distribution and plot it using Matplotlib.

Another early step in data analysis is the building graphical summaries of the data. These help us focus in on different attributes of the data. One of the most important tools for analyzing numerical data is a histogram.

A histogram is a type of bar chart that divides the total range of the data into a number of "bins" of equal width and then sorts the data into the bins based upon those ranges. It answers the questions about

1.  [center (Where do the numbers tend to concentrate?),]
2.  [spread (How variable is the data?), and]
3.  [shape (In what pattern do the data tend to fall?).]

```python
import numpy as np
import matplotlib.pyplot as plt
%matplotlib inline

def plot_norm_hist(s, mu, sigma, vline = True, title= True):
    count, bins, ignored = plt.hist(s, 30, density=True)
    plt.plot(bins, 1/(sigma * np.sqrt(2 * np.pi)) *
               np.exp( - (bins - mu)**2 / (2 * sigma**2) ),
         linewidth=2, color='r')
    
    if vline:
        lline = -.67*sigma + mu
        uline = .67*sigma + mu
        plt.axvline(lline, color='g')
        plt.axvline(uline, color='g')

    if title:
        plt.title("Normal distribution with mean: {:.02f} and StDev: {:.02f}".format(mu, sigma))
    return plt.show()

mu, sigma = 0, 1 # mean and standard deviation
s = np.random.normal(mu, sigma, 1000)

plot_norm_hist(s, mu, sigma, vline=True, title=True)
```


<figcaption>A histogram showing 1,000 random values. The mean is 0 and the standard deviation is 1.</figcaption>


We can see how the histogram "smooths" as we increase the number of simulated values from 1,000 to 100,000.

``` 
mu, sigma = 50, 10 # mean and standard deviation
s = np.random.normal(mu, sigma, 100000)

abs(mu - np.mean(s))

abs(sigma - np.std(s, ddof=1))

count, bins, ignored = plt.hist(s, 30, density=True, alpha=.3)
plt.plot(bins, 1/(sigma * np.sqrt(2 * np.pi)) *
               np.exp( - (bins - mu)**2 / (2 * sigma**2) ),
         linewidth=2, color='r')
lline = -.67*sigma + mu
uline = .67*sigma + mu
plt.axvline(lline, color='g')
plt.axvline(uline, color='g')
plt.title("Normal distribution with mean: {:.02f} and StDev: {:.02f}".format(mu, sigma))
plt.show()
```


Now we can apply some colors to draw attention to different parts of the data. I wouldn't use all of these in real life but I'm including them so you can see how they could be layered using `axvspan` .

``` 
mu, sigma = 0, 1 # mean and standard deviation
s = np.random.normal(mu, sigma, 1000)

abs(mu - np.mean(s))

abs(sigma - np.std(s, ddof=1))

count, bins, ignored = plt.hist(s, 30, density=True, alpha=.5)
plt.plot(bins, 1/(sigma * np.sqrt(2 * np.pi)) *
               np.exp( - (bins - mu)**2 / (2 * sigma**2) ),
         linewidth=2, color='r')
plt.axvspan(-4, -.67, color='g', alpha=0.1)
plt.axvspan(-.67, 0, color='g', alpha=0.2)
plt.axvspan(0, .67, color='g', alpha=0.3)
plt.axvspan(.67, 4, color='g', alpha=.4)
plt.show()
```


Another graphical tool for numerical data is the box plot. This plot typically shows five numbers: the minimum value, the 25th percentile, the median, the 75th percentile, and the maximum value.

The 25th percentile is the number such that (approximately) 25% of the data falls below it and (approximately) 75% of the data falls above it.

Outliers, data values that are extremely small or large compared to the rest of the data, are typically plotted separately.

``` 
fig1, ax1 = plt.subplots()
ax1.set_title('Basic Plot')
ax1.boxplot(s, showfliers=False, vert=False)
```


### Related Stories
- [[Monte Carlo simulation using Black-Scholes for stock price in Python](https://medium.com/@kylejones_47003/monte-carlo-simulation-using-black-scholes-for-stock-price-in-python-808574935473)]
- [[Time Series Forecasting for Stock Prediction in Python](https://medium.com/python-in-plain-english/time-series-forecasting-for-stock-prediction-in-python-710a88b7ccbb)]
- [[Building a Recommendation Engine using Association Rules for item to item similarity in R](https://medium.com/@kylejones_47003/association-rules-for-item-to-time-personalization-in-r-9d6de7d6db8e)]
