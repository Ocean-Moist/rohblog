+++
title = "O(n) vs. O(n^2) Startups"
date = "2025-05-14"
+++

I recently saw a tweet[1] about how people should go about starting startups/businesses, and it caused me to formalize my intuitions around two distinct types of tech businesses I am familiar with. I'll call them $O(n)$ startups and $O(n^{2})$ startups.

Throughout this essay, let _n_ represent the time elapsed since launch. An **$O(n)$** startup grows its key metric (revenue, users, etc.) roughly linearly with time—double the time, double the metric. An **$O(n^{2})$** startup accelerates, with growth compounding super-linearly over time.

Here are a few popular examples:
-   **$O(n)$:** Mailchimp, 37signals -> steady ARR, high margins, no outside capital.  
-   **$O(n^{2})$:** Slack (pre-acq), Uber -> heavy spend, but every user fuels ecosystem/network effects.

## what do i mean?

Businesses generally grow following a few patterns. They generally have some TAM to saturate and saturate the TAM at some rate. This rate can be *vaguely* linear, what I call $O(n)$, or *vaguely* superlinear, what I call $O(n^{2})$.

The reason I borrow the [asymptotic notation](https://en.wikipedia.org/wiki/Big_O_notation) is because it implies the growth rate is *an upper bound* (best case scenario) and generalizes away specific constant factors and sums. The analogy breaks down when you force $n$ or $n^{2}$ imply something numerically specific about your growth rate, or introduce functions with different growth rates like logs or exponentials. For now we will (somewhat unprincipledly) stick with two sole classes: $O(n)$ and $O(n^{2})$.[2]

I think businesses aim to improve their growth rate via constant factors (eg $O(n^{2})$ -> $O(2*n^{2})$)[3] but fundamentally can't change them. Some businesses are doomed to grow linearly (lifestyle businesses) and some are able to grow superlinearly.

## implications

VCs generally only invest in $O(n^{2})$ companies. While $O(n)$ businesses are far more common. $O(n)$ businesses can't be fund returners.

Notice how this growth rate is *an upper bound* and ignores intercepts? This essentially means a company could underperform their growth rate in some cases and that an $O(n)$ company could be valued higher than an $O(n^{2})$ company at some non-asymptotic time.

## differences (people)

The $O(n)$ companies I am familiar with are generally 100% bootstrapped, B2B SaaS or tech adjacent, and have between 10–50m in revenue. The $O(n^{2})$ companies I am familiar with are pre series B consumer/B2B SaaS.

The way these two companies operate are completely different from day 1. I think one of the biggest ways is talent/people.

$O(n)$ companies can't afford to hire the absolute best talent. At the top, the founder(s) are generally very smart, but they don't have the budget for the best growth/product people. They hire and value sales people to butter up their clients who are generally execs at super big publicly traded companies. They hire people who fit a job description.

$O(n^{2})$ companies hire high agency people. People who can just go in under constrained environments. People are generally given a lot of equity to join and as a reward.

## differences (economics)

Another difference is the economics.

For $O(n)$ companies the biggest stressor is making payroll. Invoices are paid net 30 or even net 90, but people expect to get paid twice a week. You either need excellent lines of credit, or a lot cash reserved, something which can be hard to do from scratch.

For $O(n^{2})$ companies the biggest stressor is growth and retention. Sure you have a runway, but generally PMF can solve all your problems so you can become default alive or raise your next round.

## differences (PMF)

Now we have come to another key difference. PMF is practically assumed, almost a certainty, for $O(n)$ companies. You understand your customer, and it's very easy to build for them. You are capitalizing on your networking/sales to become the default for clients while ensuring you keep them happy by running a tight, operationally efficient ship.

Because of this $O(n)$ companies have nice deadlines, clear SoW ([statement of work](https://en.wikipedia.org/wiki/Statement_of_work)), and are easy to reason about.

$O(n^{2})$ businesses sacrifice all this. The future is much less promised. All for the possibility of "hyperscale".

## conclusion

This brings us to perhaps the most important part of the essay: **$O(n)$ companies are higher EV than $O(n^{2})$ companies**.

I mean that, on average, a founder will make more money pursuing an $O(n)$ company than an $O(n^{2})$ company. And not an insignificant amount, the amount of liquidity and networth a 20m ARR $O(n)$ company is extremely hard to match by a traditional VC backed company.

People don't really tell you this because it is in VCs best interest people keep filling out lottery tickets, and it's in the $O(n)$ business owners best interest to keep their moat a secret.

$O(n)$ businesses (and founders), since they don't need to raise money or do much marketing, can keep an *extremely* low profile. It's very hard to access them simply because of obscurity.

### I think many prospective founders, if their goal is money, should optimize for $O(n)$ businesses from day 1.

[1] https://x.com/oceanmoist/status/1921751004938465347

[2] Perhaps choosing a better two functions could more closely explain the growth dynamics of network effects, which could be more exponential. I think the analogy diminishes in value if you try to directly numerically match it to some growth metric.

[3] $\Theta(n^{2})$ technically.

