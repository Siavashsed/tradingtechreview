# Backlink content - PFOF Under Fire: How the 2021 Payment for Order Flow Debate Changed Algo Trading Forever
**URL:** https://siavashsed.github.io/tradingtechreview/pfof-2021-algo-trading-execution-debate/
**Generated:** 2026-05-28

---

## REDDIT
**Post to:** r/algotrading, r/investing, r/stocks
**Title:** Did anyone else notice their fills getting worse right before the GME squeeze? Here's what I think happened.

I've been backtesting momentum strategies since 2019, and January 2021 was the first time I watched my own execution quality tank across multiple tickers on the same day. Three separate fills came back 4+ cents worse than expected within minutes of each other. At the time I chalked it up to volatility, but I've been digging into the mechanics of how retail orders actually get routed.

Turns out the GameStop situation didn't just expose market structure issues—it exposed how little visibility we actually have into order flow. If you're running algos through any retail broker, your orders are likely being sold to market makers before they hit an exchange. That's not conspiracy thinking, it's literally the PFOF business model.

The 2021 debate around this changed a lot, but most retail traders never connected the dots. Worth understanding how your execution actually works.

Full breakdown here: https://siavashsed.github.io/tradingtechreview/pfof-2021-algo-trading-execution-debate/

---

## LINKEDIN
**Hook:** Retail traders paid $4+ per share in hidden execution costs during 2021. Most still don't know why.

The GameStop squeeze wasn't just a meme stock moment—it was a structural revelation. When retail order flow peaked in January 2021, execution quality collapsed for thousands of algorithmic traders running momentum strategies.

The reason? Payment for Order Flow (PFOF) created a perverse incentive where market makers profited most when retail traders were most confident. Your broker gets paid to route your order to a specific venue, and that venue isn't chosen because it's best for you.

The 2021 debate forced regulators and brokers to finally acknowledge this openly. Some firms eliminated PFOF entirely. Others doubled down. For algo traders, it meant rethinking execution strategy completely—routing preferences became as important as signal quality.

If you're still not sure how your fills actually get processed, this matters more than your entry model.

Read the full analysis → https://siavashsed.github.io/tradingtechreview/pfof-2021-algo-trading-execution-debate/

#algotrading #marketmicrostructure #trading #fintech #execution

---

## QUORA
**Answer this question:** How did Payment for Order Flow (PFOF) affect retail traders during the 2021 market volatility?

The 2021 GameStop squeeze exposed PFOF mechanics that most retail traders had never seriously considered. I experienced it firsthand—momentum algorithms that worked consistently suddenly produced fills that were 4+ cents worse than expected, and it happened to multiple positions simultaneously.

Here's what was actually happening: When retail order flow spiked (everyone trying to buy the same momentum stocks), the market makers who pay for that order flow had maximum information advantage. They knew retail demand was concentrated in specific names, so they widened spreads and delayed execution precisely when retail traders most needed good fills.

The PFOF model creates a misalignment of incentives. Your broker makes money when your order goes to their highest-paying market maker, not necessarily when you get the best execution. During volatile periods, those incentives diverge dramatically.

What changed in 2021 was transparency. The debate forced firms to disclose execution quality metrics publicly. Some brokers eliminated PFOF entirely. For algo traders, it meant we finally had to engineer around this structural headwind rather than pretend it didn't exist.

I wrote a detailed breakdown of how this actually shifted algorithmic trading execution strategies and what to watch for now: https://siavashsed.github.io/tradingtechreview/pfof-2021-algo-trading-execution-debate/ - worth reviewing if you're running momentum or latency-sensitive algos.
