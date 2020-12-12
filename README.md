# Udacity-AI-for-Trading-Nanodegree

## Project 1: Trading With Momentum

The projects aims to generate a trading signal based on a momentum indicator. In general, I computed the signal for the time range given and applied it to the dataset to produce projected returns. I ultimately performed a statistical test on the mean of the returns to conclude if there is alpha in the signal.

In general, I followed the steps below in this analysis:

1. Resample daily close prices to monthly close prices
2. Compute log returns (primary momentum indicator)
3. Shift returns to get previous month and lookahead returns
4. Generate a trading signal: Produce a long/short portfolio of stocks on each trading date. For each month-end observation period, rank the stocks by previous returns, from the highest to lowerst. Select the top performing stocks for the long portfolio, and the bottom performing stocks for the short portfolio.
5. Check if the signal has potential to be profitable: compute net returns.
6. Run a t-test on sample of portfolio returns to test against a null hypothesis of the actual mean return from the signal being zero.

## Project 2: Breakout Strategy

Given the following investment hypothesis, generate a breakout strategy.

Hypothesis: In the absence of news or significant investor trading interest, stocks oscillate in a range. Traders seek to capitalize on this range-bound behaviour periodically by selling/shorting at the top of the range and buying/covering at the bottom of the range. This behavior reinforces the existence of the range. When stocks break out of the range, the liquidity traders who have been providing liquidity at the bounds of the range seek to cover their positions to mitigate losses, thus magnifying the move out of the range, and the move out of the range attracts other investor interest; these investors, due the behavioral bias of herding build positions which favor continuation of the trend.

Price highs and lows are the indicator in this breakout strategy. In general, I followed the steps below in this analysis

1. Compute highs and lows in a window
2. Compute long and short signals, assigned signal values per the table below

| Signal | Condition |
|--------|-----------|
|   -1   | Low  > Close Price |
|    1   | High < Close Price |
|    0   |     Otherwise      |

3. Filter signals to eliminate repeated signals
4. Evaluate how many days to short or long the stocks: Get lookahead prices 5, 10, and 20 days in advance
5. Generate log price returns between closing and lookahead prices
6. Compute signal return from price returns
7. Test for significance
8. Find stocks that are outliers in the signal returns using a Kolmogorov-Smirnov Test (applied to teach ticker's signal returns where a long or short signal exits).

## Project 3: Smart Beta and Portfolio Optimization

This project looks at designing portfolios using two methods/hypotheses: 1) dividend-issuing stocks tend to perform better than stocks that do not and 2) design a portfolio that can be made into an ETF by creating a portfolio that tracks an index while minimizing the portfolio variance. Ideally, this portfolio will match the index returns with less volatility to provide a higher risk-adjusted return (Sharpe Ratio). Smart Beta ETFs can be designed with both of these methods.

Part 1. Smart Beta Portfolio: choose portfolio weights using dividend yields
1. Generate market cap weighted index weights from dollar volume
2. Simplified approach using cumulative dividend yield to calculate portfolio weights
3. Generate stock returns
4. Generate weighted returns
5. Calculate cumulative index and ETF returns
6. Calculate tracking error (of ETF against the index): 10%

Part 2. Portfolio Optimization

I want to minimize the portfolio variance while tracking the market cap weight index as closely as possible. I used L2-Norm to minimize distance between the weights of our portfolio and the index per the governing equation below.

![equation](http://www.sciweavers.org/tex2img.php?eq=Minimize%5B%20%20%5Csigma%5E%7B2%7D_%7Bp%7D%20%20%2B%20%20%5Clambda%20%20%5Csqrt%7B%20%5Csum_%7B1%7D%5E%7Bm%7D%28weight_%7Bi%7D%20-%20indexWeight_%7Bi%7D%29%5E%7B2%7D%20%7D%20%20%20%5D%20&bc=White&fc=Black&im=jpg&fs=12&ff=arev&edit=0)

Using a cvxpy optimizer, I was able to generate optimal weights of the stocks for a portfolio that would track the index as best it could while minimizing volatility.

The portfolio initially used the same weights for the entire trade history. Thus, I rebalanced the portfolio every n days to better simulate reality. Finally, to measure the cost of rebalancing, I calculated the annual portfolio turnover.
