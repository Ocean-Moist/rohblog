+++
title = "Java is an amazing language (better than rust)" 
date = "2024-03-05" 
+++

DISCLAIMER: Let me preface this by saying my favorite language is Haskell and that I write toy languages for fun. I am a pl nerd so my opinion is valid. Also the title is like 20% bait. 

My secret was always that I like coding in java, in some sort of masochistic way. Everything is dead simple. Everything is so verbose you can never forget what anything is. It is like sitting down and playing a relaxing game of stardew valley. It flows so easily. The feeling of mastery is so easy to attain. 

Coding in rust is like playing chess and league at the same time. It is the same mental exertion and the same insufferable people yelling at you on the internet. The semantics are cool. I love how it borrows stuff from functional languages. But can I tell you a secret? Java gets 75% of the way there with 10% of the complexity. 

Error handling is definitely better in Rust, but it is closer than most think. The way errors get buried and propagated up the call stack can be confusing. In complex programs it can be missed. Pattern matching is better in Rust, but is closer than most think. Java records, java switch statements, Optional<>, streams, they all basically make up for the OOPiness of the language and are all pretty straight forward. Also the concurrent data structures in java are much nicer to use than in rust. 

Learning rust is hard, it could not be the language AP CS is taught in. The first skill gap is the borrow checker, then lifetimes, then async, and then macros. The smallest, first skill gap, the borrow checker, was about 10 times harder than learning about Java classes for the first time, and about 3.5 times harder than grokking monads. I still can  BARELY write complex async rust, and if I see or have to write a macro that is like a hair above the simplest examples I will quit the editor. 

I would say the most clusterfucked abstract class inheritance system design in Java would not even approach the most complex Rust system design. Then again, I have not worked in a legacy Java environment, but I think this argument is still valid. Rust simply does not scale as well as Java. 

I also hate the skill issue argument. Like you know what the ultimate skill issue is? You not knowing C well enough to make memory safe code. Forget C, you not going complete rollercoaster tycoon and writing some plain x86 assembly. 

The whole point of a language is to be easy. Basically the Go philosophy (which I do like more than Java these days, although it does not have the functional stuff I want). Like the whole point of high level languages is to never encounter such skill issues. It is to write working code fast and in a maintainable way. Naturally you would want this to be easy. 

It is so easy to write good java with a few guidelines. Duplicate 1-2x before abstraction. No inheritance unless you are sure, especially no more than one layer deep. Use Optional<> over null. Do not get cute with your abstractions. Java is so easy people feel the need to make it hard doing OOP gymnastics to build "elegant" systems. 

Now here are some cheap, easy arguments. More people know Java and more jobs need Java. Tooling is better for Java and the ecosystem is more developed. I absolutely love JetBrains IDEA and no amount of loser lua neovim (don't come after me I use neovim for C, zig, and other low level languages) config for Rust will match IDEA's support for Java. (also if the primeagen is reading this, lua sucks, don't @ me, it is never enjoyable to write, imagine liking the language I used to code roblox hacks in when I was 9 years old).

I am going to admit, maybe I just do not know rust enough. But I promise I have coded more rust than most of you have, and I probably know it better than the average self proclaimed rust enthusiast. And yet, if I had to write a big grug "business logic" project, you would see me reaching for Java before rust.  

The final thing about rust is that it is not even particularly elegant. Haskell is nice to look at, APL (BQN, UIUA) is nice to look at. When I want a puzzle I write in those languages. Because I admire the mathematical abstraction. Rust is marred with the compiler, marred with low level BS that makes it ugly. That does not make it satisfying in this way. If you love language design, or beauty in programming languages, Rust is not even that good. It is not beautiful, it is not as useful as people proclaim, and it occupies such a small use case that the language is mid.  

Even when I do systems programming, like low level stuff, I just want to manage my own memory. I do not want to beg the compiler to let me write code, I just want to allocate stuff and put stuff into there. C is fine for this. I'll try zig later. 

And I am not saying rust is always bad. It has a small but limited number of use cases. For example I wrote a bot that helped buy things rather quickly in 2020-2021 (provided I was awake to do some captchas). I needed it to be performant, robust, and the scope was just simple enough (even though it was async) where I knew I would not need a lot of code (but a mediocre amount). It occupied the space just before the complexity curve went asymptotic. The other use case is for writing toy languages, it does that super well. At its best it feels like using a cnc mill to machine a precise gear. But most times you just need an injection mold and some plastic. 

P.S. check out this fizzbuzz impl. I did in Java, I have not found a similar solution in Java ANYWHERE on the internet. It also shows the power of modern Java. (please do not actually use this in an interview) https://github.com/Ocean-Moist/FizzBuzz/blob/master/src/Main.java  

P.S. plz write your applications in Go instead of Java, otherwise you might get brainwashed by RxJava. if this happens, no one has found a cure. 


