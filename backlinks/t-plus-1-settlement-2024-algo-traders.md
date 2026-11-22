# Backlink content - T+1 Went Live in May 2024 and Broke My Settlement Assumptions
**URL:** https://siavashsed.github.io/tradingtechreview/t-plus-1-settlement-2024-algo-traders/
**Generated:** 2026-11-22

---

## REDDIT
**Post to:** r/algotrading, r/Daytrading, r/quant
**Title:** Did T+1 break anyone else's settlement logic? Mine failed the morning after the switch

I've been running a retail algo stack for a few years, and the May 28, 2024 move to T+1 caught me out in a way I didn't expect. Most of the coverage treated it as a back-office change, so I assumed my bot wouldn't care.

On May 29 at 9:40 a.m., it rejected a cash-funded order. I'd sold a position the previous afternoon. In my head (and in my code) that cash was still unsettled, because I had a helper function with a hardcoded two-day settlement lag from years ago. The broker's API already showed the funds as available, so the two views of my account disagreed.

The fix itself was small. The real lesson was that I'd baked a market-structure assumption into a utility function and never documented it. Once I started looking, I found a couple of other places where the old lag was implicitly assumed, including a buying-power estimate and a wash-sale date check.

If you trade cash accounts or size positions off settled funds, it's worth grepping your code for any date arithmetic tied to settlement. Also worth asking whether you should trust the broker's reported settled cash over your own calculation.

Has anyone else found T+1 leftovers in their code months later? Full breakdown here: https://siavashsed.github.io/tradingtechreview/t-plus-1-settlement-2024-algo-traders/

---

## LINKEDIN
**Hook:** One hardcoded number in a helper function cost me a morning of trading after T+1.

When the US moved to T+1 settlement on May 28, 2024, most people filed it under back-office news. I did too.

The next morning, my trading bot rejected a cash-funded order. A position I'd sold the day before looked unsettled to my code but settled to my broker's API. The cause was a two-day settlement lag I had hardcoded years earlier and forgotten about.

The bug was trivial to fix. The lesson wasn't: market-structure rules were living inside my code as unlabeled constants, with no tests and no documentation.

I now treat anything tied to settlement, calendars, or fee schedules as configuration that gets reviewed when the rules change, and I defer to the broker's reported figures instead of recomputing them myself.

If you run automated strategies, when did you last audit your hidden assumptions?

Read the full analysis → https://siavashsed.github.io/tradingtechreview/t-plus-1-settlement-2024-algo-traders/

#AlgorithmicTrading #T1Settlement #TradingTechnology #SoftwareEngineering #QuantFinance

---

## QUORA
**Answer this question:** How did the switch to T+1 settlement affect retail algorithmic traders?

For most retail traders the change was invisible, but if you run automated strategies it can matter more than you'd expect. I'm a software engineer turned full-time algo trader, and it affected my own setup.

The US moved from T+2 to T+1 settlement on May 28, 2024. That means a stock sale settles one business day later instead of two, so the cash becomes available sooner. In theory that's purely good news for anyone trading in a cash account.

The problem is that many retail systems encode the old rule somewhere. In my case it was a helper function with a hardcoded two-day lag. The morning after the switch, my bot refused an order because it believed yesterday's sale hadn't settled, while my broker's API already showed the cash as available. The two systems disagreed about the state of my account.

Here is where I'd look in your own stack:

1. Any date arithmetic involving settlement, especially constants like 2 or 'two business days'.
2. Buying-power or available-cash calculations that you compute yourself rather than reading from the broker.
3. Tax and compliance logic, such as wash-sale windows or good-faith violation checks, that depends on settlement dates.
4. Backtests that assume T+2 cash availability, since they may understate how quickly capital can be recycled.
5. Holiday calendars, because T+1 shifts which business day cash lands on around market closures.

My practical advice is to move these assumptions into named configuration, add tests that fail loudly when they change, and prefer the broker's reported settled cash over your own estimate.

I wrote up what I found and how I fixed it here if you want more detail: https://siavashsed.github.io/tradingtechreview/t-plus-1-settlement-2024-algo-traders/
