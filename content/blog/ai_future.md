+++
title = "How AI Will Create the Future" 
date = "2025-01-06" 
+++

My vision for how AI will create the future.

<blockquote class="twitter-tweet" data-theme="dark"><p lang="en" dir="ltr">AI won’t replace programmers, but rather make it easier for programmers to replace everyone else.</p>&mdash; Naval (@naval) <a href="https://twitter.com/naval/status/1875297712993964231?ref_src=twsrc%5Etfw">January 3, 2025</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>  

## core belief

### Every company will become a tech company

People said this during the web era, and they were partially right. Every company has a website, every business manages some online presence. But the web was merely the protocol over which business was done. AI will fundamentally change *how* business is done. The magnitude of labor reduction and efficiency gains with AI is much higher than with the web, and the transformation is more essential. **Instead of seeing companies with tech, we will see more tech companies.**

## a new mental model for AI

I think of each call to an LLM and its subsequent output representing a quantum of intelligence—a discrete packet of cognitive work. Every business needs X quanta to run, whether sourced from humans or machines.[1] 

This is counterintuitive because humans don't emit intelligence in quanta. It's much harder to quantify or track productivity (quanta of intelligence per dollar) for individual humans. It's also much harder to maximize human quanta at scale—think of the inefficiencies of bureaucracy and organizational hierarchy.

## the challenge

From first principles, you must break down business problems into sub-problems that can be tackled by quanta from LLMs. Notably, it is hard to this with current AI tools and those who figure it out are keeping it secret and trying to build companies out of it. 

Consider customer support automation:
1. A ticket comes in and the triage agent[2] categorizes it and routes it
2. The knowledge base agent searches internal docs and previous solutions
3. The resolution agent drafts a detailed response using this context
4. The QA agent validates the response against company policy
5. The followup agent monitors customer satisfaction and escalates if needed

Each step represents a discrete quantum of intelligence that traditionally required human judgment. The hard part is architecting the system so these quanta work together effectively. I would imagine a business in the future to look like building and deploying these workflows/agents/automations.[3]

## in practice

Companies like https://www.origamiagents.com/ are already doing this and generalizing it and selling it. Imagine if every company just built these workflows for their exact situation and cut out the middle man, that's the future we are headed towards. A company with a lean technical team will beat out incumbents just based on efficiency gains from removing people. The bigger the company the harder they will fall, as companies scale they get less quanta per person. Scaling LLM "agents" or workflows will not run into this problem. It will happen very slowly and then all at once, as the efficiency gains are so great that once an "AI-first"[4] company gets a foothold in a given market, the competitors will be forced to change. Think about all the businesses that died because of the web. Adapt or die.

People are currently building platforms that plug into existing enterprise structures for non-technical people, consider devin. However, each business has unique needs and needs unique workflows which are best structured and created by technical people, i.e. software engineers. 

It turns out we already have many elegant languages for building specific, structured, testable, and scalable workflows. This "decomposition" is such a hard problem to solve it will necessitate the expressive power of programming languages. Building great software already requires thinking from first principles and decomposing big problems into human digestible and delegatable pieces. So I think software engineers will be the best choice for these AI "builders" and I think no-code tools will ultimately fail.

[1] CoT/o1 is grouping these quanta together. The issue is with CoT/o1 the price of intelligence scales exponentially and it's much cheaper and more testable/observable to manually break the CoT into separate calls/workflows. To enable agents on the model level you would need to allow tool use while reasoning, something that safety people are probably working diligently to provide. Even then it makes sense to have some structure and modularity to take agency away from the model and direct it to us humans. It's also cleaner to have many small workflows which each have a few tools, instead of one massive workflow with one massive list of tools. Once the TTFT/latency comes down CoT will be pretty good. 

[2] For me agents are LLM systems that are:
1. Goal oriented
2. Able to "interact" with their "environment" 
	a. By "interact" I mean observe or/and make changes (think tool calls). 
	b. By "environment" I mean whatever context you give it. 

Or rather, agents are LLMs that use structured outputs in an effectful way. 	 

[3] Consider how terrible and imprecise the naming is, this is indicative people are struggling to actualize this vision and that it is very early, perhaps too early. 

[4] I struggle to use the term "AI-first" as this description is likely to get its meaning hijacked by corporate doublespeak. 


