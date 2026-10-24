# Repository instructions

## Build and checks

This repository is a standalone `index.html` with no package manifest, build system, linter, or automated test runner. Open the file directly in a browser; it does not require a server or dependencies. For a manual smoke test, answer a question correctly and another incorrectly, verify score and progress updates, finish all 10 questions, then use **Volver a intentarlo** and confirm the quiz resets. There is no configured single-test command.

## Architecture

The app lives entirely in `index.html`: its inline `<style>` defines the layout, theme tokens, responsive rules, and animations; its inline `<script>` contains the question data and quiz state/rendering; the body contains the quiz and results view. Keep changes self-contained and dependency-free unless the project is intentionally being expanded.

The `questions` array is the quiz content source. Each item has a question string, four answer strings, a zero-based `correct` answer index, and a short explanatory `fact`. `renderQuestion()` updates the current prompt and progress; `chooseAnswer()` locks a response, updates score and feedback, then advances; `showResults()` and `restart()` handle completion and reset.

## Project conventions

- Keep theme colors as CSS custom properties in `:root`, and provide corresponding overrides in `@media (prefers-color-scheme: light)` so both color schemes stay consistent.
- Respect reduced-motion preferences for decorative and interaction animations via `@media (prefers-reduced-motion: reduce)`.
- Use native `<button>` elements for answer and restart actions, preserve visible `:focus-visible` styling, and keep dynamic feedback/results announced through their existing live regions.
- Add or edit quiz content in the `questions` array and keep the answer count, valid `correct` index, progress total, and displayed question count aligned.
