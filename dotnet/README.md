# .NET · ASP.NET Core Projects

REST APIs and backend services built with C# and ASP.NET Core, covering automotive data platforms and fintech trading systems.

---

## Projects

### CarAPI

**Stack:** C# · ASP.NET Core 8 · Entity Framework Core · PostgreSQL · Docker

RESTful API for automotive data — vehicle listings, specifications, pricing, and dealer information.

**Key features:**
- CRUD endpoints for vehicles, dealers, and enquiries
- Advanced filtering: make, model, year, price range, mileage, fuel type
- Pagination and cursor-based navigation for large result sets
- JWT authentication with role-based authorisation (Admin, Dealer, Public)
- EF Core with code-first migrations
- Swagger / OpenAPI documentation
- Docker Compose setup for local dev

---

### CarAPI-Enhanced

**Stack:** C# · ASP.NET Core 8 · EF Core · PostgreSQL · Redis · MediatR

Performance and feature-enhanced evolution of CarAPI, introducing CQRS patterns, caching, and a richer domain model.

**Key improvements over CarAPI:**
- CQRS via MediatR: commands and queries cleanly separated
- Redis caching layer for frequently accessed listing data
- Background job processing with Hangfire (e.g. nightly price-index refresh)
- Outbox pattern for reliable domain event publishing
- FluentValidation for request validation
- Structured logging with Serilog → Seq
- Integration tests with Testcontainers (real PostgreSQL in CI)

**Highlights:**
- p95 response time on listing search dropped from ~320ms to ~45ms after Redis layer
- Clean Architecture folder structure (Domain / Application / Infrastructure / API)

---

### Leverr TradeUp API

**Stack:** C# · ASP.NET Core · Entity Framework Core · PostgreSQL · SignalR

Core backend for the Leverr car-trading marketplace. Manages the full lifecycle of a vehicle deal from listing to completion.

**Key features:**
- Vehicle listing management with rich media support
- Offer / counter-offer state machine with event history
- User accounts: buyers, sellers, dealers
- SignalR hub for real-time deal status updates
- Payment intent integration (Stripe)
- Soft-delete and audit columns on all domain entities
- Rate limiting on public-facing endpoints

**Highlights:**
- Deal state machine enforces valid transitions only — no invalid state corruption
- Idempotency keys on payment endpoints prevent double-charges

---

## Tech Patterns Used

- Clean Architecture (Domain · Application · Infrastructure · API layers)
- CQRS + MediatR
- Repository + Unit of Work
- EF Core code-first migrations
- FluentValidation for input validation
- Serilog structured logging
- xUnit + Moq unit tests; Testcontainers for integration tests
- GitHub Actions CI: build → test → Docker build → push

---

[← Back to Portfolio](../README.md)
