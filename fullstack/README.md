# Full-Stack Applications

End-to-end systems designed, built, and deployed across web, API, and infrastructure layers.

---

## Projects

### Employee Monitoring System

**Stack:** React · Node.js / Spring Boot · PostgreSQL · Redis · Docker

Internal productivity and attendance platform for remote and hybrid teams.

**Key features:**
- Clock-in / clock-out with GPS-aware location tagging
- Screenshot capture at configurable intervals (with employee consent)
- Active/idle time detection via mouse and keyboard event monitoring
- Project and task time allocation
- Manager dashboard: real-time team status, daily summaries, export to CSV
- Role hierarchy: Super Admin → Manager → Employee
- Email digest reports (daily/weekly) per manager

**Highlights:**
- End-to-end encryption for screenshot storage
- Audit trail for all admin actions (GDPR-ready logging)

---

### Leverr Platform (Full System)

**Stack:** C# · ASP.NET Core · TypeScript · React · Python · PostgreSQL · Redis · WebSockets

Full car-trading marketplace combining a REST API backend, real-time chat, and an agentic AI layer.

**Components:**
- **leverr-tradeup-api** (C#) — Core REST API: listings, offers, user management, deal workflow
- **leverr-chat-ui / v2** (TypeScript) — Real-time negotiation chat with AI suggestions
- **leverr-chat-server / v2** (Python) — WebSocket chat server with message persistence
- **Agentic-LeverrAPI** (Python) — LangGraph multi-agent layer for deal automation

**Key features:**
- JWT authentication with refresh-token rotation
- Offer/counter-offer state machine
- Real-time notifications via WebSockets
- AI-assisted deal summaries and negotiation tips
- Admin moderation panel

---

### RevUpChat

**Stack:** TypeScript · Python · PostgreSQL · OpenAI

Automotive-focused chat and AI assistant platform for RevUp — helping dealers manage customer conversations with AI co-pilot features.

**Key features:**
- Multi-channel inbox (web widget, SMS via Twilio)
- AI-drafted reply suggestions in the inbox UI
- Conversation tagging and CRM sync
- Dealer inventory context fed into AI responses

---

### MyCarProj

Automotive project management tool for tracking vehicle builds, parts sourcing, and service history.

---

### Career AI Platform

**Stack:** JavaScript · Node.js · React · OpenAI

Career guidance web app combining a CV analyser, job-match scoring, and an AI interview coach chatbot.

---

## Tech Patterns Used

- REST API design with OpenAPI/Swagger documentation
- JWT + refresh token auth (httpOnly cookies)
- WebSocket real-time layers (Socket.IO / native WS)
- Repository pattern with unit-of-work
- Database migrations (EF Core / Flyway / Alembic)
- CI/CD via GitHub Actions → Docker → Railway / AWS
- Environment-based config (dev / staging / prod)

---

[← Back to Portfolio](../README.md)
