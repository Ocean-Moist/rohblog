+++
title = "Why ML is DOOMED! (Formal Verification)" 
date = "2024-1-31T19:30:33-08:00" 
+++

A lot of people are into "AI/ML", and that **scares me**, and not only because half of them don't know what it is (see: non-technical cofounder of buzzword filled tech startup). You basically chuck a bunch of data into a black hole and it spits out this relatively massive file of weights that serves as an oracle for everything (ML-speak for random numbers intuited by dark magic [gradient descent]). 

Why does this scare me? Well it is because we trust our lives to these things **which exist apart from any self-consistent systems of logic** (at least one intuitable by humans). We don't know what Tesla's autopilot is "thinking". This is why LLM models are notoriously bad at math. My suspicion is even GPT-4 is using some sort of formally verified backend to do math, as GPT-3 was terrible at it. Basically just asking "Hey GPT parse this human input and generate an expression in the syntax of **Wolfram Alpha**". 

I predict, **formal methods**, especially in cybersecurity will become much more significant. And I think, even though the research has been there, no startups take advantage of it, because it is too "unsexy". At the very least, all complicated AI systems will come to have a stage or process that requires formal methods. 
### WTF are you talking about? 
Let me backup, what are formal methods? [Nasa](https://shemesh.larc.nasa.gov/fm/fm-what.html) says:

> "Formal Methods" refers to mathematically rigorous techniques and tools for the specification, design and verification of software and hardware systems. The phrase "mathematically rigorous" means that the specifications used in formal methods are well-formed statements in a mathematical logic and that the formal verifications are rigorous deductions in that logic (i.e. each step follows from a rule of inference and hence can be checked by a mechanical process.)

They go one to say formal methods are not used due to the complexity of modern systems. Which is sort of true. What really is happening is that **formal methods are rarely built into the tools we use.** 
### A Story (why failure is success in disguise, and my next project)   
Naively, I tried to write a quick script to formally verify C. I wanted to see if it could identify heap overflows (this is usually called [concolic testing](https://en.wikipedia.org/wiki/Concolic_testing#:~:text=Concolic%20testing%20%28a%20portmanteau%20of,testing%20on%20particular%20inputs%29%20path.)). **This is hard for many, many reasons.** The main one was that, errors, heap overflows are fundamentally not explicit, extraordinarily hard to identify when they could happen. I mean, if we could identify them, it would built in to GCC! 

I realized something though, some languages really restrict side effects and their semantics are more interpretable via formal methods. This is, of course, functional and statically typed programming languages (also helps if only const vars exist). Like haskell. So I planned to play around with it, but **not** with C **or haskell**.

### Why not haskell? (other than it being [useless](https://www.youtube.com/watch?v=iSmkqocn0oQ&pp=ygUSaGFza2VsbCBpcyB1c2VsZXNz))
Haskell semantics are notoriously difficult, with higher kinded types, and all sorts of PHD triggering abysses of mathematical complexity. In the wise words of a second-semester senior: **Im not doing allat.** 

### Why [Roc](https://www.roc-lang.org/)?
I love Roc. It is almost exactly my **dream programming language** (other than the decision for currying to not be automatic and how point free syntax is an "anti-pattern"). A functional language designed to be embedded in other code. In this way Roc (or rather the environment surrounding Roc code) abstracts effectful state away, while maintaining the concision and robustness of a language like haskell. 

AND the compiler is written in **rust**, just like my own programming language. AND its semantics are INTENTIONALLY simpler than haskell. AND its new, not bogged down by bureaucracy! 

I envision a future where if a specific part of your application, which is overall written in say C or another language, is mission critical and lends itself to FP design patterns, you can write it in ROC and **verify that there does not exist a set of inputs that allow the function to be "hacked"** (privileged behavior). 

### On hacking (and how I think about computer science)
Every program is, fundamentally a **function**. A mapping of inputs to an output. For example, a CLI app's input is its arguments and it produces something that lowkey looks like an output. 

So, as a hacker, let call a program `f(x)` and lets call `x` its inputs. Basically we have to find an `x` and an `f(x)` pair that is interesting. **It's a satisfiability problem!** 

Take a banking app. I want to find an `x` such that `f(x)` is me having a million dollars. I need to find a set of inputs that satisfy this constraint. One input might be cashing a check that's actually worth a million dollars. But there might exist  an input that cashes a fake check that I trick the program into thinking is worth a million dollars. 

So how do you find such an `x`? There is something called [SMT solvers](https://en.wikipedia.org/wiki/Satisfiability_modulo_theories) that can do this for well defined systems of logic. They are heavily used in concolic testing and I think there is a **distinct asymmetric advantage** to applying this tech (and other formal methods) to cybersec and other forms of innovation. (this is the real millenium problem)

### What are effects (why a CLI app only does stuff that "lowkey" looks like outputs) 
In reality all programs are only useful **insofar as it has effects** (SPJ's point in the haskell is useless discussion). **Every interaction**, all IO **needs effects**, which is why haskell wraps every bit of IO in monads. Roc solves this problem differently as I mentioned above. These effects can programmatically represented as state (types or something) and then turning them into effects is simple.  For example, take a Roc program embedded in a procedural lang (basically ONLY effects, maybe not even turing complete). 

Take side-effect ridden input (stdin) and pass it off to Roc -> Roc pure, easily testable, function -> Take Roc output and do effects strongly correlated with Roc output.   

**Roc never does IO (effects)**, the environment handles that, but the business logic is done in Roc. I also want to mention that Roc also can handle IO, but I think this use case is much cooler. 

### tl:dr My next big project 
Concolic testing and formal methods in [Roc](https://www.roc-lang.org/). 
