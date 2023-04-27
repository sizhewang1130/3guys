# Research Proposal: < Layoffs>
By Sizhe Wang, Chengxi Wu, and Jerrick Ren
## Research Question
### Big picture:
A wave of layoffs has swept across American businesses in 2022.The cuts stem from slower business growth, inflation paired with rising labor costs.Our project is focus on illustrating the company’s stock price changing that caused by the layoff and  finding out the correlation between them.This can help investors and analysts evaluate the potential risks and opportunities associated with layoffs and make informed investment decisions.

### Specific Research Question:
1. Whether the layoff would affect stock price? If yes, positive or negative?
2. Whether the changing of stock price would be different in differnt industry?
### Testing hypothesis:
- H0: Companies/industry that experience layoffs are more likely to experience a decline in stock prices compared to companies that do not experience layoffs.
- H1: Companies/industry that experience layoffs are unlikely to experience a decline in stock prices compared to companies that do not experience layoffs.

### steps 
1. Download layoff data and yfinance stock price.
2. Merge data by tickers (layoff data and yfinance stock price)
3. export to a new csv
4. import the new csv we just made
5. select related predictors
6. Calculate daily Return value
7. Regression modeling
8. . visualization
    - regplot
    - bar chart
    - pie plot
9. Analysis
10. Report

## Necessary Data
1. The Observations should be ticker.
2. Sample Period: Jan 1, 2020 to Mar 31, 2023

### Now dataset and some changes of the dataset:
- Our dataset having Laid_Off_Count and some company's basic information already
- We have to get the ticker by company name (Manully)
- Have to get the stock price within yfinance
- Have to calculate Daily Return Value
```
stock[Daily RV]=stock["Adj.Close"].pct_change()
```

### The final dataset should include:
1. Date
2. ticker
3. Industry
4. Stock Price
5. Daily Return Value today 
6. Daily Return Value yesterday
7. Daily Return Value tomorrow
8. Location
9. Laid_Off_Count
10. Laid_Off_Percentage
11. Stage
12. Country
13. Market Daily Return Value today 
14. Market Daily Return Value tomorrow
15. log(Laid_Off_Count)
16. Diff

### Raw data: 
https://www.kaggle.com/datasets/swaptr/layoffs-2022
### Transform
```
stock[Daily RV]=stock["Adj.Close"].pct_change()
```

## How final dataset looks like:
```
import pandas as pd
import numpy as np

# Generate fake data
dates = pd.date_range(start='2023-04-20', periods=7)
tickers = ['TICK' + str(i) for i in range(1, 8)]
industries = ['Industry' + str(i) for i in range(1, 8)]
stock_prices = np.random.uniform(10, 200, 7)
daily_returns_today = np.random.normal(0, 0.01, 7)
daily_returns_yesterday = np.random.normal(0, 0.01, 7)
daily_returns_tomorrow = np.random.normal(0, 0.01, 7)
locations = ['Location' + str(i) for i in range(1, 8)]
laid_off_counts = np.random.randint(10, 100, 7)
laid_off_percentages = np.random.uniform(0.1, 0.5, 7)
stages = ['Stage' + str(i) for i in range(1, 8)]
countries = ['Country' + str(i) for i in range(1, 8)]
market_daily_return_value_today = np.random.normal(0, 0.01)
market_daily_returns_today = [market_daily_return_value_today] * 7
market_daily_return_value_tomorrow = np.random.normal(0, 0.01)
market_daily_returns_tomorrow = [market_daily_return_value_tomorrow] * 7
log_laid_off_counts = np.log(laid_off_counts)
diffs = daily_returns_today - market_daily_returns_today
l_diff = np.log(diffs)

# Create the DataFrame
data = {
    'Date': dates,
    'ticker': tickers,
    'Industry': industries,
    'Stock Price': stock_prices,
    'Daily Return Value today': daily_returns_today,
    'Daily Return Value yesterday': daily_returns_yesterday,
    'Daily Return Value tomorrow': daily_returns_tomorrow,
    'Location': locations,
    'Laid_Off_Count': laid_off_counts,
    'Laid_Off_Percentage': laid_off_percentages,
    'Stage': stages,
    'Country': countries,
    'Market Daily Return Value today': market_daily_returns_today,
    'Market Daily Return Value tomorrow': market_daily_returns_tomorrow,
    'log(Laid_Off_Count)': log_laid_off_counts,
    'Diff': diffs,
    'log(Diff)': l_diff
}

df = pd.DataFrame(data)

# Display the DataFrame
df

```

![image](https://user-images.githubusercontent.com/112133489/235004747-0e3b8bd6-47b9-4710-b455-5872401f32dc.png)


