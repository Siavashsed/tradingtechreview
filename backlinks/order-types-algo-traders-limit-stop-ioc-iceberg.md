# Backlink content - Your Stop Order Is a Market Order in Disguise
**URL:** https://siavashsed.github.io/tradingtechreview/order-types-algo-traders-limit-stop-ioc-iceberg/
**Generated:** 2026-11-23

---

## REDDIT
**Post to:** r/algotrading, r/Daytrading, r/quant
**Title:** Anyone else realize a stop order is just a market order waiting to happen? What failure mode do you design around?

I've been going back through my fills from a bad morning in March 2023, when a plain stop on 4,000 shares of a thin small cap triggered and filled way past where I thought I'd be protected. The stop price felt like a promise. It wasn't. Once it triggers, it's a market order, and in a thin book it will walk the book until it's done.

That got me thinking about order types differently. Instead of asking which one is best, I started asking which failure I can afford:

- Limit: might not fill at all
- Stop: might fill at a terrible price
- IOC: might only partially fill
- Iceberg: might leak your intent through the repeated refills

Once you pick the failure you can live with, the code around it gets much simpler. For example, if a limit that doesn't fill is acceptable, you can build retry and repricing logic. If a partial fill is fine, you size your logic to handle remainders explicitly.

Curious how others handle this. Do you use stop-limits, or do you manage exits in code with marketable limits and a price collar? And has anyone measured how much iceberg refills actually leak in practice?

Full breakdown here: https://siavashsed.github.io/tradingtechreview/order-types-algo-traders-limit-stop-ioc-iceberg/

---

## LINKEDIN
**Hook:** A stop order isn't protection. It's a market order that hasn't fired yet.

In March 2023, a plain stop on 4,000 shares of a thin small cap cost me far more than I had budgeted for. The stop price felt like a guarantee. It was only a trigger.

That morning changed how I think about order types in algorithmic trading. The question isn't which order type is best. It's which failure mode you can afford.

A limit order can fail to fill. A stop can fill at a terrible price. An IOC can fill only partially. An iceberg can leak your intent to the market.

Every one of them fails somehow. The engineering job is to pick the failure you can live with, then write the code around it: retries for unfilled limits, price collars for exits, explicit remainder handling for partial fills.

If you build execution logic, I'd be curious which failure mode you've designed around, and why.

Read the full analysis → https://siavashsed.github.io/tradingtechreview/order-types-algo-traders-limit-stop-ioc-iceberg/

#AlgorithmicTrading #TradingTechnology #OrderExecution #QuantTrading #FinTech

---

## QUORA
**Answer this question:** What order types should an algorithmic trader use: limit, stop, IOC, or iceberg?

There's no single best order type. The more useful question is which failure mode you can afford, because every order type has one.

A limit order gives you price control, but it can fail to fill. If the market moves away, you're left watching. That's fine for entries where missing the trade costs little, and you can add repricing logic to chase carefully.

A stop order is the one most people misunderstand. Once the stop price is hit, it becomes a market order. In a liquid name that's usually fine. In a thin book it can fill far from your stop price, because it takes whatever liquidity is available. I learned this the hard way in March 2023, when a plain stop on 4,000 shares of a thin small cap filled much worse than I'd planned for. If you need exits in illiquid stocks, consider a stop-limit, or better, manage the exit in code with a marketable limit and a price collar so you define the worst price you'll accept.

An IOC (immediate or cancel) order fills what it can right now and cancels the rest. The failure mode is a partial fill, so your code has to handle remainders explicitly instead of assuming all or nothing. It's great for taking liquidity without leaving a resting order.

An iceberg shows only a slice of your total size. It reduces visible footprint, but repeated refills at the same price can reveal that a large order is hiding there, so smart counterparties can detect it. Randomizing slice sizes helps somewhat.

My practical rule: decide the failure you can live with first, then write the order logic around it. Don't pick the order type and hope.

I wrote a longer breakdown with the code patterns here if you want more detail: https://siavashsed.github.io/tradingtechreview/order-types-algo-traders-limit-stop-ioc-iceberg/
