# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project

A shopping list web app that lives entirely in a single file, `index.html` (HTML, CSS and JS inline). There is no package.json, build step, linter or test suite.

## Running

Open `index.html` directly in a browser. No server is needed, but network access to Supabase is.

## Architecture

- State is one in-memory array, `items`, of `{ id, text, done }`, mirrored from the Supabase table `shopping_items` (project `gwseozgjfuvspqioudpc`) via the PostgREST API with `fetch`. The publishable key in the file is intentionally public; RLS policies grant the `anon` role access.
- Every mutation (add, toggle, delete, clear checked) goes through `save(mutation)`, which runs the API call, reloads `items` from the database and then calls `render()`. `render()` rebuilds the whole `<ul>` from `items`, so never edit the DOM directly. Pass the API call to `save()`.
- Item text is inserted with `textContent`, not `innerHTML`. Keep it that way, since the text is user input.
- Network failures are caught in `save()` and shown in the `#error` element.

## Skills

`.claude/skills/` holds two project skills: `auto-code-review` and `vibeindex`.
