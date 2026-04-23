# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Single-file Gomoku (五子棋) game — `gobang.html` contains all HTML, CSS, and JavaScript. No build step, no dependencies.

## Development

Open `gobang.html` directly in a browser. No server or build tooling required.

To run a local dev server (optional):
```bash
# Python
python -m http.server 8000
# or Node
npx serve .
```

## Architecture

- **Board**: 15x15 grid, rendered on a `<canvas>` (540x540px)
- **Game modes**: PvP (`pvp`) and PvP-vs-AI (`ai`, default)
- **AI**: Greedy heuristic — `evaluatePosition()` scores empty cells by simulating placements in 4 directions, with a 1.1x weight favoring AI (white) moves
- **State**: `board[15][15]`, `currentPlayer` ('black'/'white'), `history[]` for undo, `lastMove` for highlight
- **Undo**: In AI mode, undoes 2 steps (player + AI); in PvP, undoes 1 step. Resets `currentPlayer` to 'black' after undo
- **Win detection**: `checkWin()` checks 4 directions (`[0,1]`, `[1,0]`, `[1,1]`, `[1,-1]`) for 5+ consecutive same-color pieces, returns the winning line for highlighting
- **Last move highlight**: Yellow circle rendered around the most recent piece via `lastMove`
