# Welcome to our [team project website!](https://julioveracruz.github.io/testwebsite/)

This is a website to showcase our final project for FIN 377 - Data Science for Finance course at Lehigh University.

## The files should be accessed in this order:
- [data.ipynb](https://github.com/sizhewanglehigh/3guys/blob/main/data.ipynb)
- [code.ipynb](https://github.com/sizhewanglehigh/3guys/blob/main/code.ipynb)
- [data visualization.ipynb](https://github.com/sizhewanglehigh/3guys/blob/main/Data%20Visualization.ipynb)

## Table of contents
1. [Introduction](#introduction)
2. [Methodology](#meth)
3. [Data processing](#data)
4. [Analysis Section](#section3)
5. [Summary](#summary)

## Introduction  <a name="introduction"></a>

Recent years have been marked by a wave of layoffs that has swept across American businesses, leaving a trail of job losses and economic uncertainty in its wake. The pandemic has disrupted industries across the board, with many companies facing a decline in revenues and profits. In response, businesses have been forced to make difficult decisions, with layoffs becoming an increasingly common strategy for reducing costs and improving their bottom line. The cuts have affected a broad range of industries, from hospitality and retail to finance and technology. While some companies have been able to weather the storm and maintain their profitability, others have struggled to stay afloat, with layoffs becoming a necessary and sometimes painful step. Our project seeks to shed light on the impact of layoffs on the stock prices of affected companies, as well as the broader economic implications of these cuts. By analyzing the stock prices of companies before and after a layoff announcement, we aim to identify any patterns or trends that may exist. Ultimately, our goal is to provide valuable insights to investors and analysts, helping them to evaluate the potential risks and opportunities associated with layoffs and make informed investment decisions. By providing a deeper understanding of the impact of layoffs on the economy and the stock market, we hope to contribute to a more informed and nuanced conversation around this important issue.

## Methodology <a name="meth"></a>
We only selected companies in the United States and only chose companies whose stocks are traded on the public market.
<br>
Here is some code that we used to develop our analysis.

###  top 10 companies layoff
```python

top_10 = new.groupby('ticker').agg({'Laid_Off_Count': 'sum'}).reset_index().sort_values(by='Laid_Off_Count',ascending=False)[['ticker','Laid_Off_Count']].head(10)
import plotly.express as px
fig=px.bar(top_10,x='ticker',y='Laid_Off_Count',text='Laid_Off_Count',title='Top 10 Companies with Maximum Lay-offs',
      labels={'ticker':'ticker','Laid_Off_Count':'Laid_Off_Count'})
fig.show()
```

### top 10 location layoff
```python

us_df = new[new['Country'] == 'United States']
top_10 = us_df.groupby('Location_HQ').agg({'Percentage':'sum'}).sort_values(by='Percentage', ascending=False).head(10).reset_index()
# Using a custom color scale
custom_color_scale = ['#ff9999', '#66b3ff', '#99ff99', '#ffcc99', '#c2c2f0', '#ffb3e6', '#ff6666', '#c2f0c2', '#8080ff', '#f7d4f1']

fig = px.pie(top_10, names='Location_HQ', values='Percentage',
            color_discrete_sequence=custom_color_scale, # Use the custom color scale
            title='Top 10 Locations where most layoffs happened in USA.')

fig.show()
```
### Industry vs Layoff
```python
industry_df = new.groupby('Industry').agg({'Laid_Off_Count':'sum'}).sort_values(by='Laid_Off_Count', ascending=False).reset_index()
fig=px.pie(industry_df,names='Industry',values='Laid_Off_Count',
      color_discrete_sequence=px.colors.sequential.thermal,
       title='Industry v/s Layoffs')
fig.show()
```
### Stock price Change
```python
import pandas as pd
import plotly.subplots as sp
import plotly.graph_objs as go

# Create a subplot with 3 rows and 1 column
fig = sp.make_subplots(rows=3, cols=1)

# Create bar plots and add them to the subplot
fig.add_trace(go.Bar(x=date1['ticker'], y=date1['Daily Return Value yesterday'], name='Data 1'), row=1, col=1)
fig.add_trace(go.Bar(x=date1['ticker'], y=date1['Daily Return Value today'], name='Data 2'), row=2, col=1)
fig.add_trace(go.Bar(x=date1['ticker'], y=date1['Daily Return Value tomorrow'], name='Data 3'), row=3, col=1)

# Customize the layout
fig.update_layout(title='Combined Plots', showlegend=False)

# Update xaxis and yaxis titles
# fig.update_xaxes(title_text='ticker', row=1, col=1)
# fig.update_xaxes(title_text='ticker', row=2, col=1)
fig.update_xaxes(title_text='ticker', row=3, col=1)

fig.update_yaxes(title_text='yesterday', row=1, col=1)
fig.update_yaxes(title_text='today', row=2, col=1)
fig.update_yaxes(title_text='tomorrow', row=3, col=1)

# fig.update(config=dict(displayModeBar=True, scrollZoom=False))

# Display the combined plot
fig.show()
```
### Regression
```python
from statsmodels.formula.api import ols as sm_ols
from statsmodels.iolib.summary2 import summary_col # nicer tables

reg1 = sm_ols('diff~l_Laid_Off_Count', data=new).fit()
reg1.summary()
```

```python
from statsmodels.formula.api import ols as sm_ols
from statsmodels.iolib.summary2 import summary_col # nicer tables

reg1 = sm_ols('l_diff~Percentage', data=new).fit()
reg1.summary()
```


## Data Processing <a name="data"></a>
Our main data sources are Yahoo Finance and layoff data from kaggle. To acquire adj close price and daily return for each firms, we first set up the start time and end time, after that, we use the .pct_change to get daily return. After we got the daily return, we merge it with layoff data, and we save this dataset as ‘newdata.csv’.\
<br>
During the period under investigation, we downloaded the daily prices of the S&P 500 stock market index and calculated the daily return for each day using the same method. We then calculated the daily return for each company and subtracted the daily return of the S&P 500 from it, resulting in a difference between the two. We also took the logarithm of this difference and Laid_Off_Count, which allowed us to better analyze the data and identify patterns or trends

## Analysis Section <a name="section3"></a>

We calculate difference between company daily return value and market (SP500) daily return value, and save it into new column('diff')

### Regression 1 (Laid Off Count vs diff)
<br>
![image](https://user-images.githubusercontent.com/111511037/235481640-f1f61541-291e-4cc4-95f4-e55e7f643357.png)

<img class="img-circle" src="code/regression 1.png" width="50%">

### Regression 2 (log(Laid Off Count) vs diff)
<br>
![image](https://user-images.githubusercontent.com/111511037/235482715-3d0ea98b-4855-4d9f-9766-c03f61e29289.png)

<img class="img-circle" src="code/regression 2.png" width="50%">

### Regression 3 (Percentage vs diff)
<br>
![image](https://user-images.githubusercontent.com/111511037/235482903-aa826945-3925-4fd1-b275-2798f5ffb93c.png)

<img class="img-circle" src="code/regression 3.png" width="50%">

Here are some graphs that we created in our analysis.

[top 10 location layoff](https://htmlpreview.github.io/?https://github.com/sizhewanglehigh/3guys/blob/main/top%2010%20location%20layoff.html)

It is useful to analyze which industries are experiencing the most job losses. This information can provide insights into which sectors of the economy are struggling, and can help policymakers and businesses develop strategies to address the problem
<br><br>
[Industry vs Layoff](https://htmlpreview.github.io/?https://github.com/sizhewanglehigh/3guys/blob/main/Industry%20vs%20layoff.html)

By analyzing the data and identifying which industries have been most affected by layoffs, policymakers and businesses can develop strategies to support workers and help the affected industries recover. This may include providing financial support or training programs to help workers transition to new jobs or supporting the growth of industries that are less affected by job losses.
<br><br>
[top 10 companies layoff](https://htmlpreview.github.io/?https://github.com/sizhewanglehigh/3guys/blob/main/top%2010%20company%20layoff.html)

By analyzing the data and identifying which companies have been most affected by layoffs, policymakers and businesses can develop strategies to support workers and help the affected companies recover. This may include providing financial support or training programs to help workers transition to new jobs or supporting the growth of companies that are less affected by job losses. It can also help investors and shareholders understand which companies may be facing challenges and inform their investment decisions.
<br><br>
[Stock price change](https://htmlpreview.github.io/?https://github.com/sizhewanglehigh/3guys/blob/main/stock%20price%20change.html)

By analyzing the data and identifying how layoffs have affected stock prices, investors and analysts can make more informed investment decisions and adjust their expectations for the future performance of the companies in question.
More analysis.

## Summary <a name="summary"></a>
Overall, we found that there was no significant correlation between a company's layoff rate and changes in its stock price, as a company's stock price can be influenced by a variety of factors. Additionally, we found that layoff rates vary across different industries and regions, with higher layoff rates being more common in industries with closer ties to the economy. In terms of stock prices, different companies experience different changes, and we cannot simply judge changes in stock price based solely on whether or not the company has laid off employees or the number of employees laid off.
<br>
## About the team
<img src="031013c219dd41d2366805bc591182e.jpg" alt="Damon" width='300'/>
<br>
Damon is a Master student at Lehigh studying Business Analytics.
<br><br><br>
<img src="selfie.jpg" alt="Sizhe" width='300'/>
<br>
Sizhe is a Master student at Lehigh studying Business Analytics.
<br><br><br>
<img src="a2b8ec7db8bde8ded08644bef9769e2.jpg" alt="Jerrick" width='300'/>
<br>
Jerrick is a MBA student at Lehigh University

## More 

To view the GitHub repo for this website, click [here](https://github.com/sizhewanglehigh/3guys).
