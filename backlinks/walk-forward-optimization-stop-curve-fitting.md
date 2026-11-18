# Backlink content - Walk-Forward Optimization Killed My Best Strategy, and It Was Right
**URL:** https://siavashsed.github.io/tradingtechreview/walk-forward-optimization-stop-curve-fitting/
**Generated:** 2026-11-18

---

## REDDIT
**Post to:** r/algotrading, r/quant, r/FuturesTrading
**Title:** My best backtest had a 2.4 Sharpe. Walk-forward testing showed most of it was luck. How do you size your windows?

Back in March 2022 I ran a grid search over about 2,800 Keltner channel breakout combinations on ES futures. The top parameter set showed a 2.4 Sharpe across 2015 to 2021. I was convinced I had something, and I traded it for eleven weeks before admitting it wasn't what the backtest promised.

What I should have done first was walk-forward optimization. You tune on one window, test on the next window the optimizer never saw, roll forward and repeat. Then you judge only the stitched out-of-sample equity curve.

My "best" set didn't hold up. Out-of-sample performance looked nothing like in-sample. With 2,800 combinations, something was always going to look brilliant by chance.

What I check now:
- Out-of-sample vs in-sample efficiency
- Whether neighboring parameters perform about the same (a plateau, not a lone spike)
- How many individual windows are profitable, not just the total

I'm curious how others here split in-sample and out-of-sample. Do you anchor the start or roll the whole window?

Full breakdown here: https://siavashsed.github.io/tradingtechreview/walk-forward-optimization-stop-curve-fitting/

---

## LINKEDIN
**Hook:** A 2.4 Sharpe backtest can be the most dangerous number in algorithmic trading.

In March 2022 I grid-searched 2,800 Keltner channel breakout combinations on ES futures. The winner showed a 2.4 Sharpe from 2015 through 2021. It looked like the best strategy I had ever built.

It was not. Test 2,800 variations and one of them will look brilliant by chance alone.

Walk-forward optimization exposes this. You tune parameters on one window, trade them on the next window the optimizer never saw, roll forward and repeat. Only the out-of-sample results count. A real edge survives that process. Luck collapses.

The lesson reaches well beyond trading. Any system tuned on historical data has to prove itself on data it has not seen. Otherwise you are only measuring how well you memorized the past.

Read the full analysis → https://siavashsed.github.io/tradingtechreview/walk-forward-optimization-stop-curve-fitting/

#AlgorithmicTrading #QuantitativeFinance #Backtesting #TradingStrategy #DataScience

---

## QUORA
**Answer this question:** How does walk-forward optimization prevent overfitting when backtesting a trading strategy?

Walk-forward optimization stops overfitting by never letting a parameter set be judged on the data it was tuned on.

A normal optimization takes your whole history, tries every parameter combination and reports the best one. The problem is that the more combinations you try, the more likely the winner is fitting noise. I learned this firsthand. In March 2022 I ran a grid search over about 2,800 Keltner channel breakout combinations on ES futures, and the top result showed a 2.4 Sharpe from 2015 through 2021. It looked like a great edge. Live trading over the next eleven weeks said otherwise.

Walk-forward works like this:

1. Split your history into an in-sample window (for example, two years) and an out-of-sample window right after it (for example, six months).
2. Optimize on the in-sample window only.
3. Apply the winning parameters, unchanged, to the out-of-sample window and record the result.
4. Roll both windows forward and repeat until you run out of data.
5. Stitch the out-of-sample segments together. That combined curve is the only performance you should believe.

It works because every period you evaluate is one the optimizer never saw. A strategy that only looked good because of lucky parameter choices won't keep that up window after window.

A few things to watch:

- Walk-forward efficiency: out-of-sample returns divided by in-sample returns. Very low ratios point to curve-fitting.
- Parameter stability: if the best values jump around wildly between windows, there probably isn't a stable edge.
- Consistency: count how many windows are profitable, not just the total.

I wrote up the full process, including how my own strategy failed the test, here: https://siavashsed.github.io/tradingtechreview/walk-forward-optimization-stop-curve-fitting/

The uncomfortable truth is that a strategy failing walk-forward is good news. It is far cheaper to find out in a backtest than in your account.
