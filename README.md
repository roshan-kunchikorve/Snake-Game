# Snake Game

A classic Snake game built with plain HTML, CSS and JavaScript. It has a retro LCD look, levels that get faster as you score, and works with a keyboard or a touch screen. No libraries, no build step, and the whole game lives in a single file.

![HTML5](https://img.shields.io/badge/HTML5-E34F26?logo=html5&logoColor=white)
![CSS3](https://img.shields.io/badge/CSS3-1572B6?logo=css3&logoColor=white)
![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?logo=javascript&logoColor=black)
![Dependencies](https://img.shields.io/badge/dependencies-none-brightgreen)
![License: MIT](https://img.shields.io/badge/license-MIT-blue)

<!-- Add a screenshot or GIF here once you have one, then remove this comment:
![Snake game screenshot](screenshot.png)
-->

## Play it

**[Play the live demo](https://roshan-kunchikorve.github.io/snake-game/)**

Or run it on your own computer in a few seconds (see [Getting started](#getting-started)).

## Features

- Classic Snake rules: eat food to grow, and avoid the walls and your own tail
- Score, best score (saved in your browser) and level display
- Levels: a new level every 5 foods, and the snake moves faster each time
- Pause, resume and restart at any time
- Walls on or off: with walls off, the snake wraps around to the opposite edge
- Fill the whole board to win
- Keyboard controls (arrow keys or W A S D) and on-screen arrows for touch screens
- No instant U-turns: pressing keys very quickly cannot make the snake run into its own neck
- Retro LCD screen, with light and dark mode for the page around it
- Responsive: the board shrinks to fit small phone screens
- Zero dependencies, and it works offline

## How to play

- Steer the snake and eat the food (the hollow square) to grow.
- Each food gives **10 points**, and every **50 points** starts a new level.
- The game ends when the snake hits a wall (if walls are on) or its own body.
- Fill all 400 cells of the board to win.

### Controls

| Action | Keyboard | Touch screen |
| --- | --- | --- |
| Move | Arrow keys or W A S D | On-screen arrow buttons |
| Start | Space or Enter (a move key also works on the first screen) | Start button |
| Pause or resume | Space or P | Pause button |
| Restart | Enter or R | Play again button |
| Walls on or off | Walls button | Walls button |

## Getting started

No installation is needed.

```bash
git clone https://github.com/roshan-kunchikorve/snake-game.git
cd snake-game
```

Then open `index.html` in your browser by double-clicking it. That is all.

If you prefer a local server, any static server works. For example:

```bash
npx serve
```

## Customize it

Everything is in `index.html`. These are the easiest things to change:

| What to change | Where | Notes |
| --- | --- | --- |
| Starting speed | `150` in `startTimer()` | Delay between moves in milliseconds. Lower is faster. |
| Fastest speed | `60` in `startTimer()` | The delay never goes below this value. |
| Points per food | `score += 10` in `step()` | |
| Points per level | `50` in the `level = ...` line | |
| Board size | `GRID` and `CELL` | Set the canvas `width` and `height` in the HTML to `GRID × CELL`. Keep `GRID` at 12 or more. |
| Colors | CSS variables at the top of the `<style>` block | If you change `--ink`, change `INK` in the JavaScript to match. |

## How it works

The game is one small program with a few core ideas:

- **Game loop.** `setInterval` calls a `step()` function every 150 ms (less at higher levels, down to 60 ms). Each call moves the snake one cell, checks for crashes, and redraws the board.
- **The snake is an array.** Each item is a cell like `{ x: 10, y: 10 }`, and item 0 is the head. To move, the game adds a new head and removes the tail. When the snake eats, it skips the removal, so it grows by one cell.
- **Canvas drawing.** The board is a 20 × 20 grid on an HTML `<canvas>`. `draw()` clears the canvas and repaints the snake and the food on every tick.
- **Direction buffer.** The game keeps the last direction moved (`dir`) separate from the next direction requested (`nextDir`). This blocks instant U-turns, even when two keys are pressed within one tick.
- **Game states.** One `state` variable (`ready`, `running`, `paused` or `over`) decides what each key does.
- **Saved best score.** The best score is stored with `localStorage`, wrapped in `try/catch` so the game still works if the browser blocks storage.
- **Theme.** CSS variables and `prefers-color-scheme` switch the page between light and dark, while the LCD screen keeps its colors.

The code in `index.html` is split into numbered, commented sections:

- **CSS:** 1 Colors, 2 Page layout, 3 The LCD screen, 4 Buttons
- **JavaScript:** 5 Settings, 6 Game state, 7 Setting up a new game, 8 One game tick, 9 Speed, start, pause and game over, 10 Drawing, 11 Controls, 12 First screen

## Project structure

```
snake-game/
├── index.html   # the whole game: HTML, CSS and JavaScript in one file
└── README.md    # this file
```

## Roadmap

Ideas for future versions:

- [ ] Swipe controls for touch screens
- [ ] Sound effects with a mute button
- [ ] Bonus food that disappears after a few seconds
- [ ] Difficulty presets (slow, normal, fast)
- [ ] Obstacles and extra levels

## Contributing

Ideas and fixes are welcome.

1. Fork the repository
2. Create a branch: `git checkout -b feature/your-idea`
3. Commit your changes and push the branch
4. Open a pull request that describes what you changed

## License

This project is released under the [MIT License](LICENSE).

## Author

Made by [Roshan Kunchikorve](https://github.com/roshan-kunchikorve). If you like the project, a star on GitHub is always appreciated.
