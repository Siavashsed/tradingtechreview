# Backlink content - The T+1 Switch Broke My Settlement Code Before Breakfast
**URL:** https://siavashsed.github.io/tradingtechreview/t-plus-one-settlement-algo-traders-2024/
**Generated:** 2026-11-15

---

## REDDIT
**Post to:** r/algotrading, r/Daytrading, r/Trading
**Title:** PSA: if your bot computes settlement dates itself, check it for a hardcoded T+2

Posting this because I suspect a few of you have the same landmine in your code.

I run a small mean-reversion strategy in a cash account. I also have a reconciliation script that compares my expected settled cash against what the broker reports. On the morning of May 29 it flagged a $14,200 mismatch. It took me longer than I'd like to admit to find the cause: a helper I wrote in 2021 that calculated settlement date as trade date plus two business days. Hardcoded, and never touched since.

The fun part is that May 29 was a double settlement day. Memorial Day pushed Friday's trades, which were still T+2, to Wednesday. Tuesday's trades, the first day of T+1, also settled on Wednesday. So my projected settled cash was off by a whole session of sells.

If you track unsettled funds to avoid good faith violations, or size positions off settled cash, check how you get your settlement dates. Pull them from the broker if you can, and use a real exchange holiday calendar.

Full breakdown here: https://siavashsed.github.io/tradingtechreview/t-plus-one-settlement-algo-traders-2024/

---

## LINKEDIN
**Hook:** One hardcoded line from 2021 triggered a $14,200 reconciliation mismatch the morning after T+1 went live.

On May 28, 2024, US equities moved from T+2 to T+1 settlement. Most investors never noticed. For anyone running automated strategies in a cash account, it quietly changed the cash math.

My reconciliation script caught it at 6:40 the next morning. A settlement helper I wrote years ago assumed trade date plus two business days. It had never been wrong, so I had never looked at it again.

The timing made it worse. Because of Memorial Day, Friday's T+2 trades and Tuesday's first T+1 trades both settled on Wednesday, May 29. My projected settled cash was short a full session.

The lesson goes beyond settlement. Any market convention you store as a constant depends on a regulator never changing it. Get it from the broker or a maintained calendar, and reconcile daily so drift shows up fast.

Read the full analysis → https://siavashsed.github.io/tradingtechreview/t-plus-one-settlement-algo-traders-2024/

#AlgorithmicTrading #T1Settlement #FinTech #QuantTrading #SoftwareEngineering

---

## QUORA
**Answer this question:** How did the switch to T+1 settlement affect algorithmic traders who use cash accounts?

I run a small mean-reversion strategy in a cash account, so this one hit me directly. Short version: T+1 is mostly good news for retail algo traders, but it breaks any code that still assumes T+2 timing.

What changed: since May 28, 2024, most US equity trades settle one business day after the trade instead of two. In a cash account you can't freely reuse sale proceeds until they settle. That means settlement timing feeds straight into how much buying power your strategy really has.

The upside: sale proceeds turn into settled cash a day sooner. If your strategy rotates capital often, you get more usable cash and fewer chances of a good faith violation. That violation happens when you buy with unsettled proceeds and then sell the new position before those proceeds settle.

The risk is hardcoded assumptions. My reconciliation script flagged a $14,200 mismatch the morning after the switch. The cause was a helper I wrote in 2021 that calculated settlement as trade date plus two business days. The transition week made it obvious. Memorial Day pushed Friday's T+2 trades to Wednesday, the same day Tuesday's first T+1 trades settled. My projected cash was a full session behind reality.

If you trade algorithmically, check these:
- Anywhere you calculate settlement dates yourself. Use the broker's reported settlement date if you can.
- Your holiday calendar. Business-day math that ignores exchange holidays will drift.
- Position sizing that depends on settled cash versus total cash.
- Daily reconciliation between your model and the broker. It's the only reason I caught this before it caused a violation.

I wrote up the full incident and the fix here if you want the details: https://siavashsed.github.io/tradingtechreview/t-plus-one-settlement-algo-traders-2024/

Margin accounts are less exposed, but the same assumptions can still hide in reporting and P&L code.
