+++
title = "On Zero Sum Games (The Informational Meta-Game)" 
date = "2025-02-02" 
+++

### These are my thoughts on zero sum games. From poker to quant trading. 

Zero-sum games are fundamentally informational contests. The GTO (unexploitable) strategy is often suboptimal in practice because it is either unimplementable or even unknown and assumes everyone else is playing optimally. The GTO strategy is not **maximally exploitative** it is **minimally exploited**. In a game of non-optimal participants, the GTO strategy is **not guaranteed to be the one that makes the most money**. In order to craft a maximally exploitative strategy you must **have information** about your opponents strategy while **concealing information** about your own. 

The Monty Hall problem elegantly demonstrates how information asymmetry drives outcomes in zero-sum scenarios. When Monty reveals a door, he's not randomly sharing information—he's bound by rules that make his choice meaningful. This transforms a simple probability problem into a strategic information game. The host knows everything, you know something, and that partial information advantage is what makes switching the dominant strategy.

## markets

In financial markets, the zero-sum nature of trading manifests through information asymmetry rather than pure strategy. While prices theoretically reflect all available information, reality is more complex. Traders don't seek an unbeatable strategy—they hunt for exploitable patterns in others' behavior. A high-frequency trading firm might detect when a large institutional algorithm typically breaks up big orders, creating predictable price pressure that can be anticipated and traded against.

Consider algorithmic feature spoofing: A quant firm notices a competitor's mean reversion algorithm triggers on specific price and volume patterns. They can deliberately create these patterns, essentially "feeding" the target algorithm its preferred signals while positioning to profit from its predictable response. To defend against this, sophisticated firms intentionally add entropy to their execution--deliberately randomizing parameters, switching between multiple strategies, or even taking occasional unprofitable trades. These entropy inducing behaviors are a pure cost in isolation, but they serve to obscure the true underlying strategy and make reverse engineering dramatically more difficult. 

Success comes from identifying exploitable patterns in opponent behavior while concealing one's own patterns and intentions. The meta-game becomes more important than object-level analysis. Technical patterns work not because they have inherent meaning, but because collective belief in them creates exploitable behavior.

## poker (skip if unfamiliar)

Consider table image in poker: A player might intentionally play loose and aggressive with weak hands early in a session, creating a reputation for reckless behavior. This manufactured image leads opponents to call their large bets later when they actually hold strong hands. The initial losses are an investment in creating exploitable patterns in opponent behavior--they believe they've identified a pattern (reckless play) while missing the actual pattern. 

Another poker phenomenon is making looser calls earlier in the session, or when at an informationally disadvantage. You are paying for information, even if your equity is bad. You get to see their cards. 

Further, modern poker players rarely do the same things in the same spots. They do carefully calculated actions at some predetermined frequency to shield their strategy from their opponents. This is much like the quant trading firm adding entropy to their execution to prevent reverse engineering from other firms.  

Obviously not investment advice. 

**UPDATE: 21 Feb, 2025. Rewrote for clarity** 
