# Workspace

## Overview

pnpm workspace monorepo using TypeScript. Each package manages its own dependencies.

## Stack

- **Monorepo tool**: pnpm workspaces
- **Node.js version**: 24
- **Package manager**: pnpm
- **TypeScript version**: 5.9
- **API framework**: Express 5
- **Database**: PostgreSQL + Drizzle ORM
- **Validation**: Zod (`zod/v4`), `drizzle-zod`
- **API codegen**: Orval (from OpenAPI spec)
- **Build**: esbuild (CJS bundle)
- **AI**: Replit AI Integrations (OpenAI gpt-5.2)

## Applications

### Kisan Saarthi AI (`artifacts/kisan-saarthi`)

Indian farmer AI assistant with:
- AI Chat in multiple Indian languages (Hindi, English, Marathi, Punjabi, Telugu, Tamil, Bengali)
- Crop information page
- Weather farming advisory
- Session-based chat history

Runs at `/` (preview path root).

## Structure

```text
artifacts-monorepo/
├── artifacts/              # Deployable applications
│   ├── api-server/         # Express API server
│   └── kisan-saarthi/      # React + Vite frontend (Kisan Saarthi AI)
├── lib/                    # Shared libraries
│   ├── api-spec/           # OpenAPI spec + Orval codegen config
│   ├── api-client-react/   # Generated React Query hooks
│   ├── api-zod/            # Generated Zod schemas from OpenAPI
│   ├── db/                 # Drizzle ORM schema + DB connection
│   ├── integrations-openai-ai-server/  # OpenAI server-side integration
│   └── integrations-openai-ai-react/   # OpenAI React hooks
├── scripts/                # Utility scripts
├── pnpm-workspace.yaml     # pnpm workspace
├── tsconfig.base.json      # Shared TS options
├── tsconfig.json           # Root TS project references
└── package.json            # Root package
```

## API Routes

- `GET /api/healthz` — Health check
- `POST /api/chat` — AI chat with farmer assistant
- `GET /api/chat/history?sessionId=...` — Chat history
- `GET /api/crops` — List of common crops with info
- `GET /api/weather?location=...` — Weather-based farming advisory

## DB Schema

- `chat_messages` — Chat history (sessionId, role, content, createdAt)
- `conversations` — OpenAI conversation sessions
- `messages` — OpenAI conversation messages

## Environment Variables

- `DATABASE_URL` — PostgreSQL connection string
- `AI_INTEGRATIONS_OPENAI_BASE_URL` — Replit AI proxy URL
- `AI_INTEGRATIONS_OPENAI_API_KEY` — Replit AI proxy key

## Development Commands

- `pnpm --filter @workspace/api-server run dev` — Run API server
- `pnpm --filter @workspace/kisan-saarthi run dev` — Run frontend
- `pnpm --filter @workspace/api-spec run codegen` — Regenerate API clients
- `pnpm --filter @workspace/db run push` — Push DB schema changes
