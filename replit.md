# BusySailing API - Replit Setup

## Project Overview
**Purpose:** Backend API server for UK Tax & Finance Advisor chatbot
**Type:** Node.js/TypeScript Express API
**Current State:** Fully configured and running on Replit

## Architecture
This is a **backend-only API** with no frontend component. It provides:
- AI chat responses (Groq Llama 3.3 70B or OpenAI GPT-4o)
- Text-to-Speech generation (OpenAI TTS)
- Analytics tracking and dashboard
- Rate limiting and session management

## Technology Stack
- **Runtime:** Node.js 20
- **Language:** TypeScript
- **Framework:** Express.js
- **Database:** PostgreSQL (Neon via Replit)
- **ORM:** Drizzle ORM
- **AI Providers:** Groq SDK, OpenAI SDK
- **WebSocket:** ws library

## Recent Changes (November 10, 2025)
- Initial import from GitHub
- Configured PostgreSQL database with Drizzle ORM
- Set up API keys for Groq and OpenAI
- Database schema pushed successfully
- Backend workflow configured on port 3000
- Server running and health endpoint verified

## Project Structure
```
.
├── index.ts              # Main Express server and CORS config
├── routes.ts             # API route handlers (chat, TTS, analytics)
├── schema.ts             # Drizzle ORM database schema
├── db.ts                 # Database connection setup
├── storage.ts            # Database query methods
├── openai.ts             # AI service integrations (Groq/OpenAI)
├── analytics.ts          # Usage tracking and analytics
├── rateLimiter.ts        # Rate limiting logic
├── drizzle.config.ts     # Drizzle ORM configuration
└── package.json          # Dependencies and scripts
```

## Environment Variables
All required secrets are configured in Replit Secrets:
- `DATABASE_URL` - PostgreSQL connection (auto-configured)
- `GROQ_API_KEY` - Groq API for chat responses
- `OPENAI_API_KEY` - OpenAI API for chat and TTS
- `ADMIN_PASSWORD` - Analytics dashboard access password

## API Endpoints

### Core Features
- `POST /api/chat` - Send chat message, get AI response
- `POST /api/tts` - Generate text-to-speech audio
- `GET /health` - Server health check

### Analytics
- `POST /api/admin/verify` - Verify admin password
- `GET /api/analytics?period={today|week|month|all}` - Get usage analytics

## Development Workflow

### Running the Server
The backend workflow automatically runs: `npm run dev`
- Server listens on port 3000 (localhost)
- Hot-reloading enabled via tsx --watch
- Logs visible in the console

### Database Management
```bash
# Push schema changes to database
npm run db:push

# Force push (if needed)
npm run db:push --force

# Open Drizzle Studio (database GUI)
npm run db:studio
```

### Important Notes
- **Database Safety:** Never manually write SQL migrations. Always use `npm run db:push` or `npm run db:push --force` to sync schema changes.
- **CORS:** Server allows requests from busysailing.com and all Replit domains (*.replit.dev, *.replit.app, *.repl.co)
- **Rate Limiting:** Chat endpoint has rate limiting by IP address
- **Port Configuration:** Backend uses port 3000 on localhost (not exposed as webview)

## AI Provider Priority
The system automatically selects AI providers in this order:
1. **Groq** (if GROQ_API_KEY is set) - Preferred for chat, faster and cheaper
2. **OpenAI** (if OPENAI_API_KEY is set) - Chat and TTS support
3. Falls back to error if no keys are configured

## User Preferences
- Backend API only, no frontend in this repository
- Uses existing project structure and conventions
- PostgreSQL database for analytics and user data
- Supports multiple AI providers with automatic fallback
