# Automation, Scrapers & Data Pipelines

Workflow automation built with n8n, Python-based web scrapers, and data sync pipelines for e-commerce and market intelligence.

---

## Projects

### n8n Workflow Automations

**Stack:** n8n · Node.js · REST APIs · Webhooks

Collection of production n8n workflows automating business processes across CRM, email, Shopify, and third-party APIs.

**Key workflows:**
- Lead capture → CRM enrichment → Slack notification pipeline
- Automated follow-up email sequences triggered by deal stage changes
- Invoice generation and delivery on payment confirmation
- Daily report aggregation and delivery to stakeholders
- Error alerting and retry logic for failed webhook deliveries

---

### Elady Shopify Sync

**Stack:** Python · Shopify Admin API · PostgreSQL · Celery · Redis

Automated product and inventory synchronisation pipeline between a supplier data feed and a Shopify storefront.

**Key features:**
- Scheduled ingestion of supplier CSV/XML feeds
- Delta detection: only pushes changed products to Shopify
- Variant and metafield mapping with configurable field rules
- Image upload and CDN URL replacement
- Conflict resolution for concurrent updates
- Email alerts for sync failures or data anomalies

**Highlights:**
- Handles 10,000+ SKUs with sub-5-minute sync cycles
- Zero manual intervention required after initial setup

---

### ScraperMaster

**Stack:** Python · Selenium · BeautifulSoup · PostgreSQL · Docker

Configurable multi-target web scraping framework designed to handle JavaScript-heavy sites, pagination, and anti-bot measures.

**Key features:**
- YAML-based scraper configuration (no code changes to add new targets)
- Headless Chrome via Selenium for JS rendering
- Proxy rotation and user-agent randomisation
- Rate limiting and polite crawl delays
- Structured output to PostgreSQL or CSV
- Duplicate detection via content hash

---

### PSA Scraper

**Stack:** JavaScript · Node.js · Puppeteer

Scraper targeting PSA (Professional Sports Authenticator) card grading database to extract card grades, population reports, and auction results for market analysis.

**Key features:**
- Pagination and infinite-scroll handling
- Automatic retry on rate-limit responses
- JSON output with structured card metadata

---

### DealLens Scraper

**Stack:** Python · Playwright · PostgreSQL

Market intelligence scraper for automotive deal listings, extracting pricing, mileage, and dealer data for competitive analysis.

---

### Tickets Monitoring Bot

**Stack:** JavaScript · Node.js · Playwright

Real-time ticket availability monitor with instant notifications via Telegram/email when target events go on sale or drop in price.

---

## Tech Patterns Used

- Playwright / Puppeteer / Selenium for browser automation
- BeautifulSoup + httpx for lightweight HTML parsing
- Celery + Redis for distributed task queues
- Cron-driven scheduling (system cron + n8n built-in scheduler)
- PostgreSQL for structured storage, S3 for raw HTML archives
- Docker for portable, reproducible scraper environments

---

[← Back to Portfolio](../README.md)
