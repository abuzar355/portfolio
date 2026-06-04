# AI Agents & Chatbot Systems

Conversational AI applications, multi-agent pipelines, and chatbot infrastructure built with LangChain, LangGraph, and the OpenAI API.

---

## Projects

### Northtown Auto Chatbot

**Stack:** Python · LangChain · LangGraph · OpenAI GPT-4 · FastAPI · PostgreSQL · Pinecone

AI-powered dealership assistant for Northtown Auto that helps customers search inventory, book test drives, get financing estimates, and connect with sales staff.

**Key features:**
- RAG pipeline over live inventory data (vector search via Pinecone)
- Multi-turn conversation with memory across sessions
- Intent detection: inventory search, booking, financing, escalation
- Seamless handoff to human agents with full conversation context
- Twilio SMS integration for appointment confirmations
- Admin panel to update FAQs and vehicle descriptions without redeployment

**Highlights:**
- Reduced average time-to-quote from 8 minutes (phone call) to under 90 seconds
- Context-aware follow-up questions guide users to the right vehicle faster

---

### Agentic Leverr API

**Stack:** Python · LangGraph · OpenAI · FastAPI · PostgreSQL

Multi-agent orchestration layer sitting atop the Leverr car-trading API. Agents handle deal discovery, price negotiation suggestions, and automated outreach drafting.

**Key features:**
- LangGraph state machine orchestrating Researcher, Negotiator, and Writer agents
- Tool-calling agents with access to Leverr REST API endpoints
- Structured output validation with Pydantic
- Async task queue for long-running agent runs (Celery + Redis)
- Streaming intermediate steps to frontend via Server-Sent Events

---

### Chatbot SDK

**Stack:** Python · FastAPI · WebSockets · Redis

Reusable SDK and server infrastructure for deploying AI chatbots across multiple clients. Provides a standardised interface over different LLM backends.

**Key features:**
- Provider-agnostic LLM interface (OpenAI, Anthropic, local models)
- Session and conversation history management in Redis
- Plugin system for custom tools (web search, calendar, CRM lookup)
- REST + WebSocket transport layers
- Rate limiting and usage tracking per client API key

---

### CarirerAI Chatbot

**Stack:** JavaScript · Node.js · OpenAI API

Career guidance chatbot that helps users with CV review, job matching advice, and interview preparation tips.

---

## Tech Patterns Used

- LangGraph for stateful, cyclical agent workflows
- RAG: document ingestion → chunking → embedding → vector store → retrieval
- Structured tool use with OpenAI function calling
- Async Python (asyncio + FastAPI)
- Pydantic for data validation at agent boundaries
- Docker + Railway for deployment

---

[← Back to Portfolio](../README.md)
