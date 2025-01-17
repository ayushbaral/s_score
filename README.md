## For Analysis look at signals.ipynb

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
   <img width="839" alt="image" src="https://github.com/user-attachments/assets/9af60b09-8872-4c56-af67-36b1f7ba31b2" />
5) Now comes one of the very important steps: Calculating the Eigenportfolio Returns. These "Eigenportfolio Returns" will be the factors to our PCA based Model.
   Here is how we can calculate the Eigenportfolio returns.
   <img width="415" alt="image" src="https://github.com/user-attachments/assets/eb8536b3-c71b-44ee-9a77-e082e3a72772" />
   <img width="448" alt="image" src="https://github.com/user-attachments/assets/c21fad05-6f41-417d-a225-52991dfcd7d1" />
6) These returns will be the factors for our model. And will be used as a quantitative approach for the valuation of individual stocks.
7) We perform regression using X as our Eigenportfolio Returns and Y as our Stock Return. And calculate Residual.
8) These residuals now need to be tested on a rolling window and the interesting thing is - These residuals now should follow the OU process. OU process is a mean reverting process, and that is how we will typically make money or thats what the paper says haha. Dont forget we are performing these steps in a rolling window.
9) And now we perform a AR(1) on these residuals. And figure out the Beta(b). Now according to the OU process, if the b < 0. It cannot be considered a OU process. So everytime while calculating if b < 0, then we close our trades if it is open. Because it is no longer a mean-reverting process.
10) Now by estimating the values of the residuals. We will calculate our S-Score.
    <img width="452" alt="image" src="https://github.com/user-attachments/assets/67892da3-45e9-4175-b28e-3b8774c8583f" />
    <img width="296" alt="image" src="https://github.com/user-attachments/assets/8ecc3021-b909-4129-a6c8-5af65426d2ca" />

11) So the signals to buy and sell would be:
    if the s_score <= -1.25 we buy else if the s_score goes above 1.25 we close our position.

Example:
<img width="972" alt="image" src="https://github.com/user-attachments/assets/0a9d4b4b-8bd4-40c5-95d5-d171d5d95042" />







