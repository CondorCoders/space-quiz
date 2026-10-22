# Orbit space quiz

## Running and validation

Open `index.html` directly in a browser using a `file://` URL. Keep the app
self-contained: no server, package installation, build step, external assets,
or runtime dependencies.

Validation is browser-based; there is no checked-in automated test or lint
runner. For a focused single-question check, reload the page and answer Mars
with B: the score should become 1, the correct answer should turn green, the
explanation should appear, and progress should become 1/10. Repeated answers
must not add points. Advance and choose A on question 2 to check incorrect
feedback: the score stays 1, the selected answer shakes red, and Neil Armstrong
is revealed as correct.

For a full smoke test, complete mixed, perfect, and zero-score runs. Verify
results, accuracy, emoji reactions, full progress, and replay reset. Exercise
actual Tab/Shift+Tab and Enter/Space navigation as well as A-D shortcuts.
Dispatched JavaScript keyboard events check shortcut handlers, not native
browser keyboard navigation.

Check narrow layouts, both `prefers-color-scheme` settings, and
`prefers-reduced-motion`. Wait for the 0.2-second answer background transition
before asserting its final computed color.

## Architecture and state

`index.html` contains the CSS, semantic page structure, inline SVG artwork,
question data, and plain JavaScript. The script runs after the markup; `$` is
a local `document.querySelector` shorthand, not a library.

The quiz uses an ordered `questions` array and three in-memory state variables:
`current` (zero-based question index), `score`, and `answered`. Each question
has `category`, `question`, four `answers`, a zero-based `correct` index, and
an explanatory `fact`.

- `renderQuestion()` rebuilds answer buttons, clears feedback, disables Next,
  and optionally focuses the question heading.
- `chooseAnswer()` is the shared click/shortcut path. It locks all answers,
  awards at most one point, reveals the correct answer and explanation,
  updates completed-question progress, and focuses Next.
- Next advances only after an answer; the last question opens `showResults()`.
  Results replace the quiz within the same card using `hidden`.
- Replay resets all three state variables, score display, and progress before
  rendering the first question. Reloading also starts a fresh quiz.

Progress counts answered questions, not the displayed question number.
Results use score bands of 8-10, 5-7, and 0-4. The design is explicitly a
10-question quiz: changing its length also requires updating static totals,
the progress ARIA maximum, briefing copy, completion label, and score bands.

## UI conventions

Keep the centered 510px maximum content column, sans-serif body, orange accent,
and mission-control intro. Monospace labels are scoped to mission metadata.
The mobile overrides begin at 540px.

Light colors are defined in `:root`; dark overrides live in
`prefers-color-scheme: dark`. Reuse the surface, border, text, feedback, and
star custom properties; intro-specific colors use scoped `--console-*`
properties with their own dark overrides.

The star field is a decorative, non-interactive `body::before` layer behind
content, using body isolation and `pointer-events: none`. Its brief animation
is enabled only under `prefers-reduced-motion: no-preference`. The reduced
motion rule disables animations and transitions for elements and pseudo-elements.

Preserve native answer buttons, visible focus indicators, the answer group's
heading association, the progress bar's ARIA value, and polite status feedback.
Correctness is communicated with text, symbols, and answer labels as well as
green/red colors. Decorative SVGs and symbols are hidden from assistive technology.

Question and result headings use `tabindex="-1"` for programmatic focus.
Keyboard shortcuts accept A-D case-insensitively and ignore Alt/Ctrl/Meta,
repeated keydown events, answered questions, and the results screen.
Use DOM creation and `textContent` for question, answer, and explanation text;
existing `innerHTML` assignments are limited to controlled UI templates.
