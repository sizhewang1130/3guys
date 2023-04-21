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
