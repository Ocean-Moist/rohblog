+++ 
title = "o1-preview is Pretty Good at Chess (a New Benchmark?)" 
date = "2024-11-14" 
+++
# overview
I figured the reasoning capabilities would lend themselves to chess, and they do. Right now I am limited by the 50 o1-preview requests I have to do research in this area so keep this mind when I share.

# testing vs stockfish
I was playing o1-preview against stockfish (via lichess), and it held up for the most part, but stockfish was winning when I ran out of tokens. It also played a lot of theory, we transposed from a psuedo-catalan to a neo-grunfield. I was the one playing white for the opening and just played the theory I knew. (find game record at the end)

From what I can tell, it only generally uses a depth of 2-3 and its breadth is much narrower than other chess engines. This is characteristic of a human. Once inference time compute is scaled, I think that the breadth and depth will increase to a point where it will at least match Stockfish and other top engines.

# technical challenges & solutions
Around move 25 it started spitting nonsense moves, so I looked at what the reasoning traces said and I saw it try and process and step through the PGN or recreate the FEN in a different internal representation. So I asked it what format it would like the board state to be communicated in and to make a python script to generate them.

After using the script it made (with some modifications), it replied with valid moves. Put your FEN into the [script here](https://gist.github.com/Ocean-Moist/0064caf583bc4ccf4151fd1a50601836) and paste the output into o1-preview to get your next move. Perhaps if I used this from the beginning the moves would have been of a higher quality. 

# cognitive similarities to humans
What's interesting is that the same things that would make it readable to a human make it readable to the machine. Originally it seems it was first interpreting the PGN/FEN into a format it understood and then doing reasoning from there. This is the same thing humans do. They have a internal representation for a chess board that they can visualize transformations of it, most chess pros are used to pgn so they communicate their thoughts via that. This is what allows chess pros to play games without a board, or blindfolded.

I wonder if similarly, if you finetune a model to communicate via PGN (chess puzzles, calculating lines, playing games), instead of relying on inference time interpretations, you will notice improved performance. This would allow it to build an internal representation of the chess board. If you notice chess pros playing, they often look up and to the left/right to visualize different board permutations and continuations when calculating.

# potential as a benchmark
I would love to automate this and make it a real benchmark for reasoning models, as this seems like a new capability of them vs. previous LLMs. I estimate o1-preview is around ~1600-1800 chess.com, though take this with a massive grain of salt (n=0.8, I am around 1900 chess.com). It would be hard as each game would cost you a bunch of money. I found that o1-mini has a much harder time providing coherent moves.

# game record
PGN: 1. Nf3 d5 2. d4 Nf6 3. g3 g6 4. Bg2 Bg7 5. O-O O-O 6. c4 c6 7. Nc3 e6 8. cxd5 exd5 9. Ne5 Nbd7 10. Nxd7 Qxd7 11. Re1 Re8 12. Bf4 Nh5 13. Be3 f5 14. Qd2 Qf7 15. Bh6 Bxh6 16. Qxh6 Nf6 17. Rac1 Ng4 18. Qd2 f4 19. Qxf4 Qxf4 20. gxf4 Nf6 21. Na4 Nh5 22. e3 Nf6 23. Nc5 b6 24. Nd3 Ba6 25. Rxc6 Bxd3 26. Rxf6 Rad8 27. Rc1 Bc4 28. b3 Kg7 29. Rc6 Rc8 30. Rxc8 Rxc8 31. bxc4 b5 32. c5
