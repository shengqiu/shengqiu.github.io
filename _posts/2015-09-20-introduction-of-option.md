---
layout: post
title:  "Introduction of Option "
date:   2015-09-20 08:29:35
categories: RMFE
---

# Kinds of Option

- call option   `right to buy in the future`   `看涨`
- put option   `right t o sell in the future`   `看跌`
- maturity date   `date in the option contract`
- strick price   `price in the option contract`
- American option   `allow exercise at any time before the maturity data`
- European option   `only allow exercise maturity date`

# Call option
The contract to buy the stock in the future

- The seller of the call is said to have shorted the call option
- The buy of the call is said to have longed the call option

![call_option_1](/images/call_option_1.png)

- left hand side of `strike price` is called in the price
- at `strike price` is call at the price
- right hand sdie of `strike price` is called out of the price

# put option
The right to sell the stock in the future

- The seller of the call is said to have shorted the call option
- The buy of the call is said to have longed the call option

![put_option_1](/images/put_option_1.png)

# American Option
In the market, most of the options are American Option

# Positions in Option Contracts
### long put `buy stock in the future`

Invester of a contract that allows buying a stock at $K$ in the future.

![long_put_1](/images/long_put_1.png)


- For $$S_T > K$$, the invester in the long put position will exercise, 
- he can buy the stock from the writer using the option at a lower price of $$K$$, and sell to the market at a higher price at $$S_T$$
- For $$S_T \leq K$$, he will not exerice. So nothing happens.
- The profit is $$max (S_T - K, 0)$$


### short put `sell stock in the future`

Writer of a contract that allows buying stock at $$K$$ in the future.

![short_put_1](/images/short_put_1.png)

- For $$S_T > K$$, since the invester will exercise, the writer has to buy from the market at the higher price &S_T&, and sell it to the invester at the lower price $$K$$.
- For $$S_T \leq K$$, nothing happens.
- the profit of the writer is $$min(K--S_T,0)$$

### long call `sell stock in the future`

Invester of a contract that allows selling stock at $K$ in the future.

![long_call_1](/images/long_call_1.png)

- For $$K_T < K$$, the invester will exercise.
- He will buy the stock from the market at a lower price $$S_T$$, and sell the stock to the writer at the higher price $$K$$
- For $$K_T \geq K$$, he will not exercise
- So the invester's profit is $$max(K-S_T,0)$$

### short call `buy stock in the future`

Writer of a contract that allows selling stock at $K$ in the future

![short_call_1](/images/short_call_1.png)

- For $$K_T < K$$, the invester will exercise.
- So, the writer has to buy the stock at higher price $$K$$ from the invster, and sell it at a lower price $$S_T$$ to the market.
- For $$K_T \geq K$$, he will not exercise
- So the invester's profit is $$min(S_T-K,0)$$

# Underlying Asset

### Stock option

Since stock are traded with a minimun unit of 100 shares, so normally, the underlying asset of an option contract is 100 shares of stock. Some biggest option exchange market are 

- `CBOE` :Chicago Board of Option Exchange, largest U.S. options exchange 
- `NYSE Euronext`: including the New York Stock Exchange, Euronext and NYSE Arca
- `ISEO Options`: focus on innovation, technology and competition create better, more efficient markets for investors
- `Boston Options`: 

### Foreign Currency Options

Mostly the underlying asset is 10K of foreign currency. Mostly OTC, some in exchange:
- `NSADAQ OMX`: a lot of American Options
- `Philadelphia Stock Exchange,PHLX`, many European Options

### Index Optiosn

The method of delievery is the difference of the spot price and strick price in cahs. All in `CBOE`, mostly european options:
- `SPX`: S&P 500 index. \==this is american\==
- `NDX`: the Nasdaq 100 index
- `DJX`: Dow Jones Industrial Index

### Future Options

Mostly American, and it is normally writter in a very short time interval before delievery.  And they are normally delievered in cash.

