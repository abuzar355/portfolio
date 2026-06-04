# Java · Spring Boot Projects

Backend microservices and enterprise integrations built with Java and Spring Boot, covering fintech payment processing, telephony systems, ACH transfers, and automotive finance tooling.

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

### ACH & Direct Deposit Payment Service

**Stack:** Java 17 · Spring Boot 3 · Spring Batch · PostgreSQL · RabbitMQ · Nacha (ACH) · REST

Microservice handling ACH (Automated Clearing House) origination and direct deposit disbursements, compliant with Nacha operating rules. Supports both PPD (Personal) and CCD (Corporate) entry classes.

**Key features:**
- ACH file generation in Nacha IAT/PPD/CCD format with strict field-length and checksum validation
- Direct deposit scheduling: one-time and recurring disbursements with configurable settlement windows
- Debit and credit origination: payroll direct deposit, vendor payments, refunds
- Return and NOC (Notification of Change) handling — automatically updates stale account/routing data
- Prenote workflow: zero-dollar test transactions before first live transfer
- Dual-approval workflow for high-value transfers (configurable threshold)
- Spring Batch for bulk file processing: ingests payment instruction CSVs, validates, generates ACH output
- RabbitMQ for async settlement status updates back to calling services
- Idempotency keys on all transfer creation endpoints to prevent duplicate origination
- Full audit trail: initiated → submitted → settled / returned / rejected lifecycle
- Webhook callbacks to upstream services on settlement confirmation or return

**Highlights:**
- Processes payroll batches of 5,000+ entries in under 30 seconds via Spring Batch parallelism
- Return rate tracking dashboard with automated alerts when return rate approaches Nacha thresholds
- Encrypted storage of bank account numbers (AES-256) with tokenisation for repeat transfers

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

### Lease & Finance Calculator Service

**Stack:** Java 17 · Spring Boot 3 · Spring Data JPA · PostgreSQL · Redis · REST

Financial calculation microservice for automotive dealerships, powering real-time lease and loan payment estimates. Consumed by dealer portals, customer-facing web apps, and the IVR system.

**Key features:**

**Finance (Loan) Calculator:**
- Monthly payment calculation using standard amortisation formula with configurable compounding
- APR and effective interest rate disclosure in line with Regulation Z (Truth in Lending Act)
- Down payment, trade-in value, and negative equity handling
- Multi-tier credit scoring: rate tables per credit band (Tier 1–6) loaded from DB, cacheable in Redis
- Extended warranty and GAP insurance add-on pricing rolled into monthly payment
- Balloon payment / deferred payment option modelling
- Amortisation schedule generation (full term breakdown of principal vs. interest per period)

**Lease Calculator:**
- Residual value computation from configurable mileage/term depreciation tables (per make/model/trim)
- Money factor (MF) to APR conversion and disclosure
- Capitalised cost reduction (cap cost reduction) with and without incentives
- Acquisition fee, disposition fee, and excess mileage charge modelling
- Multiple security deposit (MSD) optimisation: calculates optimal MSD count to reduce money factor
- Gap liability estimation between payoff amount and residual at any point in term
- Lease-vs-buy comparison report: total cost of ownership over equivalent ownership periods

**API & Integration:**
- REST endpoints: `/api/v1/finance/calculate`, `/api/v1/lease/calculate`, `/api/v1/compare`
- Request/response DTOs with full OpenAPI 3 documentation
- Redis caching of rate tables and residual grids (TTL-based invalidation when rates change)
- Audit log of every calculation with input parameters stored for compliance review
- Webhook support for pushing updated rate sheets from lender integrations

**Highlights:**
- Sub-10ms p99 response time on calculate endpoints thanks to Redis-cached rate/residual tables
- Supports multi-lender scenarios: dealer can compare payments across 3 captive lenders simultaneously
- Calculation engine fully unit-tested against known amortisation and lease payment references

---

## Tech Patterns Used

- Layered architecture (Controller → Service → Repository)
- DTO / MapStruct mapping
- Spring Profiles for env-specific config
- Flyway database migrations
- Spring Batch for bulk payment file processing
- RabbitMQ for async event publishing
- Redis for rate/residual table caching
- AES-256 encryption for sensitive financial data
- JUnit 5 + Mockito unit and integration tests
- Docker Compose for local development

---

[← Back to Portfolio](../README.md)
