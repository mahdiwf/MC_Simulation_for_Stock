# MC_Simulation_for_Stock
Using Monte Carlo Simulation to evaluate upside and downside (risk) potential of a stock

*Apple is now the most valuable US public company* By Krystal Hur, CNN Thu June 13, 2024 <br>
https://edition.cnn.com/2024/06/13/investing/apple-microsoft-market-cap-nvidia/index.html <br>

*Nasdaq, S&P 500 post record closing highs as Apple soars* By Caroline Valetkevitch, June 12, 2024 <br>
https://www.reuters.com/markets/us/futures-fall-markets-await-fed-decision-cpi-data-2024-06-11/ <br>

*Famous Analyst Thinks Apple Inc (NASDAQ:AAPL) is a Better AI Investment Than Nvidia(NVDA) — Here’s Why* By Fahad Saleem, Jun 8, 2024 <br>
https://finance.yahoo.com/news/famous-analyst-thinks-apple-inc-192335822.html <br>

Today is Saturday, June 15th, 2024. After reading the above articles, I am wondering:<br> 
**Should I invest in AAPL? What is the chance of returns of 12% in a year?** <br>
**Is there a potential loss? How much is that?** <br>

This project is for me to learn to answer those questions. I briefly learned Monte Carlo Simulation in my junior Numerical Analysis class.<br>
So, I will use **Monte Carlo Simulation** to:
* Simulate AAPL future prices (portfolio values).
* Risk Analysis (VaR & CVaR Calculation).

Apple stock price for the last 252 trading days.<br>
![image](https://github.com/mahdiwf/MC_Simulation_for_Stock/assets/163992115/28b3c2e1-c9ca-4ec5-8d1e-7598ada75965)

The daily price percentages returns
![image](https://github.com/mahdiwf/MC_Simulation_for_Stock/assets/163992115/8b821e7d-3b02-4d53-9279-4901ae9c90a6)

Using this percentage returns distribution statistical properties (median & standard deviation), I simulated daily returns for the next 252 trading days. Add these simulated daily returns to the last prices (of each calculation), and I get a simulated stock price (a random walk).
![image](https://github.com/mahdiwf/MC_Simulation_for_Stock/assets/163992115/0e92e697-984a-4b9a-bb5f-003c2712577e)

Iterating the above process 10000 times, I got 10000 price paths/random walks.<br>
![image](https://github.com/mahdiwf/MC_Simulation_for_Stock/assets/163992115/efb6a086-176a-42e1-b4df-313d609a3295) <br>
The upside potential is about 300 (500 - 200), and the downside potential is about 80 (200 - 120).

From this simulation, I also calculated the VaR & CVaR.<br>
![image](https://github.com/mahdiwf/MC_Simulation_for_Stock/assets/163992115/af3ae1c5-e870-4a0e-85fe-8a693ddcc45d)

The distribution of simulated portfolio returns and VaR threshold
![image](https://github.com/mahdiwf/MC_Simulation_for_Stock/assets/163992115/afc49e2c-8074-4243-baae-b4704aac1a15)

From the simulation result, I can get the probability of achieving the 12% return.
>desired_return = 0.12  #Desired return (12%)
>num_success = np.sum(sim_port_avg >= initial_investment * (1 + desired_return))
>probability_of_success = num_success / num_simulations
>print(f"Probability of achieving at least a {desired_return*100}% return: {probability_of_success*100:.2f}%")

Probability of achieving at least a 12.0% return: **36.98%**. <br>

Comparing VaR (Historical, Parametric, and Monte Carlo).<br>
![image](https://github.com/mahdiwf/MC_Simulation_for_Stock/assets/163992115/3528bfcd-ef2c-47f3-9640-9c4d5a1f066b)

**Conclusion:**<br>
I think Monte Carlo Simulation is a great tool to analyze a probabilistic view of future stock prices/other events.<br>
  1) The upside potential (reward) is higher than the downside potential (risk)
  2) There is about 37% that AAPL will return more than 12% in a year.
  3) The downside potential (VaR and CVaR) is about 8-20% of the initial investment value depending on the confidence levels.

Since this project is my first time calculating VaR & CVaR, I have yet to learn to make decisions based on these results.
However, I think I will not buy a stock solely based on Monte Carlo Simulation.
