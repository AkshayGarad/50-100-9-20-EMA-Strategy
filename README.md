# 50-100-9-20-EMA-Strategy

This is a simple trading strategy implemented in Pine Script for TradingView. It is based on the Exponential Moving Average (EMA) crossover concept, where a shorter EMA crosses over a longer EMA, indicating a potential buying opportunity, and vice versa for selling opportunities.

## Strategy Overview

### Strategy Script
```pinescript
//@version=4
strategy("EMA Crossover Strategy", shorttitle="EMA Cross", overlay=true)

// Input parameters
emaLengthShort = input(50, title="Short EMA Length")
emaLengthLong = input(100, title="Long EMA Length")

// Calculate EMAs
emaShort = ema(close, emaLengthShort)
emaLong = ema(close, emaLengthLong)

// Plot EMAs on the chart
plot(emaShort, color=color.blue, title="Short EMA")
plot(emaLong, color=color.red, title="Long EMA")

// Create strategy conditions
emaCrossOver = crossover(emaShort, emaLong)
emaCrossUnder = crossunder(emaShort, emaLong)

// Buy and exit conditions
strategy.entry("Buy", strategy.long, when=emaCrossOver)
strategy.close("Buy", when=emaCrossUnder)

// New exit condition: 9-period EMA crosses under 13-period EMA
ema9 = ema(close, 9)
ema13 = ema(close, 13)
emaCrossUnder9_13 = crossunder(ema9, ema13)

strategy.close("Buy", when=emaCrossUnder9_13)
```

### Description

This script implements an EMA crossover strategy on the TradingView platform. It uses two Exponential Moving Averages (EMAs) with user-defined lengths (short and long) to generate buy and sell signals. Here's how it works:

- The short EMA (blue line) and long EMA (red line) are plotted on the chart.
- A "Buy" signal is generated when the short EMA crosses above the long EMA (emaCrossOver).
- A "Buy" trade is entered when the "Buy" condition is met.
- A "Buy" trade is exited when the short EMA crosses below the long EMA (emaCrossUnder).

Additionally, the strategy includes a new exit condition:

- A "Buy" trade is also exited when a 9-period EMA crosses below a 13-period EMA (emaCrossUnder9_13).

## How to Use

1. Add the script to TradingView's Pine Script editor.
2. Customize the lengths of the short and long EMAs using the input parameters.
3. Apply the strategy to your trading chart.
4. Monitor the chart for buy and sell signals based on EMA crossovers.
5. Use proper risk management and stop-loss orders when trading with this strategy.

Please note that this is a simple example, and trading involves risks. Make sure to backtest the strategy and consider additional risk management measures before trading with real funds.

**Disclaimer:** This script is for educational purposes only and should not be considered financial advice. Trading carries a risk of capital loss, and you should trade responsibly.
