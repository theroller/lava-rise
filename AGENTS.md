# Lava Rise — AI Conventions

Inherits from `../../AGENTS.md` and `../AGENTS.md` (Ford-specific rules).

## Game Overview

Side-scrolling stick-fighter survival. Lava rises. Two players on one iPad fight each other while climbing to survive. Canvas + vanilla JS, single `index.html`, no build step.

## Architecture

- **Single file:** all game logic in `index.html` — no imports, no modules
- **Rendering:** Canvas 2D API, `requestAnimationFrame` loop
- **Input:** Touch events on HTML buttons overlaid on canvas; keyboard fallback for desktop testing
- **State machine:** `title` → `playing` → `gameover` → (restart) `playing`

## Ford-Specific Rules

- Zero typing. All interaction is tap/button.
- Buttons must be 65px minimum tap targets.
- Visual feedback on every action: flashes, color changes, screen shake.
- Labels use icons + color, not text the player must read.
- No multi-step menus — max one tap from any screen to playing.

## Code Style

- Global `input` object holds button state; players read from it directly.
- `setupLevel()` resets all state; call it on every new game.
- Keep platform layout in a named array; don't hardcode positions inline.
- Lava speed formula: `BASE_SPEED + frame * ACCELERATION`. Tune these constants, don't add complexity.
- Drawing functions are pure: `draw*(thing, ctx)` — no side effects.

## What Not to Do

- No external libraries, CDNs, or build tools.
- No keyboard-only features (must have touch equivalent).
- Don't add features mid-session without noting them in session-log.md.
