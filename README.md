# S&P500 Data Extrapolation
In this series of notebooks we are going to describe the methodology used for extracting relevant statistics from an S&P500 csv file. These statistics are then used to compare synthetic data generated from a WGAN-GP and an SPDGAN.

# The dataset
### Composition
This dataset is comprised of X stocks for Y observations ranging from xx/xx/xx tp yy/yy/yy. The values represent stock prices and we compute simple returns (however using log returns leads to identical results).
### Missing values
After the above transformation we check how many values are missing and indeed 12% of the whole data is missing. Missing data is not uniformly distributed but happens for 133 stocks, with 2/3rds of them having more than 30% missing values and half of them having more than 50% missing values. We decide to discard all stocks having more than 30% missing values thus ending up with XX stocks.
### Sampling procedure
Our main interest is to sample correlation/covariance matrices from 80 stocks considering a time window of 252 + K days (where K is a small integer, in our case K=4). We uniformly choose 80 stocks without repetition and if each one does not contain missing values. In order to compute the correlation and covariance matrix from this [80, 252+K] subsample of our starting dataset we follow two procedures:
##### Direct sampling
We extract the usual pearson correlation matrix and covariance.
##### Exponentially weighted Riemann mean
We extract K+1 covariance matrices with a moving time window of 252 days. Then we fix the most recent covariance matrix (the k-th one) and interpolate between it and the remaining others along the Riemannian geodesic with an exponentially decaying weight. Afterwards we perform the Riemann mean.
In order to obtain the correlation matrices we convert the covariance matrix dividing by the inverse square root of the diagonal elements.

From now on we analyze the canonically computed correlation matrices.
# The Statistics
### Upper triangular elements
{% include Onion_hist_corr.html %}
