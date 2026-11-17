# Backlink content - Your Python Position Sizing Engine Should Treat Kelly as a Ceiling
**URL:** https://siavashsed.github.io/tradingtechreview/python-kelly-volatility-position-sizing/
**Generated:** 2026-11-17

---

## REDDIT
**Post to:** r/algotrading, r/quant, r/FuturesTrading
**Title:** 140 trades isn't enough to trust your Kelly fraction. How do you size around edge uncertainty?

I wrote a full-Kelly position sizer over a weekend and it told me to put 38% of a $62k account into a single NQ mean-reversion setup. The edge estimate behind that number came from 140 trades. You can guess how the next two weeks went.

Kelly's math wasn't the problem. The input was. With 140 trades and a 55% win rate, the standard error on that win rate is about 4 points, so the true number could plausibly sit anywhere from 47% to 63%. Kelly takes the optimistic end of that noise and turns it into leverage.

What I run now: volatility targeting sets the size (target annual vol divided by the instrument's realized vol, scaled to contract value). Kelly, computed on a shrunk edge estimate and then halved, acts only as a hard ceiling. The sizer takes the minimum of the two. Vol targeting responds to what the market is doing today, and Kelly only gets a vote when the vol target would overreach.

How do others here handle edge uncertainty in sizing? Do you shrink the estimate, use fractional Kelly, or skip Kelly entirely?

Full breakdown here: https://siavashsed.github.io/tradingtechreview/python-kelly-volatility-position-sizing/

---

## LINKEDIN
**Hook:** A position sizer I wrote over a weekend told me to risk 38% of my account on one trade.

The math was correct. The input was the problem. My edge estimate on that NQ mean-reversion setup came from 140 trades, which is nowhere near enough to pin a win rate down to within a few percentage points.

The Kelly criterion assumes you know your edge. In live trading you never do, and Kelly turns estimation error directly into leverage. Overestimate your edge slightly and you get sized far past the point where the strategy can survive a normal losing streak.

The fix I now build into every sizing engine: volatility targeting decides the position, and Kelly only sets a ceiling it can never break. Vol targeting adapts to current market conditions without leaning on a fragile edge estimate.

Engineers will recognize the pattern. Never let your least reliable input drive the output.

Read the full analysis → https://siavashsed.github.io/tradingtechreview/python-kelly-volatility-position-sizing/

#AlgorithmicTrading #QuantitativeFinance #Python #RiskManagement #Trading

---

## QUORA
**Answer this question:** Should I use the Kelly criterion to size positions in my algorithmic trading system?

Use it, but not as your sizing rule. Use it as a cap.

Kelly gives you the bet size that maximizes long-run growth, but only if you know your edge exactly. That condition is what breaks it in practice. Your edge is an estimate from a backtest or a limited live sample, and Kelly is very sensitive to that estimate. Overstate the edge and Kelly oversizes you. Bet at double the true Kelly fraction and your expected growth drops to roughly zero while your drawdowns get much deeper.

I learned this firsthand. In March 2024 a full-Kelly sizer I had written told me to put 38% of a $62,000 account into a single mean-reversion setup on NQ futures. The edge came from 140 trades. At that sample size, a measured 55% win rate has a standard error of roughly 4 percentage points, so the true rate could reasonably be anywhere from about 47% to 63%. The low end of that range is a losing strategy, and Kelly had no way of knowing that.

What I do now:

1. Size with volatility targeting. Pick a target annualized volatility for the strategy, divide it by the instrument's recent realized volatility, and convert the result to contracts. This depends on something you can measure well (recent vol) instead of something you can't (true edge).

2. Compute Kelly on a shrunk edge estimate, then take a fraction of it, half or less.

3. Take the smaller of the two as your final size. Kelly only matters when the vol target would overreach.

4. Round down to whole contracts. If the cap says zero, trade zero.

This keeps sizing responsive to market conditions and makes sure an overconfident edge estimate can never put you in a position you can't survive.

I wrote up the full Python implementation and the March 2024 post-mortem here: https://siavashsed.github.io/tradingtechreview/python-kelly-volatility-position-sizing/
