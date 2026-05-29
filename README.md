# React Bootcamp (Thai)

A single-file, browser-only React learning playground with lessons written in **Thai**. Open the HTML file and start learning — no install, no build step, no server.

## Try it

Just open [`react-bootcamp.html`](react-bootcamp.html) in any modern browser (Chrome or Firefox recommended). Everything runs from `file://` — React, ReactDOM, and Babel are loaded from CDN, and your code is compiled in the browser.

## What's inside

- Bite-sized React lessons covering JSX, components, props, state, effects, lists, forms, and small projects.
- An in-page code editor with **Run / Check / Solve / Reset / Hint** buttons for each lesson.
- An auto-grader (`check(html)`) that inspects the rendered preview to confirm each lesson passes.
- A progress bar across all lessons and a completion banner at the end.

## Project layout

```
react-bootcamp.html   # The entire app — lessons, UI, code runner, grader
CLAUDE.md             # Notes for AI assistants working on this repo
README.md             # You are here
```

Everything — curriculum data, UI components, and the runtime — lives in one HTML file on purpose. The goal is "open the file and learn." Graduating to a real toolchain (Vite + npm) is suggested as the next step *after* finishing the bootcamp.

## Tech

- React 18 (via CDN)
- ReactDOM 18 (via CDN)
- Babel Standalone (compiles `<script type="text/babel">` in the browser)
- Plain HTML + CSS, no framework

## Adding a lesson

Append one object to the `LESSONS` array inside `react-bootcamp.html`. Each lesson has:

| Field | Purpose |
|---|---|
| `id`, `tag`, `title` | Identity and label |
| `intro`, `concepts[]` | Teaching copy (Thai) |
| `prompt`, `hint` | Task description and a hint |
| `starter`, `solution` | Code shown in the editor and the reference answer |
| `component` | Function name to mount as the preview |
| `check(html)` | Auto-grader that reads the rendered `innerHTML` |

The progress bar, lesson routing, and completion logic all derive from `LESSONS` — no other changes needed.

## License

Personal learning project. Use freely.
