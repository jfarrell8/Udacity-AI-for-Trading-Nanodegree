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

