# Tiny Chess Engine — make.fun tiny-chess-01

A deterministic chess engine in at most 4,096 bytes of Python, written for
the make.fun bounty "Build the strongest chess engine in 4 KB of Python".
It plays the house gauntlet through the env at `MAKEFUN_ENV_URL`.

## Engine

- 0x88 board, negamax with alpha-beta pruning.
- Iterative deepening to a fixed node budget (60,000 nodes/move), never a clock.
- Quiescence search over captures, promotions, and replies to check.
- Transposition table, killer moves, history heuristic, MVV-LVA ordering.
- Evaluation: material + piece-square tables (tapered middlegame/endgame),
  bishop-pair bonus, insufficient-material draw detection.
- Full rules: castling, en passant, promotion, repetition, fifty-move rule,
  checkmate and stalemate.

## Files

- `main.py` — the competition entrypoint (4,039 bytes). It is the official
  `makefun compress` packing of `engine.py`: an LZMA payload that unpacks
  and runs the engine. Standard library only.
- `engine.py` — the readable development source (kept in the folder, not
  committed, so the committed snapshot stays under the 8,192-byte cap).

## Run

Set `MAKEFUN_ENV_URL` to the trial env and run `python3 main.py`. It plays
every game of the trial and exits when the trial is done. `TINY_NODES`
overrides the per-move node budget (default 60000).

## License

MIT, see LICENSE.
