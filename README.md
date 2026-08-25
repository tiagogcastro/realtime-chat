# realtime-chat

![TypeScript](https://img.shields.io/badge/TypeScript-4.x-3178C6?logo=typescript&logoColor=white)
![Express](https://img.shields.io/badge/Express-4-000000?logo=express&logoColor=white)
![Socket.IO](https://img.shields.io/badge/Socket.IO-4-010101?logo=socketdotio&logoColor=white)
![TypeORM](https://img.shields.io/badge/TypeORM-0.2-FE0803?logo=typeorm&logoColor=white)
![SQLite](https://img.shields.io/badge/SQLite-003B57?logo=sqlite&logoColor=white)

Real-time customer support chat built during [Rocketseat NLW #5](https://rocketseat.com.br)
(April 2021). The backend exposes a REST API and a WebSocket layer; users open
a support session from a lightweight vanilla JavaScript client and every message
is persisted to SQLite via TypeORM.

## Features

- Support session start by email (`client_first_access` socket event): creates or reuses the user and binds their Socket.IO connection
- Message persistence per user
- Admin settings entity with per-username chat configuration (create / read / update via REST)
- TypeORM migrations for all entities (settings, users, messages, connections)

## Tech stack

| Layer | Tools |
|---|---|
| Language | TypeScript |
| HTTP | Express |
| Realtime | Socket.IO 4 |
| ORM / DB | TypeORM + SQLite |
| Dev server | ts-node-dev, EJS for HTML views |

## How to run

```bash
# requirements: Node.js 14-16 era runtime (see legacy note)
yarn install

# run migrations
yarn typeorm migration:run

# start dev server on http://localhost:3333
yarn dev
```

Open the client page at <http://localhost:3333/pages/client>.

## REST endpoints

| Method | Route | Purpose |
|---|---|---|
| POST | `/settings` | Create chat settings |
| GET | `/settings/:username` | Get settings by username |
| PUT | `/settings/:username` | Update settings |
| POST | `/users` | Create user |
| POST | `/messages` | Create message |
| GET | `/messages/:id` | List messages by user id |

## WebSocket events

| Event | Direction | Payload |
|---|---|---|
| `client_first_access` | client -> server | `{ text, email }` |

## Legacy note

Educational project from April 2021. Dependencies are pinned to that era
(TypeScript 4.2, TypeORM 0.2, Node 14-16 runtimes); expect friction on current
Node versions without upgrades. Scope is limited to the client side of the
chat flow; the admin dashboard was not implemented. Estimated modernization
effort if picked up later: small (half-day), bump dependencies to current
majors, replace SQLite config paths, and finish the admin socket handlers.
No fixes are planned as part of this cleanup phase.

## Author

Built by [Tiago Gonçalves de Castro](https://github.com/tiagogcastro)
· [LinkedIn](https://www.linkedin.com/in/tiagogcastro)

## License

[MIT](LICENSE)
