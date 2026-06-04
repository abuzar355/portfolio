# React · Next.js Projects

Production frontend applications built with React and Next.js, ranging from SaaS platforms to real-time chat interfaces.

---

## Projects

### QFinishes — Construction Management SaaS

**Stack:** Next.js 14 · TypeScript · Tailwind CSS · React Query · REST API

Web application for managing construction finishing projects — scheduling, contractor assignments, task tracking, and client reporting.

**Key features:**
- Project dashboard with Gantt-style schedule view
- Contractor onboarding and work-order assignment flows
- Real-time status updates via polling + optimistic UI
- Client-facing progress portal with photo uploads
- Role-based views: Admin, Contractor, Client
- PDF report generation for project milestones

**Highlights:**
- Server Components (Next.js App Router) for fast initial loads
- Tailwind + shadcn/ui design system for consistent UI

---

### Leverr Chat UI (v1 & v2)

**Stack:** TypeScript · React · WebSockets · Tailwind CSS

Real-time chat interface for the Leverr car-trading platform, allowing buyers and sellers to negotiate deals with AI-assisted suggestions.

**Key features:**
- WebSocket-based real-time messaging
- Message threading and read receipts
- AI response suggestions inline in chat
- Mobile-first responsive layout
- v2 rewrite: improved state management with Zustand, virtualized message lists for performance

---

### Carrier Connect Bot UI

**Stack:** TypeScript · React · Vite · Tailwind CSS

Conversational chat widget for a logistics carrier-matching AI assistant. Embedded as a standalone React app.

**Key features:**
- Embeddable chat widget (iframe + postMessage API)
- Streaming AI response rendering (token-by-token)
- Session persistence across page reloads
- Configurable branding via props

---

### Portfolio Business Website

**Stack:** TypeScript · Next.js · Tailwind CSS

Professional business portfolio site with animated sections, project showcases, and contact form integration.

---

## Tech Patterns Used

- Next.js App Router with Server & Client Components
- TypeScript strict mode throughout
- React Query / SWR for server-state management
- Zustand for client-state
- Tailwind CSS + component libraries (shadcn/ui, Radix UI)
- ESLint + Prettier + Husky pre-commit hooks
- Vercel deployments with preview environments

---

[← Back to Portfolio](../README.md)
