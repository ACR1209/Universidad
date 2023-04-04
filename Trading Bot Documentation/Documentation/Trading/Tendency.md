
_BASED ON: https://medium.com/@chris_42047/determining-bull-bear-market-trends-programmatically-python-e68f1ec18f28_

> One easy way without having to get into complicated trend calculation is to Calculate the Simple Moving Average (SMA) for 50 trading days and the SMA for 200 trading days and then determine when the SMA 50 rises or falls below the SMA 200.

The SMA is calculated by adding the price of an index over a number of time periods and then dividing the sum by the number of time periods. The SMA is basically the average price of the given time period, with equal weighting given to the price of each period.
$$SMA_{current}(n)=\frac{\sum_{j=current-n}^{current} Price_j}{n}$$
Where $n$ is the period of the SMA. Meaning that calculating the SMA 50 and the SMA 200 in python looks like this:

```python
def calculate_smas(df):  
    df['SMA50'] = ta.sma(df["close"], length=50)  
    df['SMA200'] = ta.sma(df["close"], length=200)
    return df
```


Is important to note that using a SMA 50 and a SMA200 if the SMA 50 < SMA 200 then the market is bearish, else its bullish. 

```python
def determine_primary_market(df):  
    df['BEAR'] = np.where(df['SMA50'] < df["SMA200"], df['close'], np.NaN)  
    df['BULL'] = np.where(df['SMA50'] > df["SMA200"], df['close'], np.NaN)
    return df
```

SEE: pandas_ta for more technical analysis implementations.