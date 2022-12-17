# Crypto-Long-Only-Momentum-Strategy
In this notebook, we will create and backtest a long-only momentum strategy using a basket of 10 cryptocurrencies.

# 1. Universe Selection 
We have defined a static list of 10 cryptocurrencies which will form the universe for this strategy (the selection criteria for the universe can be based on the market cap and the daily volume traded). The selected cryptocurrecnies are: Bitcoin, Ripple, EOS, Stellar Lumens, Litecoins, Ethereum, Dash, Monero, Neo, and Ethereum Cash.

# 2. Alpha Generation 
We have used the following parameters to assign a score to each of the cryptocurrencies.

2.1. 2-day returns
2.2. 7-day standard deviation
2.3. 14-day relative strength index

In this step, the 2-day returns, the 7-day standard deviation and 14-day RSI is computed and are ranked as below

1. The higher 2-day returns is given a higher rank assuming that the returns momentum will continue

2. The lower 7-day standard deviation is given a higher rank assuming that relatively less volatile cryptos are preferred

3. The higher 14-day RSI is given a higher rank assuming that the trend will persist

Using the rank function, the cryptos are ranked in the ascending order. Since the 2-day returns of the ETH is lowest it is ranked "1" and the 2-day returns of the XRP is highest it is ranked "10".

The individual ranks obtained from each of the parameters is added to get a combined score. This combined score is again ranked in ascending order to generate a score/rank which will be used in the portfolio construction step.

Another approach would have been to take a weighted average of the ranks. The weight could be based on historic predictive power of that alpha component. For example, for the past 100 days, if RSI predicted better than 2-days returns than RSI can be assigned more weight than the 2-days returns.

# 3. Portfolio Construction
Based on the combined score ranks, we will go long on top 5 cryptocurrencies with the highest score. We will allocate an equal amount of capital to all. We have arbitrarily selected 5 as it was 50% of the universe.

As seen from the dataframe, on 2018-10-12, we will go long on BTC, XRP, EOS, LTC and XMR.

### Note: Number of positions
On certain days, the combined_ranks is same for some cryptocurrencies and therefore we will not be uniquely able to determine the top 5 cryptocurrencies. Thus, on those days we may have positions in 3, 4, or 6 cryptocurrencies instead of 5 as we have taken positions into all the cryptocurrencies with rank greater than or equal to 6.

# 4. Strategy Returns
The strategy returns are computed by multiplying the signal with the daily percentage change. The signal is shifted by 1 day to avoid look-ahead bias.

The strategy returns are computed for all the cryptos and stored in daily_ret.

# 5. Sharpe Ratio
The strategy has a Sharpe ratio of 1.76. If you have an account with an exchange that allows you to short cryptos then you can modify the strategy to short the bottom 50% of the universe. This long-short strategy is expected to be more stable compared to the long-only strategy.
