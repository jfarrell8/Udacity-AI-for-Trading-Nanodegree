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

