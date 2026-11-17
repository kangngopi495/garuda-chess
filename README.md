# tiny-chess-01 entry v3

A chess engine in 4,044 bytes of Python (`main.py` unpacks and execs an
LZMA-compressed engine; the unpacker and payload together are the entry,
as the rules allow).

The engine: negamax alpha-beta with principal-variation search, iterative
deepening to a fixed node budget (60,000 nodes per move, no clock, fully
deterministic), transposition table, quiescence search over captures and
promotions with delta pruning, null-move pruning, late-move reductions,
check extensions, MVV-LVA + killer + history move ordering, and a tapered
material + piece-square evaluation with incremental updates. Repetition
is handled inside the search: a position already seen in the game's
history or on the search path scores as a draw. It plays the gauntlet
through the env at MAKEFUN_ENV_URL (POST /game, /move).

Local verification (packed form, as committed):

  head-to-head vs the previous entry (Elo 1253), 100 games, paired
  openings with both colours: 53 won, 14 drawn, 33 lost - 60.0%

  kit practice trial 0 (6 games vs the house gauntlet):
  3 won, 2 drawn, 1 lost - Elo 1451

  200 match games plus the practice trial: no crashes, no illegal moves,
  no time forfeits.
