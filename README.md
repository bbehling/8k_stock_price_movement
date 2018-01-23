# Buy the Rumor, Sell the News
#### Predicting stock price directional movement after 8-K filings
*This project is intended to explore machine learning concepts using stock market data and not to provide trading recommendations.*

## Background and motivation
A form 8-K is a general form used by publicly traded companies in the United States to notify shareholders of specific events that may be important. These events can include bankruptcy, the issuing of new shares, change in accountants, and more. [Read more about 8-K's at wikipedia](https://en.wikipedia.org/wiki/Form_8-K).

This project aims to answer two areas of question:

1) Can we evaluate the information gain from 8-K text through natural language processing? If so, can this along with technical indicators about the stock price's recent performance be used to accurately predict stock price movement following the filing of an 8-K?

2) Can we use our model to find actionable trading opportunities through both long and short strategies?

## Data
* More than 48,000 8-K's scraped from sec.gov for all S&P 500 companies. ([See my gist on how to web scrape sec.gov.](https://gist.github.com/Luke-G-B/bacbdeeb3c5502651fc6e84e5c50edb1))
* Stock price data collected from the Alpha Vantage API
  * Relative Strength Index
  * Consumer Channel Index
  * On Balance Volume
  * Moving Standard Deviation
  * Moving Rate of Change

## Model flow
#### Natural Language Processing (NLP) model
**Label**: To evaluate information gain from the 8-K release, the price before the filing is divided by the price after the filing. For example, if the 8-K was filed after market close on trading day one, the closing price on trading day one divided by the opening price on trading day two is used as the label.

**Feature matrix**: The corpus of 8-K texts is vectorized into a bag of words. The bag of words is then used as the feature matrix in a Multinomial Naive Bayes model, which classifies each 8-K into either a negative class, predicting the stock price will go down, or a positive class, predicting the stock price will go up.  

#### Technical Indicators (TI) model
**Label**: The same label as above is used to evaluate the 8-K information gain, however the label is adjusted to the next day's opening price divided by the next day's closing to predict on actionable stock trading opportunities following the filing.

**Feature matrix**: Relative Strength Index, Consumer Channel Index, On Balance Volume, Moving Standard Deviation, Moving Rate of Change over a rolling five day interval are downloaded from the Alpha Vantage API or engineered from the Alpha Advantage data.

#### NLP + TI
**Feature matrix**: The NLP classifications are combined with the TI features and trained and evaluated on both labels.

## Evaluation
All data is split into training and holdout sets. The models are trained on the training set and evaluated on the holdout set. All true predictions are important, because both are actionable. Therefore, all models are evaluated on overall accuracy, and estimated rate of return.

#### Information Gain
Accuracy score, Accuracy by accuracy compliment plot (), AUC, for all three models and random
Profit curve
**NLP model**

**TI model**

**NLP + TI model**

## Conclusion
