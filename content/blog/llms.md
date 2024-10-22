+++
title = "Writing Code with LLMs Leads to Better Software (and other insights from building LLM systems)" 
date = "2024-10-08" 
+++

Recently I have been working on what I guess is called an LLM agent, but it's more just building more ergonomic tools for myself to use LLMs in my life. The code base keeps growing, and I use it to help write itself.    

What I have noticed is that the patterns I have applied for making code more intelligible to LLMs also apply to making code more intelligible for humans. I think the reason for this is that LLMs can only successfully hold so many details in their context window, and we can only hold so many details in our mind. These observations may seem obvious, but what's so interesting is that two different sets of constraints lead to similar invariants. 

Generally if you `find . -name '*.go' -exec cat {} + >> out.txt` and just append that to the prompt, the LLM will get confused if it's being asked to do something mildly complicated and if out.txt is over >5k lines (degraded performance around 2-3k). This is like if we had to keep a whole API, implementation details and all, in our head while using it. 

When faced with this issue there are a few easy optimizations. The Cursor AI method is to selectively provide a subset of relevant files. This works up to a point, because at some point, there are way too many relevant files and definitions. In order to decrease the amount of relevant files, you need to decouple your code and modularize it, so parts can be worked on non-monolithically, which is also general coding advice. 

Further, extracting common actions to an API, and then writing api docs so that the user (or LLM) does not have to concern itself with implementation details is another way to reduce the necessary context size. Initially I just wrote (or, rather, the LLM wrote) API docs for the backend REST api so the LLM could work on the frontend without concerning itself with backend code, but then my backend got way too complex. Then, I wrote API docs for my external API wrappers (I had go wrappers around OAI, Claude, GPTZero, et al) and other functions.

Overtime I split my project up using these es so that I could use LLMs more efficiently on them, then I realized I inadvertently made it easier for *anyone* to work on my project. As someone who codes a lot as a single person (and not as team) and who hates premature optimization,  I start (and end) most projects as a monolith. When you are the only working on a project you develop seemingly obvious intuitions just by working in the problem domain for a long time. I generally also don't write docs for solo projects except for a TODO list and spend little time worrying about naming.

So writing code for/with LLMs makes you write better software. I think this is a very counter-intuitive point. 

 ## general tip for coding complex projects with LLMs or making LLM agents

I find that LLMs have terrible intuition for creating big project's architecture, especially 0-shot. I am trying to solve this problem via prompting and other stuff in the very tool I am building. Even o1 models (though significantly better) still suffer from this issue. 

LLMs are maximally advanced beginner in all fields and will just make things that don't make sense and have terrible intuition. You basically have to supply intuition. There are 3 steps to software development: describing goals/functionality (planning) -> architecting -> implementations. The one LLMs struggle with is architecting. If you ask it to create an API that does XYZ on a high level it will struggle. If you ask to clarify what XYZ is it will excel. If you ask it to implement a, b, c API routes via implementing d, e, f functions it does pretty well. 

If you've been working in a large, monolithic, project for a long time, and you are tasked with implementing a simple feature you will think it's easy. You'll just define the shapes of the functions and fill them in, aligning with the patterns of problem solving used in the program. If you dump 5k LOC into an LLM and tell it to implement the same feature it will do terribly and the functions and their shapes will be convoluted or not clearly help solve the business objective.

To be fair, if you dump a new person in the same code base they will probably struggle too. The average new hire probably (hopefully?) is equivalent to o1-mini in coding. 

## random stuff/advice
Create new chats/contexts as often as possible and optimize for only including necessary information and compressing that information into the smallest amount of intelligible tokens as possible. 

I also noticed o1 tends to fix badly/complexly worded prompts so prompting is less important with it, you just have to prompt for guarding it from doing unrelated/unnecessary stuff.  

I find that after the initial gains I am somewhere between 1.5-2.5x more efficient at coding when using LLMs. Cursor AI value add vs. basic bash tools + LLMs is maybe around 20-30%, not worth leaving Jetbrains.  

ChatGPTClaude and other chat based interfaces have terrible UX. Cursor is better, but value prop is too weak for most actual programmers to switch. I'm thinking m going to neatly package all the tools I use, call it rhoGPT, and launch it. I suggest you write your own tools/agents, as interfaces with LLMs is (what I think) the next billion dollar problem.  

P.S. `find . -name '*.go' -exec cat {} + >> out.txt`, knowing other terminal text processing tools (sed, awk, etc), and vim/editor keybinds is the best 80/20 choice to implement creating prompts fo LLMs for coding. I suggest writing simple tools for creating prompts in bash first, you don't need anything complicated. 

I have a folder of common prompts in plain text files then I mix and match them using the bash tools. 

Perchance I am at the rare intersection of maximalist gen z LLM users and suckless driven linux hackers, but this workflow is surprisingly productive. 

Ask me question/provide feedback/share what interesting thing your building at my email--I reply to >95% of them. :) 

rganapav [at] purdue [dot] edu OR rohanganapa [at] gmail [dot] com
