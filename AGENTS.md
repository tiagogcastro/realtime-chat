# AGENTS.md

Guidance for AI coding agents working in this repository.

## Project

Real-time customer support chat built during Rocketseat NLW #5 (April 2021).
Express + Socket.IO REST/WebSocket API serving a vanilla JavaScript client page.
Legacy educational project: dependencies are pinned to 2021-era versions.

## Commands

- Install: `yarn install`
- Migrations: `yarn typeorm migration:run`
- Dev server: `yarn dev` (http://localhost:3333)
- Client page: http://localhost:3333/pages/client

## Structure

- `src/server.ts`: entry point, port 3333
- `src/http.ts`: Express app + Socket.IO server wiring, serves `public/`
- `src/routes.ts`: REST routes (settings CRUD by username, users create, messages create/list)
- `src/controllers`, `src/services`, `src/repositories`: layered per feature
- `src/entities`: TypeORM entities (Setting, User, Message, Connection)
- `src/database/migrations`: TypeORM migrations
- `src/websocket/client.ts`: handles `client_first_access` socket event
- `src/websocket/admin.ts`: intentionally empty, admin dashboard was never implemented
- `public/html/client.html`, `public/js/chat.js`: vanilla JS client

## Rules for agents

- Docs-only maintenance phase: do not upgrade dependencies or change runtime behavior
- SQLite database files are gitignored; never commit `*.sqlite`
