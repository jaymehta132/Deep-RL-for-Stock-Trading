# FinSearch_2023

This is a repo for the FinSearch project by my team. I have made two RL models using PPO and DQN to simulate stock trading. The PPO model is the main model and the DQN model was made just to compare results. I will first explain PPO model and then the DQN in brief.

I have made a custom environment from scratch which has a 13 feature state-space and Discrete(101) action type.

The state-space of the environment consists of the Closing price of the stock on the previous 9 days, Opening price of the stock of the current day, current cash balance, number of shares held and the volatility in the last 9 days. We have defined volatility as average of (High - Low) on the previous 9 days. 

The action space is a discrete(101) type where an action > 50 means buying the stock and an action < 50 means selling the stock. For an action a, we buy (a-50) stocks if a > 50 and sell (50-a) stocks if a < 50. a = 50 means no buying or selling of stocks. 

We have defined the reward as the change in net worth from previous day after closing and the current day after closing. That is reward = Today's net-worth after closing - Yesterday's net-worth after closing. Net-worth os defined as the cash balance + number of shares held*current price

The above model is a pretty simple one and trades only once during a day. We have assumed the trades to happen at the Opening Price of the stock. 

The training data is Nifty 50 stock data from 4th Jan 2010 to 28th June 2019 and the test data is 1st July 2019 to 29th June 2021. 

The algorithm used is Proximal Policy Optimisation and number of training steps are 3M. Before starting the training, we have used Optuna for tuning the hyper-parameters. 

The results were as follows

Training period:- 10L starting balance to 24L final balance

Testing period:- 10L starting balance to 16L final balance

DQN Model:-

The environment is same for this model, just the RL model has changed. The model was trained for 3M timesteps. For DQN, the results were as follows:-

Training period:- 10L starting balance to 22L final balance

Testing period:- 10L starting balance to 14.5L final balance

The DQN model seems to be very underfitting as it is doing only one action for a lot days and hence requires more training. But due to lack of time and computation power, we didn't train this model for more timesteps.

At first the results might seem very mediocre but if we take into account the time constraints coupled with the extreme volatility due to Covid-19 in the test data, the results seem pretty good.
