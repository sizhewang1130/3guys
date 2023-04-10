# Research Proposal: < Layoffs>
By Sizhe Wang, Chengxi Wu, and Jerrick Ren
## Research Question
### Big picture:
A wave of layoffs has swept across American businesses in 2022.The cuts stem from slower business growth, inflation paired with rising labor costs.Our project is focus on illustrating the company’s stock price changing that caused by the layoff and  finding out the correlation between them.This can help investors and analysts evaluate the potential risks and opportunities associated with layoffs and make informed investment decisions.
### Specific Research Question:
Exploring the factors that are most strongly associated with layoffs: We want to identify the key drivers of layoffs, such as changes in the industry, company performance, or macroeconomic factors. This can help investors and analysts better understand the underlying causes of layoffs and predict which companies are most at risk.
We are trying to predict stock prices based on the company’s layoff number.
### Testing hypotheses:
- H0: Companies that experience layoffs are more likely to experience a decline in stock prices compared to companies that do not experience layoffs.
- H1: Companies that experience layoffs are unlikely to experience a decline in stock prices compared to companies that do not experience layoffs.

## Necessary Data
### The final dataset should include:
1. The Observations should be GICS Sector
2. Sample Period: Oct 2020 - Jul 2022.
3. Sample Conditions: 
    - GICS Sector: Financials, Information Technology, Industrials
    - If available, use the period from Jan 2020 to Dec 2022.
4. Variables (Stock price, Number of layoffs, Symbol, GICS Sector, News Positive Sentiment, News Negative Sentiment, Time Period) are necessary.
### Now dataset and some changes of the dataset:
We already have data from Oct 2020 - Jul 2022 from Kaggle, we might do some changes to the raw code that the author provided to get data from Jan 2020 to Dec 2022. 
### Import Raw data: 
https://www.kaggle.com/datasets/parsabg/stocknewseventssentiment-snes-10?select=data.csv 
### Transform:
Make changes to the raw code, and change the data period from Jan 2020 to Dec 2022. Got the new dataset to use. 

