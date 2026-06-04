# Java · Spring Boot Projects

Backend microservices and enterprise integrations built with Java and Spring Boot, covering fintech payment processing and telephony systems.

---

## Projects

### i2c Fintech Integration

**Stack:** Java 17 · Spring Boot 3 · Spring Data JPA · PostgreSQL · REST

Microservice layer integrating with the **i2c** card-management and payment processing platform. Handles card issuance, transaction authorisation hooks, balance enquiries, and webhook event processing.

**Key features:**
- REST adapter layer wrapping i2c's SOAP/REST APIs
- Event-driven transaction processing with Spring Events
- Idempotent request handling for payment webhooks
- Role-based access control with Spring Security + JWT
- Comprehensive audit logging for compliance

**Highlights:**
- Reduced integration latency by caching card-state lookups in Redis
- Full test coverage on the authorisation hook pipeline

---

### IVR (Interactive Voice Response) System

**Stack:** Java · Spring Boot · Twilio Voice SDK · PostgreSQL · Redis

Dynamic IVR telephony system that routes inbound calls through configurable menu trees, captures DTMF input, and connects callers to agents or automated flows.

**Key features:**
- TwiML-driven call flow engine with database-backed menu configuration
- DTMF input capture and intent routing
- Call recording and transcription storage
- Escalation to live agents via warm transfer
- Admin dashboard for menu tree management (no redeploy needed)
- Retry and fallback logic for failed TTS/recognition steps

**Highlights:**
- Menu trees fully configurable at runtime via REST API
- Supports multi-language prompts per caller locale

---

## Tech Patterns Used

- Layered architecture (Controller → Service → Repository)
- DTO / MapStruct mapping
- Spring Profiles for env-specific config
- Flyway database migrations
- JUnit 5 + Mockito unit and integration tests
- Docker Compose for local development

---

[← Back to Portfolio](../README.md)
