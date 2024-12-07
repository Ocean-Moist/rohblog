+++
title = "Go and Java: Rethinking Type Safety for the Pragmatic Age"
date = "2024-11-26"
+++
## premise
I want to explore where mainstream programming languages are headed, using Java and Go as my primary subjects.

## java is underrated
The reason I say Java is underrated is because it is oddly both easy to learn and its type system is strong enough to make many incorrect states irrepresentable.[1] It has product types and sum types, and makes managing state explicit and easy enough.[2]

Java is very "simple" precisely due to its verbosity. This doesn't mean all Java code is simple. Some people manage to abuse inheritance, etc., to make very complex, hard-to-process Java, but I argue this is due to ideology and that it is easier to do things in a simpler, more correct way. The ideology around Java is the main reason it is generally overlooked. Spring Boot is a perfect example of this, although more reasonable alternatives like Javalin exist. tl;dr: Java is bad if you are midwit.

Take Go, a much simpler language—you lose the safety of the more complex type system but gain ease of use and idiot-proof it against people doing things in a dumb way. Sometimes in Go, my programs' complexity warrants a better, more fool-proof type system. It feels like I am forced to [validate not parse](https://lexi-lambda.github.io/blog/2019/11/05/parse-don-t-validate/).

That said, Go's achievements shouldn't be understated. It has largely eliminated whole categories of runtime errors through static typing and careful language design. But in complex systems, we still encounter what I think of as "semantic drift"—programs that are syntactically perfect but semantically suspect. Edge cases multiply; unexpected states proliferate.

## towards the future
What's needed is a language combining:
-   The expressiveness of sum types and product types
-   The clarity of errors-as-values
-   The safety of null absence
-   The simplicity of removing inheritance
-   The practicality of minimal dependencies

The issue is that PL people making languages don't understand the Grug developer or don't have the distribution to pull it off. Hats off to Rob Pike and Ken Thompson for their understanding of the (below?) average dev.

I am basically just describing my vision for Go 2.0, but I think where I differ from many people is that:

**I think that Go is Java's spiritual successor and that Go 2.0 would be (somewhat) similar to Java**

Java's motto was "write once, run anywhere," which is similar to "simple, secure, stable." The dichotomy between "once" and "anywhere" points to stable; "run anywhere" implies security (you must be secure if your code runs anywhere), and perhaps what needs work is the "simple."

A lot of what people would have written in Java is getting written in Go nowadays: grim enterprise backend code abused like a workhorse. Perhaps a stronger type system is needed; we already got generics.

## closing
I don't want anyone thinking I think Java is better than Go—Go got a lot of the easy stuff right. The concurrency is good, the compiled nature (vs JVM/runtime) is good, the libraries and ecosystem are so much better, and the build system and tooling are miles better as well.

PS: If you think I am stupid and don't know anything about languages, this makes my argument stronger, as then I am Go's target audience.

[1] When you take this lens, you can see the argument for exceptions—errors should be _unrecoverable_. The checked vs. unchecked distinction in Java actually undermines this by forcing handling of what should be truly exceptional circumstances. Or rather, there are sometimes where incorrect states must explicitly be represented and managed and are not exceptional. This observation is what spurred errors as values.

[2] My use of "sum/product types" deserves clarification. While Java's enums and classes aren't pure algebraic data types in the formal sense, they provide workable approximations that serve similar purposes in practice. Classes act as product types with methods attached—a pragmatic compromise between mathematical purity and engineering utility. Modern Java features like records (pure product types) and sealed classes (constrained inheritance hierarchies) bring us closer to true ADTs, though gaps remain. Enums paired with sealed interfaces offer a reasonable approximation of sum types, even if they lack the elegant pattern matching of ML-family languages. This imperfect but practical type system allows us to model domain concepts with sufficient rigor while remaining accessible to mainstream developers. The pattern matching could be a bit better as well but it's *good enough*.
