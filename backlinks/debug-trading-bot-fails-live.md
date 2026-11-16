# Backlink content - Your Trading Bot Aced the Backtest, Then Lost $2,140 in Eleven Days
**URL:** https://siavashsed.github.io/tradingtechreview/debug-trading-bot-fails-live/
**Generated:** 2026-11-16

---

## REDDIT
**Post to:** r/algotrading, r/quant, r/learnalgotrading
**Title:** If your bot works in backtest but fails live, stop re-tuning parameters and diff the events instead

I learned this one the expensive way. When a bot crushes the backtest and then loses money live, the strategy logic is usually fine. The bug is in the gap between what the backtester assumed and what the exchange actually did.

In 2023 I ran a mean-reversion bot on BTC perps. The backtest said 2.1 Sharpe. Live, it lost $2,140 in eleven days. My first move was to re-tune parameters. That was wasted time, because the parameters were never the problem.

What actually worked was boring. I logged every live event (signal, order sent, ack, fill, fee, funding) and lined each one up against what the backtester did at the same timestamp. The first place they diverge is your bug. The usual suspects: fill assumptions (assuming you get the close or the mid), fees and funding modeled too optimistically, latency between signal and order, and partial fills the sim never produced.

How do people here reconcile live against backtest? Do you diff event by event, or just compare daily PnL?

Full breakdown here: https://siavashsed.github.io/tradingtechreview/debug-trading-bot-fails-live/

---

## LINKEDIN
**Hook:** My trading bot showed a 2.1 Sharpe in backtest. Live, it lost $2,140 in eleven days.

The strategy logic was fine. The bug was in the gap between what my backtester assumed and what the exchange actually did.

My first move was the wrong one: re-tuning parameters. If your simulation is wrong about how orders fill, no parameter set will fix it. You are optimizing against a fiction.

What worked was reconciliation. I logged every live event, from signal to order to fill to fee, and lined each one up against the backtest at the same timestamp. The first point where the two diverge is where the bug is.

This goes well beyond trading. Whenever a system works in simulation and fails in production, compare the two event by event before you touch the model.

Read the full analysis → https://siavashsed.github.io/tradingtechreview/debug-trading-bot-fails-live/

#AlgorithmicTrading #QuantitativeFinance #Backtesting #TradingBots #SoftwareEngineering

---

## QUORA
**Answer this question:** Why does my trading bot work in backtesting but lose money in live trading?

Short version: the strategy is rarely the problem. The problem is almost always the gap between what your backtester assumed and what the exchange actually did.

I learned this firsthand. In March 2023 I deployed a mean-reversion bot on BTC perpetuals after a backtest showed a 2.1 Sharpe. It lost $2,140 in eleven days. Like most people, I started by re-tuning parameters. That got me nowhere. If your simulation is wrong about execution, you are optimizing against something that does not exist.

The gap usually hides in one of these places:

1. Fill assumptions. Many backtests assume you fill at the close or the mid. Live, you cross the spread, get partial fills, or miss limit fills entirely, often on the trades that would have won.

2. Costs. Fees, slippage and, on perpetuals, funding. A mean-reversion strategy with a thin edge per trade can be wiped out by costs the backtest treated as too small.

3. Latency. Time passes between the signal and the order reaching the book. In fast markets, the price you saw is not the price you get.

4. Data. Bars built from a different feed than the one you trade on, or look-ahead bias, where the backtest used information that was not available at decision time.

The fix is reconciliation, not tuning. Log every live event: signal, order sent, acknowledgment, fill price, fee, funding. Replay the same period in your backtester and line the two up event by event. The first point where they diverge is your bug. Fix the simulator there, re-run it, and only then judge whether the strategy has an edge.

I wrote up the full debugging process here if you want more detail: https://siavashsed.github.io/tradingtechreview/debug-trading-bot-fails-live/
