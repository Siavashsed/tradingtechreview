# Backlink content - Your ML Trading Signal Is Probably Overfit, and Here's How I Found Mine
**URL:** https://siavashsed.github.io/tradingtechreview/machine-learning-trading-signals-pitfalls/
**Generated:** 2026-11-26

---

## REDDIT
**Post to:** r/algotrading, r/quant, r/MachineLearning
**Title:** How do you tell a real ML trading signal from a backtest that just memorized the past?

I spent three weeks tuning a gradient-boosted model and got a 2.1 Sharpe in backtest. I put it on a $25,000 paper account and within eleven days it was a flat line. Nothing was broken in the code. The edge simply wasn't there.

Looking back, the warning signs were all in my own process. I'd run so many feature and hyperparameter variations that I was effectively fitting to the test set by hand. My cross-validation folds leaked information because adjacent samples overlapped in time. And I never asked how many trials it took to find the good result, which is the number that tells you how much of the Sharpe is luck.

What helped: purged and embargoed walk-forward splits, counting every experiment I ran and deflating the Sharpe accordingly, and keeping a final holdout I touched exactly once. I also started distrusting any result that was too smooth.

Curious what checks others here rely on before trusting a model with real capital. Do you use deflated Sharpe, combinatorial purged CV, or something simpler? Any tests that have saved you from a bad deploy?

Full breakdown here: https://siavashsed.github.io/tradingtechreview/machine-learning-trading-signals-pitfalls/

---

## LINKEDIN
**Hook:** My machine learning trading model scored a 2.1 Sharpe in backtest and flatlined in eleven days.

In March 2024 I watched a gradient-boosted model I'd tuned for three weeks go flat on a $25,000 paper account. The code was fine. The edge was an illusion.

The cause was my own process. Hundreds of small tweaks to features and hyperparameters meant I was memorizing the past, not learning from it. Time-overlapping samples leaked information across my validation folds, and I never counted how many experiments it took to find a good result.

The fixes were unglamorous. Purged walk-forward validation. A running log of every trial, used to deflate the Sharpe. One untouched holdout, checked once.

The lesson applies well beyond trading: when you search long enough, you will find a pattern. The discipline is in proving it survives data it has never seen.

Read the full analysis → https://siavashsed.github.io/tradingtechreview/machine-learning-trading-signals-pitfalls/

#AlgorithmicTrading #MachineLearning #QuantitativeFinance #Overfitting #DataScience

---

## QUORA
**Answer this question:** Why do machine learning trading strategies that look great in backtests fail in live trading?

Short answer: most of them were never real edges. They were the result of searching until something looked good.

I'm a software engineer turned full-time algo trader, and I learned this the hard way. In March 2024 I had a gradient-boosted model with a 2.1 Sharpe in backtest after three weeks of tuning. On a $25,000 paper account it went flat in eleven days.

Here are the main reasons this happens:

1. Multiple testing. Every feature you add and every hyperparameter you tweak is another trial. Run enough of them and one will look excellent by chance. If you don't track how many you ran, you can't know how much of your Sharpe is luck.

2. Data leakage. Standard k-fold cross-validation assumes samples are independent. Financial data isn't. Labels that span several days overlap with neighbouring folds, so the model effectively sees the answer. Purging and embargoing around each split fixes much of this.

3. Low signal-to-noise. Markets are mostly noise, and flexible models like boosted trees or neural nets are very good at fitting noise.

4. Ignoring costs and regime change. Slippage, fees and a shift in market behaviour can erase a thin edge that looked solid historically.

What I do now: walk-forward validation with purging, a log of every experiment so I can deflate the Sharpe, a holdout set I look at exactly once, and a strong suspicion of any equity curve that looks too clean. I also start with simpler models and only add complexity if it clearly earns its place out of sample.

I wrote up the full story and the checklist I use here, if it's useful as additional reading: https://siavashsed.github.io/tradingtechreview/machine-learning-trading-signals-pitfalls/

The core idea is simple: a backtest is a hypothesis, not evidence. Live or paper trading on unseen data is the real test.
