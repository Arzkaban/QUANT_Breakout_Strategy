# QUANT_Breakout_Strategy_Review
Udacity Project2 of AI for Trading
Meets Specifications
Congratulations on finishing this project successfully! I hope you have enjoyed this project. In the upcoming project of this nanodegree, you will learn about portfolio optimization techniques with constraints using cvxpy https://www.cvxpy.org/ . So stay tuned :)

Generate Signal
The function get_high_lows_lookback computes the maximum and minimum of the closing prices over a window of days.

A breakout strategy seeks to benefit from the idea that stock prices typically oscillate within a range, so that when they begin to break out of the range, they are likely to continue breaking out. This function computes the range of the stock prices. If the stocks break out of the range then we can trade the stocks.

close = df.reset_index().pivot(index='date', columns='ticker', values='adj_close')
high = df.reset_index().pivot(index='date', columns='ticker', values='adj_high')
low = df.reset_index().pivot(index='date', columns='ticker', values='adj_low')
Check out OHLC lesson https://www.youtube.com/watch?v=FgNY4YgVWFk

Closing price is the end of day stock price.
Open price is the start of the day stocks price.
High price is the highest price of the stock over the entire day.
Low price is the lowest price of the stock over the entire day.

The function get_long_short computes long and short signals using a breakout strategy.

In this function, breakout strategy is actually implemented. When the stock price is out of the window, we can buy/sell the stocks accordingly.

The function filter_signals filters out repeated long or short signals.

Having additional signals to sell/buy the stocks are not helpful therefore we filter out these repeated long or short signals.

The function get_lookahead_prices gets the close price days ahead in time.

Nice work in using .shift to get the lookahead prices.

The function get_return_lookahead generates the log price return between the closing price and the lookahead price.

Raw return is defined as R = (p(t+1) - p(t)) / p(t) , we can change to log return as follows;

R = p(t+1) / p(t) - p(t) / p(t)
R = p(t+1) / p(t) - 1
Taking logs on both sides;

lnR = ln(p(t+1) / p(t)) - ln(1)
lnR = ln(p(t+1) / p(t)) where ln(1) = 0
Further step can be as follows;

lnR = ln(p(t+1)) - ln(p(t)) using logarthmic rule

The function get_signal_return generates the signal returns.

:thumbsup:

Evaluate Signal
Correctly answers the question “What do the histograms tell you about the signal returns?"

It is also worth pointing out that the signal returns distribution can be used to identify any outliers in the distribution. Here's the lesson video that talks about identifying the outliers in the histogram of the signal returns https://www.youtube.com/watch?v=BSLGZz0RzTg

Outliers
The function calculate_kstest calculates the ks and p values.

Nice job in first getting the normal_args (mean and standard deviation) of the entire portfolio and then running the KS test on a normal distribution against each stock's signal returns with normal_args of the entire portfolio.

The function find_outliers returns the list of outlying symbols.

Both conditions to find the outliers are satisfied;

Symbols that pass the null hypothesis with a p-value less than pvalue_threshold.
Symbols that with a KS value above ks_threshold.
