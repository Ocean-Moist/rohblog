+++
title = "Ideas for Super Intelligence"
date = "2025-04-12"
+++

This essay is about the nature and character of algorithms that would lead to artificial super intelligence (ASI) primarily through recursive self improvement. It is a window into my intuitions at the current time.

## current bottlenecks

OpenAI just recently released a [long form podcast](https://www.youtube.com/watch?v=6nJZopACRuQ) talking about primarily pre-training gpt4.5 and the various lessons that it taught them. I never thought I would see such transparency from OpenAI and it serves as valuable insight into the current state of ML research.

One of the researchers mentioned: "we were largely just in a compute constrained environment... but now we're in a very different kind of regime starting with 4.5 for some aspects of the data where we are much more data bound." And further that "The transformer, the GPT, is spectacular at making productive use of data... but there's somewhat of a ceiling to how deep of an insight it can gain from the data."

The issue I see is that we have effectively saturated the knowledge to be gained from all textual data. We can think of transformers and intelligence largely as compressors. This idea has been around for a long time (see: hutter prize), is [formally observable in transformers](https://arxiv.org/html/2404.09937v2), and perhaps even more tellingly, is literally what [cross-entropy loss](https://chatgpt.com/share/67fadb8c-2b44-800e-9ddd-856b219fca2e) is. We have found structures (mechanisms, if you've been follow the [Anthropic mechanistic interp papers](https://transformer-circuits.pub/2025/attribution-graphs/biology.html), [sister paper](https://transformer-circuits.pub/2025/attribution-graphs/methods.html)) that compress all data (full available textual corpus) efficiently. We can't really improve intelligence directly by continually training on this data because our mechanisms compress all our available data effectively.

To sum up current sentiment: **we are out of data which naturally embeds complexity to train our compressor (intelligence) on**. We have fully saturated out the complexity of our data. There exists no corpus of text which isn't efficiently compressed by current models.

## better data

The logical next step is to figure out **how can we get better data?**. Current data is already super contaminated with LLM generation, and is not growing fast enough to meet this need, so it seems the only option is **synthetic data**. The issue is LLMs need out of distribution (in a way which encodes complexity) text to train on, and definitionally, can itself only generate *in distribution* data. It's important to note (for both now and later) noise is degeneratively out of distribution/hard to compress but doesn't encode underlying complexity. So the issue becomes generating **out of distribution data** that **is hard to compress** but **not noise**.[1]

Well then, if we could generate such data, **wouldn't that require a model better than the one we are trying to train?** This is the hardest part of the problem to solve. Yet, I don't necessarily think this is true.[2]

As an example, NP problems provide a perfect template for generating data that is hard to compress but not random noise. Consider cryptographic hashes: they are deterministically generated from inputs (not noise), but trying to reverse engineer the input from the hash is computationally infeasible. This type of asymmetry is precisely what we need.

Formally, we can think about this using a framework with three interacting parts: an **Answer Generator (AG)**, our primary model being trained, whose goal is simply to get better at compressing the data it sees (i.e., minimizing its prediction loss, $\mathcal{L}\_{AG}$). Then there's a **Question Generator (QG)**, which generates the challenging data for AG. And finally, a **Discriminator (D)**, acting as a sort of 'realism judge'.

The QG doesn't need to be universally "better" than AG. It needs to be good at one specific thing: finding AG's current weaknesses and generating data that targets them, while staying realistic according to D. It leverages asymmetry (like NP problems). QG's objective is different from AG's general compression goal.

AG just tries to compress better. QG's goal is more complex: it tries to generate sequences that are *hard* for the current AG to compress (high $\mathcal{L}\_{AG}$ or BPC) *but* that still look like plausible, structured data according to the Discriminator (D). D, in turn, is trained to tell the difference between QG's outputs and real data (from a corpus $C$ like the web text), optimizing its own loss $\mathcal{L}\_{D}$. QG is thus rewarded ($\mathcal{R}\_{QG}$) for both difficulty and realism.

If you kind of squint at this AG-QG-D setup, it refines the **generative adversarial network** ([GAN](https://developers.google.com/machine-learning/gan)) idea: AG is the learner focused on compression, QG is the challenger trying to find AG's weak spots in understanding structure, and D keeps QG grounded in reality. QG's objective is different from AG's, and it could potentially use information about AG's performance (like how badly it compressed the last sequence) to generate the next challenge, creating the needed asymmetry.

## two ways to adversarial generators

So, how does QG generate these challenging sequences? I can think of perhaps two distinct ways to conceptualize QG's role here:

1.  **QG as a Structure Explorer:** In this view, QG focuses on the **external, abstract underlying structures** inherent in complex data – things like grammatical rules, logical entailment, algorithmic patterns, causal relationships. It learns to identify these structures (perhaps from corpus $C$ or through interaction) and then generates novel sequences that embody these structures in challenging combinations or applications. It doesn't necessarily need deep insight into AG's internals; it probes AG's understanding by presenting it with complex, structured realities, relying on the Discriminator (D) to ensure these structures are grounded and not arbitrary. Difficulty for AG arises from its inability to efficiently model these external structures.

2.  **QG as a Mechanism Projector/Generator:** This view aligns more closely with my initial intuition involving the Anthropic interpretability work. Here, QG's focus shifts **inward**, towards the **internal computational mechanisms** within AG itself. It would need tools to understand AG's current mechanisms (via interpretability) and potentially predict how mechanisms might evolve with scale. QG's goal would then be to *project* or *elicit* specific, desired mechanisms in AG by generating precisely crafted sequences ($x$) such that efficiently compressing $x$ forces AG to develop or strengthen a particular internal circuit or capability ($M$). The difficulty ($\text{BPC}\_{AG}$) is directly tied to AG's lack of the target mechanism $M$. This is a more targeted, "inside-out" approach.

Of course, the most effective approach might ultimately involve a **synthesis**: a QG that explores broad external structures *and* uses available interpretability insights to probe specific mechanistic weaknesses when possible.

Regardless of the exact view, the core training loop remains similar: Train D on real vs. QG data. Train QG (as Explorer or Projector) via reinforcement learning to maximize its reward ($\mathcal{R}\_{QG}$) for generating realistic and difficult sequences. Train AG on these challenging sequences from QG, forcing it to improve its compression ($\mathcal{L}\_{AG}$) and thus internalize the structures or develop the mechanisms QG is pushing for. As AG learns, QG must adapt to find new frontiers of complexity.

We basically are trying to **generate and train a model on more complex relationships (or elicit more complex internal computations) than are present (or rare) in the human corpus of text**. By forcing AG to compress these structurally complex, realistic sequences, it must develop more sophisticated internal representations/mechanisms. Intermittent training on the human text corpus could still be valuable for AG (like fine-tuning) to keep it grounded in human language and tasks.

I think here is where the core challenge still lies: the precise architecture and learning process for QG to *effectively* function as either a Structure Explorer or a Mechanism Projector (or both) is the crux. How does it represent and manipulate abstract structures, or predict and target internal mechanisms, to generate novel, challenging, yet coherent sequences? That's the hard part. Hopefully, framing the problem with this AG-QG-D setup, and considering these different facets of QG's potential role, makes it clearer for further research. 

## creating the arbiter of *reality*

The Discriminator (D) now brunts the frontload of potential contradictions and complexity. Its explicit task is to distinguish between real data (from corpus $C$) and synthetic data generated by QG, essentially learning $P\_{data}(C)$. However, the entire system's goal is to generate data *more complex* or *structurally novel* than what is typically found in $C$ to push AG's capabilities beyond the limits imposed by $C$. This creates a fundamental tension: **How can D, whose benchmark is the "saturated" past data $C$, possibly approve or guide the generation of novel data that surpasses $C$'s complexity?** If D perfectly enforces similarity to $C$, it would reject the very data needed for AG's progress.

Resolving this tension requires D to be more than a simple pattern matcher comparing QG's output directly against instances in $C$. Its function must be more nuanced:

1.  **Learning *Principles*:** The key is that D must learn the *underlying principles, rules, and constraints* that make the data in $C$ coherent and structured, rather than just memorizing superficial patterns. It needs to capture the *latent space of valid structures* implicit in $C$. 

	This means understanding grammar, semantic coherence, logical consistency, and even notions of causality and certainly a bunch more ineffable notions about the structures underlying the way we interpret our reality.[3] A powerful D, having learned these principles from $C$, could then recognize a novel sequence generated by QG as "realistic" if it *adheres to these principles*, even if the specific combination of ideas or the level of complexity is unseen in $C$. Think of a grammar checker: it accepts syntactically valid sentences never seen before. D needs to act similarly for deeper structural properties.

2.  **Rejecting of Degeneracy:** In practice, a crucial role for D is likely preventing QG from "cheating." QG could potentially generate high-difficulty ($BPC\_{AG}$) sequences easily by outputting random noise, repetitive patterns, or simple adversarial examples targeting flaws in AG's architecture. D acts as the essential filter against this *structural degeneracy*. Its primary task might be less about enforcing *strict* similarity to $C$ and more about ensuring the output possesses *plausible structure* and avoids obvious non-sensical failure modes. If a sequence passes this "coherence check," it might receive a sufficient realism score from D, allowing the difficulty metric ($BPC\_{AG}$) to dominate QG's reward function and drive exploration.

3.  **Guiding Exploration via Probability Gradient:** D outputs a probability $D(x)$, representing the likelihood that $x$ came from the real data distribution $P\_{data}(C)$. QG's reward typically involves balancing realism (e.g., $\alpha \log D(x)$) and difficulty (e.g., $\beta BPC\_{AG}(x)$). This allows for a trade-off. QG can be rewarded for generating sequences that are slightly less probable under D's model (lower $D(x)$, perhaps at the edge of the distribution learned from $C$) if they are significantly harder for AG to compress (high $BPC\_{AG}$). D thus provides a *gradient* guiding QG away from pure gibberish while permitting exploration into less charted, potentially more complex territory that still retains structural integrity.

4.  **Validating Combinatorial Complexity:** Significant complexity increases can arise from novel combinations of existing concepts and structures, or applying them at unprecedented scales. QG might specialize in finding these intricate but valid constructions. D's role here is to recognize that the *building blocks* and the *rules of combination* are sound according to its learned principles from $C$, thereby validating the realism of the complex new structure.

**Requirements and Challenges for D:**
For D to fulfill this sophisticated role, it must itself be a powerful model, likely comparable in capability to AG and QG. It needs robustness against adversarial inputs from QG. It must effectively capture long-range dependencies and abstract properties. Its success hinges on its ability to generalize beyond the specifics of $C$ to the underlying structural principles. 

Failure modes are significant: D could be too strict, stifling novelty; too permissive, allowing degenerate data; or simply fooled by a sophisticated QG, leading the entire system astray. Ultimately, D must implicitly build its own robust world model based on $C$ to effectively judge the plausibility of novel constructs. Its quality directly gates the quality and effectiveness of the synthetic data generation process.

Here is a [more formal write up of the ideas presented here](https://drive.google.com/file/d/1FD9eXcMy8M0YJRFi-v9FV8cPVDgW4DpY/view?usp=sharing).

[follow me on twitter.](https://x.com/oceanmoist). 

## funding 

I am currently working on consumer AI products (pre-PMF) and doing ML research (releasing research on making attention mechanisms more efficient and compressing model weights soon). I am also running out of money. I am looking for an angel check/grant. 

I am a polymath with experience in everything from:
- [self-hosting/physical infra](https://x.com/oceanmoist/status/1910788994247385450)
- [pl theory](https://rohan.ga/blog/rohlang3/)
- [linux/deploying systems](https://x.com/oceanmoist/status/1862384551991156819/photo/1)
- [web dev/SaaS](https://kara.rhogpt.ai)
- [writing/philosophy](https://rohan.ga) (this blog has been visited by well over 30k people with 10+ essays >1k visitors)
- [game theory/quant trading](https://rohan.ga/blog/zero_game/)
- and about a million other things. 

I can build or do just about anything. I am completely self-taught in ML and everything else. 

If you want to know more about my experience or are interested please email me: rohanganapa@gmail.com. 

[1] Interestingly, in our post-structural academic culture (which leads to a high multiplicity of mechanistic structures) a lot of the academia is hard to distinguish from noise, as pointed out by the Sokal affair et. al. I think this is an even bigger problem, because a lot of the hard to understand world changing ideas look like noise, and due to the large majority of such ideas looking like noise, are treated as such. 

[2] For the naive case of 2 transformers training on eachothers outputs it is obviously true, though. 

[3] An important philosophical question: what are the structures underlying the way we interpret our reality? [Kant gave his 12 categories for human understanding.](https://plato.stanford.edu/entries/categories/#KanCon)

Further if you ask me to describe how I view intelligence philosophically, I would say it's a continually growing self-consistent rhizomatic structure. Consistent in the sense where any given node or idea has to connect back to some other. 

We both attack reality with it (it structures/contextualizes our understanding) and subsume some more nodes/ideas from our stimuli. 

I would say the corpus of human text is the affectation of such rhizomatic structure. And that LLMs simply are able to generatively build up this structure from this text. This structure is much implied but the effectiveness of LLMs, and the failure of Chomskyan techniques which imply a too strong/consistent underlying structure behind text.  
