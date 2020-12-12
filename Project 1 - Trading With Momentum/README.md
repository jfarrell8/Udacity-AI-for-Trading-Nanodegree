## Project 1: Trading With Momentum

The projects aims to generate a trading signal based on a momentum indicator. In general, I computed the signal for the time range given and applied it to the dataset to produce projected returns. I ultimately performed a statistical test on the mean of the returns to conclude if there is alpha in the signal.

In general, I followed the steps below in this analysis:

1. Resample daily close prices to monthly close prices
2. Compute log returns (primary momentum indicator)
3. Shift returns to get previous month and lookahead returns
4. Generate a trading signal: Produce a long/short portfolio of stocks on each trading date. For each month-end observation period, rank the stocks by previous returns, from the highest to lowerst. Select the top performing stocks for the long portfolio, and the bottom performing stocks for the short portfolio.
5. Check if the signal has potential to be profitable: compute net returns.
6. Run a t-test on sample of portfolio returns to test against a null hypothesis of the actual mean return from the signal being zero.

