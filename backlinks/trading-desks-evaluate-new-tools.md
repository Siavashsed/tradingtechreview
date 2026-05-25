# Backlink content - How Professional Trading Desks Actually Evaluate New Tools (And Why Most Vendors Fail the Test)
**URL:** https://siavashsed.github.io/tradingtechreview/trading-desks-evaluate-new-tools/
**Generated:** 2026-05-16

---

## REDDIT
**Post to:** r/algotrading, r/Trading, r/QuantitativeFinance
**Title:** Why do 90% of trading tool demos fail in production? (A desk perspective)

Been evaluating trading infrastructure for a while now, and I've noticed vendors show up with these pristine backtest curves that somehow never match reality once you're live. The gap between demo performance and actual execution is wild.

What I've learned: the real evaluation happens after you ask the uncomfortable questions-API stability under market stress, what happens when their support team stops being responsive, whether documentation actually exists beyond "contact sales."

I wrote down the framework our desk actually uses to cut through the BS, because honestly, most vendors aren't prepared for traders who've already lost money. They expect you to trust the equity curve. We don't.

Full breakdown here: https://siavashsed.github.io/tradingtechreview/trading-desks-evaluate-new-tools/

---

## LINKEDIN
**Hook:** Most trading tool vendors fail the test before the demo even starts.

I've sat through forty+ tool pitches over the years, and the pattern never changes: flawless backtests on clean data, promises of responsive support, and documentation that vanishes after contract signing.

The problem isn't the tools themselves-it's that vendors aren't built for how actual trading desks make decisions. We're not evaluating based on theoretical returns. We're stress-testing for production failure modes.

There's a specific framework that separates tools that actually work from the ones that look good in presentations. It starts with asking the questions vendors don't want to answer: What breaks under market stress? How responsive is support when there's no sale pending? Does the API documentation actually exist?

The vendors who pass this test are rare. But they're identifiable.

Read the full analysis → https://siavashsed.github.io/tradingtechreview/trading-desks-evaluate-new-tools/

#trading #fintech #algotrading #tradingtechnology #softwareengineering

---

## QUORA
**Answer this question:** How do professional trading desks evaluate whether to adopt a new trading tool or platform?

From my experience sitting on both sides of these evaluations-as a software engineer building trading systems and later as a trader actually using them-the process is almost nothing like what vendors expect.

Most tool evaluations start with a vendor presentation featuring backtests that look suspiciously perfect. That's actually your first data point: if the equity curve looks like it was drawn by someone who's never experienced a drawdown, you're already skeptical.

Here's what actually matters to a professional desk:

**Production resilience over demo performance.** How does the tool behave under market stress? What happens when your network hiccups? Does the API remain stable during 10x normal volume? Vendors rarely have answers here because they've never had to.

**Support quality after the contract.** This is the tell. If support is incredibly responsive during evaluation but gets slower post-signature, you've learned everything you need to know about their priorities.

**Documentation and API design.** Not the flashy getting-started guide-the actual reference documentation. Can your engineers integrate this without constantly reaching out? Or are you paying for support tickets just to understand basic functionality?

**Historical performance on *your* data.** Not their clean dataset. Your actual tick data, your actual market conditions, your edge.

I've documented the full framework our desk uses to cut through vendor pitches here: https://siavashsed.github.io/tradingtechreview/trading-desks-evaluate-new-tools/. It covers the specific red flags and the questions that actually separate viable tools from expensive mistakes.
