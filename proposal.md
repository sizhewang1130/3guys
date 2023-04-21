# Research Proposal: < Layoffs>
By Sizhe Wang, Chengxi Wu, and Jerrick Ren
## Research Question
### Big picture:
A wave of layoffs has swept across American businesses in 2022.The cuts stem from slower business growth, inflation paired with rising labor costs.Our project is focus on illustrating the company’s stock price changing that caused by the layoff and  finding out the correlation between them.This can help investors and analysts evaluate the potential risks and opportunities associated with layoffs and make informed investment decisions.

### Specific Research Question:
1. Whether the layoff would affect stock price? If yes, positive or negative?
2. How does stock prive react to the different number of layoff news?
3. Whether the changing of stock price would be different in differnt firm/sub-industry/Sector?
4. Whether layoff new in on sub-industry/sector will affect another sub-industry/sector stock price?
    - correlation 
### Testing hypothesis:
- H0: Companies that experience layoffs are more likely to experience a decline in stock prices compared to companies that do not experience layoffs.
- H1: Companies that experience layoffs are unlikely to experience a decline in stock prices compared to companies that do not experience layoffs.

### steps 
1. Download bad data 
2. select related predictors
3. Allocate the Adj close one day after layoff announcement 
    - The number of media coverage of layoff
    - Calculate daily Return value (Ho-Non-Hypothesis)
4. Regression modeling
    - (Return Value ~ # of firms layoff news + # of sub-industry layoff news)-summary the model 
5. visualization
    - replot 
    - time series 
    - correlation plot 
6. Analysis
7. Report

## Necessary Data
1. The Observations should be Symbol.
2. Sample Period: Oct 2020 - Jul 2022.

### Now dataset and some changes of the dataset:
- We have cleaned data already provided by Parsa Ghaffari and Parsa Ghaffari in Kaggle.
- The data already merged with SP 500.
- We need to calculate Daily Return Value, create dummy variables for news. 
- Remove some irrelavent columns ("Open", "High", "Low", "Close", "Volume", "Security").
- 10-k file sentiment analysis (considering)

### The final dataset should include:
1. Date
2. Symbol
3. GICS sector
4. GICS sub-industry
5. Adj.Close
6. Return Value
7. layoff news(1/0)
8. number of company layoff news
9. number of GICS sub-industry layoff news
10. number of GICS Sector layoff news

### Import Raw data: 
https://www.kaggle.com/datasets/parsabg/stocknewseventssentiment-snes-10?select=data.csv 
### Transform
```
stock[Daily RV]=stock["Adj.Close"].pct_change()
```

## How final dataset looks like:
```
import pandas as pd
import numpy as np

# Create some fake data
dates = pd.date_range('20220101', periods=7)
symbols = ['AAPL', 'GOOG', 'AMZN', 'FB', 'NFLX', 'TSLA', 'MSFT'][:7]
gics_sectors = ['Technology', 'Technology', 'Consumer Discretionary', 'Communication Services', 'Communication Services', 'Consumer Discretionary', 'Technology'][:7]
gics_sub_industries = ['Internet Services & Products', 'Internet Services & Products', 'Internet & Direct Marketing Retail', 'Interactive Media & Services', 'Movies & Entertainment', 'Internet & Direct Marketing Retail', 'Systems Software'][:7]
adj_closes = np.random.randint(100, 1000, size=7)
return_values = np.random.rand(7)
layoff_news = np.random.randint(2, size=7)
num_company_layoff_news = np.random.randint(10, 50, size=7)

# Set num_company_layoff_news to 0 if layoff_news is 0
num_company_layoff_news[layoff_news == 0] = 0

# Create the dataframe
data = {'Date': dates,
        'Symbol': symbols,
        'GICS sector': gics_sectors,
        'GICS sub-industry': gics_sub_industries,
        'Adj.Close': adj_closes,
        'Return Value': return_values,
        'layoff news(1/0)': layoff_news,
        'number of company layoff news': num_company_layoff_news}

df = pd.DataFrame(data)

# Group the dataframe by GICS sub-industry and assign the sum of num_sub_industry_layoff_news for each group
df['number of GICS sub-industry layoff news'] = df.groupby('GICS sub-industry')['number of company layoff news'].transform('sum')
df['number of GICS Sector layoff news'] = df.groupby('GICS sector')['number of company layoff news'].transform('sum')

df
```

![image](https://user-images.githubusercontent.com/111511037/233721753-a4472465-ace8-459f-aa30-d0f6e4ec87e5.png)

