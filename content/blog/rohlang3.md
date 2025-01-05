+++
title = "rohlang3: (an attempt at) a point-free, homoiconic, and dependently typed SK calculus" 
date = "2025-01-02" 
+++

### github: https://github.com/Ocean-Moist/rohlang3

I’ve long been obsessed with minimalistic languages that still manage to have expressive power. My usual approach: start with a bare-bones combinator calculus (like SK), then keep adding “one more extension” until it looks suspiciously like a full-blown typed language. rohlang3 is exactly that experiment. It’s a small language built in Rust that tries to be point-free, homoiconic, and (somewhat) dependently typed, all on top of an SK-like foundation—plus reflection, partial evaluation, and a weird environment reordering system.

I also have no formal education in these fields so I could have some fundamentally misunderstanding about any of these topics. 

## the core idea

At its heart, rohlang3 is the standard `s` and `k` combinators:

-   **`s`**: (sfgx)→(fx)(gx)(s f g x) \to (f x)(g x)
-   **`k`**: (kxy)→x(k x y) \to x

But that alone wasn’t enough for me. I piled on new combinators for reflection (`q` and `e`), partial evaluation (`z`), environment reordering (`i`, `E`, `D`), and a Pi/Sigma-style dependent type system (`p`, `g`). It definitely breaks “pure minimalism,” but it’s also what makes rohlang3 interesting to hack on.

## why dependent types?

I wanted some notion of dependent types so I could treat the language as if it were a mini proof system (even though that’s kind of precarious). We have a single universe `u`. You can do `(p u u)` for a Pi type or `(g u u)` for a Sigma type—both reflect a simplified (read: incomplete) approach to higher-level type theory. It’s enough to write small examples like (pu(ku))(p u (k u)) or (gu(i))(g u (i)).

Yes, there are well-known issues with having `Type : Type` (a single universe) if you’re aiming for total consistency, but I’m not losing sleep over it. The point was to see if I could make a “dependent SK calculus,” not to prove it bulletproof.

## reflection & partial eval

One of my favorite parts is the reflection combinators `q` (quote) and `e` (evaluate). So you can do `(e (q (s (k k) x)))`, and if it type-checks, rohlang3 “splices” it back into runtime. It’s like a minimal Lisp macro, except you’re still living in an SK world. There’s also `(z expr)`, which tries partial evaluation on `expr`. If it recognizes certain patterns—like `(s (k k) something)`—it can simplify them on the spot.

## environment reordering

I wanted a built-in notion of a “typing context” that you can reorder at runtime. This is where **`i`**, **`E`**, and **`D`** show up:

-   **`i`**: references the top of the context (like “the most recent binder”).
-   **`E`**: exchanges the top two binders.
-   **`D`**: duplicates the top binder.

So you can do `(E someExpr)` to swap the top two context elements, then evaluate `someExpr`. People used to neat, lexically scoped languages will probably find it weird. I find it weird too, but that’s the point.

## homoiconicity

rohlang3 is “homoiconic” in the sense that code is just an AST you can quote and manipulate. Once you parse an expression like `(p u (k (p u (k u))))`, you can reflect or partially evaluate it. The AST is just a handful of atoms and `App(...)` nodes, so it’s easy to manipulate from inside the language if you want to get meta.

## limitations

I’m not aiming to overthrow standard type theories or run production apps on rohlang3. There’s no illusions that it’s 100% consistent, or that it handles real-world performance or advanced features. This was mainly a personal playground for me to explore how these different concepts might fit together.

I also cannot write this language, like I am not close to grokking it. 
