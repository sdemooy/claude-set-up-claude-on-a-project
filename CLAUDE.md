# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

Starter Express API for the Claude Code course. A minimal REST API with in-memory data, used as a real codebase to configure Claude Code against (not to build out further, per the course task).

## Commands

- `npm install` — install dependencies
- `npm run dev` — start the API with auto-reload on http://localhost:3000
- `npm start` — start the API without auto-reload
- `npm test` — run all tests (Node's built-in test runner)
- `npm run lint` — run ESLint

Run a single test file: `node --test tests/users.test.js`

## Architecture

- `server.js` — entry point; builds the Express app and mounts routes. Exports `app` without calling `listen()` when required (not run directly), so tests can import it via supertest without opening a real port.
- `routes/` — one file per resource (`users.js`, `health.js`), each an `express.Router()`.
- `db/store.js` — in-memory data access layer; no persistence, resets on restart.
- `tests/` — uses `node:test` + `node:assert` + `supertest` against the exported `app`.

## Conventions

- Route handlers validate input and return JSON error bodies (`{ error: "..." }`) with the appropriate status code (400, 404) rather than throwing.
- Data access always goes through `db/store.js`, never direct array manipulation in route files.
