# s_score
This repo contains files to download stock data, and run the algorithm to create Trading Signals using S-Score. This algorithm is from "Statistical Arbitrage in the US Equity Market" by Avellaneda &amp; Lee. 

## How to Start:
1) Create a Virtual Environment and install all the packages from requirements.txt
2) Download the Notebook "download_data.ipynb". In this notebook itself, we have created a list of 508 arbitrary stocks ranging from Large-Cap Stocks, Growth stocks, Value stocks, Low volatility stocks, Small-cap stocks, Momentum stocks, Additional mixed stocks. We will also down the data of the ETF "SPY". Run this notebooks and two csvs will be created. 
3) Now in the same folder where these files are created, download the file "signals.ipynb". And run it. One cell which finds the s_score of all the 508 stocks takes about 4 mins to run. Because we have been calculating the s-score in a rolling window of 60 days. Therefore, for every stocks it takes sometime.

## Steps of the Algorithm:
1) First we calculate the close to close returns of all the stocks. The 508 stocks.
2) We standardize these stocks.
3) We calculate the Covariance Matrix of these stocks.
4) We perform PCA on the Covariance Matrix. We derive the Eigenvectors of these Covariance Matrix. We can also check the percentage of variance explained by the eigenvalues.
   <img width="800" alt="image" src="https://github.com/user-attachments/assets/83c8d83d-c227-4f65-8411-633b8c8d02cb" />
5) 

