# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this is

A single-file, Thai-language React learning bootcamp (`react-bootcamp.html`). The entire app — lesson data, UI, code runner, and progress tracking — lives in one HTML file. There is no build step, no `package.json`, no tests, no lint config. React 18, ReactDOM, and `@babel/standalone` are loaded from CDN.

## Running it

Open `react-bootcamp.html` directly in a browser. No dev server is required; `file://` works because all dependencies come from CDN. Babel compiles the in-page `<script type="text/babel">` block at runtime.

## Architecture

The runtime is intentionally a teaching toy — keep this in mind before "improving" it:

- **`LESSONS` array** (around [react-bootcamp.html:393](react-bootcamp.html:393)) — the entire curriculum. Each lesson object has: `id`, `tag`, `title`, `intro`, `concepts[]`, `prompt`, `starter` (code shown in the editor), `solution`, `component` (the function name to mount), `hint`, and `check(html) => boolean` (auto-grader that inspects the rendered preview's `innerHTML`).
- **`runUserCode(code, componentName, mountEl)`** ([react-bootcamp.html:641](react-bootcamp.html:641)) — pipes the learner's code through `Babel.transform`, wraps it in `new Function("React", compiled + "\nreturn " + componentName + ";")`, and mounts the result with `ReactDOM.createRoot`. This is why lessons tell learners to type `React.useState` / `React.useEffect` instead of bare hooks — there are no imports inside the `new Function` scope.
- **`LessonCard`** ([react-bootcamp.html:657](react-bootcamp.html:657)) — per-lesson UI: editable textarea + preview ref + Run/Check/Solve/Reset/Hint buttons. `handleCheck` re-runs the code, then `setTimeout(..., 60)` waits for React to paint before reading `previewRef.current.innerHTML` and feeding it to `lesson.check`.
- **`Bootcamp`** ([react-bootcamp.html:778](react-bootcamp.html:778)) — top-level component. Tracks completed lesson IDs in state, and uses a `useEffect` to imperatively render the progress dots and completion banner into DOM nodes that live *outside* its React tree (`#progressTrack`, `#completeBanner` in the static HTML). This mixed React/DOM approach is deliberate — leave it.

## Editing conventions for this repo

- **Adding a lesson** = appending one object to `LESSONS`. The progress bar, routing-by-id, and completion logic all derive from that array; nothing else needs to change.
- **Lesson code samples are template literals.** Indentation and newlines inside `starter` / `solution` are what the learner sees in the textarea — preserve them exactly.
- **`check` functions run against `innerHTML`**, not the React tree. They use regexes like `/<h1[^>]*>/` or substring matches on rendered Thai text. Keep them lenient enough that minor styling differences still pass.
- **All learner-facing copy is in Thai.** Match the existing tone (casual, encouraging) when adding or editing lesson text. Code identifiers and concept keywords stay in English.
- **No npm / no build.** Do not introduce a bundler, package manager, or module imports — it would break the "open the file and learn" premise. The footer ([react-bootcamp.html:378](react-bootcamp.html:378)) explicitly tells learners that *graduating* to Vite is the next step beyond this file.
