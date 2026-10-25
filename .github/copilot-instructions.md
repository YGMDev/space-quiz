# Copilot instructions

## Run and verify

- This is a dependency-free static page. Open `index.html` directly in a browser; no build or server is required.
- There are no configured build, lint, or automated test commands. For a focused manual check, answer a question correctly and incorrectly, confirm only correct answers increase the score, advance through all 10 questions, verify the results, and restart.

## Architecture

- The app lives in `index.html`: semantic page markup, all styling in an inline `<style>`, and quiz logic/data in an inline `<script>`. Keep it self-contained unless the project intentionally adopts a multi-file structure.
- The `questions` array is the source of truth for question text, answer choices, correct-answer index, and feedback fact. `renderQuestion()` paints the current item; `chooseAnswer()` locks the choices and updates feedback/score; `showResults()` presents the final score and reaction; `restartQuiz()` resets state.
- Quiz progress and score are in-memory state only. There is no persistence or external service.

## Project conventions

- Keep theme colors in CSS custom properties under `:root` and override them in `@media (prefers-color-scheme: dark)`. New interface colors should work in both themes.
- Preserve semantic buttons for choices/actions, the labeled progress bar and its changing `aria-valuenow`, and the live regions used for score, feedback, and results. When replacing question content, preserve the focus handoff to the first answer; after choosing, focus the next action.
- Respect `prefers-reduced-motion`; quiz feedback and transitions should not rely on animation alone to communicate correctness.
- Update quiz content in the `questions` array and keep its `correct` value as a zero-based index into that question's `answers`.
