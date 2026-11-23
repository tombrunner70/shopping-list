# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project

A shopping list web app that lives entirely in a single file, `index.html` (HTML, CSS and JS inline). There is no package.json, build step, linter or test suite, and the directory is not a git repository.

## Running

Open `index.html` directly in a browser. No server is needed.

## Architecture

- State is one in-memory array, `items`, of `{ id, text, done }`. It is persisted as JSON in `localStorage` under the key `shopping-list`.
- Every mutation (add, toggle, delete, clear checked) goes through `save()`, which writes to localStorage and then calls `render()`. `render()` rebuilds the whole `<ul>` from `items`, so never edit the DOM directly. Change `items` and call `save()`.
- Item text is inserted with `textContent`, not `innerHTML`. Keep it that way, since the text is user input.
- Reading from and writing to localStorage is wrapped in try/catch so the app still works when storage is unavailable or the stored JSON is corrupt.

## Skills

`.claude/skills/` holds two project skills: `auto-code-review` and `vibeindex`.
