# Guest App — Hotel Guest Experience Platform

Full-stack hospitality platform built for hotels, consisting of three components: a Flutter mobile app for guests, a Java/Spring Boot backend server, and a React/TypeScript admin dashboard for hotel staff.

> **Organisation:** [Guest-App](https://github.com/Guest-App)

---

## System Overview

```
┌─────────────────────┐     WebSocket (STOMP)    ┌──────────────────────┐
│  Guest-Mobile        │ ◄──────────────────────► │  server               │
│  Flutter (iOS/Android)│     REST API (JWT)       │  Spring Boot + PG     │
└─────────────────────┘                           └──────────┬───────────┘
                                                             │  REST + WS
┌─────────────────────┐                           ┌──────────▼───────────┐
│  admin-dashboard     │ ◄──────────────────────► │  Nginx Proxy          │
│  React + TypeScript  │     REST + STOMP          │  GCP (34.87.7.190)    │
└─────────────────────┘                           └──────────────────────┘
```

Guests authenticate with a randomly generated password and receive a JWT token used for all subsequent requests. Staff manage the platform through the admin dashboard in real time.

---

## Repo 1 — `Guest-App/server` (Java · Spring Boot)

**Stack:** Java 8 · Spring Boot 2.2.7 · Spring Data JPA · Spring WebSocket · PostgreSQL · Flyway · Firebase Admin · Google Cloud Storage · Google Maps · Nginx · Docker

### Features

**Authentication**
- JWT-based session tokens (`x-token` header)
- Auto-generated guest passwords — no registration flow needed
- Permission-based access control per guest account

**Real-Time Chat (WebSocket over STOMP)**
- Each guest has a dedicated `conversationId` channel (`/topic/{conversationId}`)
- Messages persist to PostgreSQL with `SENT → SEEN → ERROR` status lifecycle
- Staff and guest messages distinguished by `ChatAuthorType`
- System status broadcasts on the same topic channel (`isSystemStatus: true`)
- Mark-as-seen endpoint for bulk message acknowledgement

**Dynamic Prompt System**
- Admins build custom UI screens (prompts) with a drag-and-drop editor
- Prompt elements: `CAROUSEL`, `BUTTON`, `TEXT`, `RECTANGLE` — each with full CSS-like positioning (top, left, width, height, layer, opacity, rotation)
- Prompts are scheduled via cron expressions per `PromptOption`
- Guests fetch active prompts for a given date; clicks are tracked as `hit_prompt` analytics events
- Hotspot feature: BLE beacon triggers prompt display locally on device; a `PromptNotificationLog` is sent back to server for performance analytics

**Express Service Requests**
- Housekeeping: schedule or cancel with date/time
- Taxi: multi-passenger booking with luggage count, departure time, pickup address
- Wake-up call: time-based scheduling
- Laundry pickup: `URGENT | NORMAL | IRON_ONLY` options
- Fresh towels / Bathrobes: quick one-tap requests
- Engineering / Technical service: one-tap request
- Electric adapters & phone chargers: browse catalogue → order by quantity
- Newspapers & flowers: catalogue browse + order

**Food & Dining**
- Food catalogue by type: `APPETIZER`, `MAIN_COURSE`, `SIDE`, `DESSERT`, `BEVERAGE`, `NON_ALCOHOLIC_BEVERAGE`, `MISCELLANEOUS`
- Snacks: `ICE_CREAM`, `CHOCOLATE`, `SNACK`
- Dining places: list restaurants, view menus, reserve tables
- In-room dining order submission

**Luxury & Business Services**
- Hierarchical luxury catalogue: Feature → Option → Item with pricing
- Business services: three-level hierarchy (option → sub-option → item)
- Cart checkout endpoint (`POST /api/buy`) combining food, luxury items, business services, and prompt orders in one transaction

**Hotel Information**
- Useful info pages (title + detail + photo)
- Attractive places / local area guides

**Health Check & Presence**
- Mobile app pings `POST /api/guest/health_check` every 5 minutes
- Updates `lastSeenTimestamp`; guests inactive for >5 min marked offline
- Accepts `firebaseClientId` for push notification targeting
- Accepts `timezone` for locale-aware scheduling

**Push Notifications**
- Firebase Admin SDK for FCM push delivery
- Payload carries `prompt_id` (standard) or `preps_prompt_id` (emergency)

**Integrations**
- Google Cloud Storage for media file hosting
- Google Maps Services for location features
- Apache POI for Excel/ODS report export
- Retrofit2 for outbound HTTP calls to third-party services

### Tech Details
- Lombok + MapStruct for clean entity/DTO mapping
- springdoc OpenAPI UI for live API documentation
- Flyway for versioned database migrations
- Docker Compose + Nginx reverse proxy for deployment on GCP
- Logback structured logging

---

## Repo 2 — `Guest-App/Guest-Mobile` (Flutter · Dart)

**Stack:** Flutter · Dart · STOMP · Firebase · BLE Beacons · SQLite (sqflite) · Hive · Provider · Geolocator

### Features

- **Authentication:** Password login screen → JWT stored in `shared_preferences` for session persistence
- **Real-time chat:** `stomp_dart_client` connects to Spring Boot WebSocket server; subscribes to `/topic/{conversationId}` for incoming messages; sends to `/app/{conversationId}`
- **Push notifications:** Firebase Messaging (`firebase_messaging` + `firebase_core`) for FCM; local notifications via `flutter_local_notifications`
- **BLE hotspot:** `beacons_plugin` detects proximity beacons — triggers local prompt display and logs event to server
- **Dynamic prompt rendering:** Fetches prompt elements from server and renders them as an overlay with carousel backgrounds, positioned buttons, and text blocks
- **Express services:** Full UI for housekeeping, taxi, laundry, room service, adapters, wake-up call, and all catalogue-based services
- **Dining & food ordering:** Browse dining venues, view menus, add to cart, submit order
- **Buying/cart screen:** Slider-confirm purchase UI; order history; add notes
- **Video content:** `chewie` + `video_player` for promotional video playback
- **Location:** `geolocator` + `geocoder2` for taxi pickup address resolution
- **Offline support:** `hive` + `sqflite` for local caching of catalogue data
- **Navigation:** `fluro` router for named routes
- **State management:** `provider`
- **Internationalisation:** `flutter_localizations` for multi-language support
- **Platforms:** Android (Gradle) + iOS

### App Screens (from assets)
Login · Home · Chat · Express Requests · Housekeeping · Laundry · Taxi · Wake-Up Call · Fresh Towels · Bathrobes · Electric Adapter · Phone Charger · Technical Assistance · Dining · Food Menu · Snacks · Ice Cream · Luxury Services · Business Services · Buying/Cart · Order History · Useful Hotel Info · Concierge · Places to Go · Hotel Facilities · Your Specials (Prompts)

---

## Repo 3 — `Guest-App/admin-dashboard` (React · TypeScript)

**Stack:** React 16 · TypeScript · Redux · Redux-Saga · Next.js 9 · Ant Design · D3.js · StompJS · react-intl · Webpack

### Features

- **Guest management:** View all guests, online/offline status (via `lastSeenTimestamp`), account activation
- **Real-time staff chat:** StompJS WebSocket connection mirrors guest chat; staff reply from dashboard inbox
- **Prompt builder:** Drag-and-drop UI editor to compose prompt screens — set element type (carousel, button, text, rectangle), position, size, font, colour, opacity, layer, and cron schedule; `react-image-crop` for image assets; `react-color` for colour picker
- **Service request management:** View and action incoming express requests (housekeeping, taxi, laundry, etc.) in real time
- **Menu & catalogue management:** CRUD for food items, dining venues, luxury items, business services, adapters, newspapers
- **Analytics & reporting:** D3.js charts for prompt performance (hit rates, click-through); guest activity reports; Excel/ODS export (via server API)
- **Push notification sender:** Target individual guests or broadcast; choose prompt payload
- **Internationalisation:** `react-intl` for multi-locale staff UI
- **Custom CSS tooling:** `tools/css_compiler.js` — bespoke CSS pre-processor run at build time
- **Polling:** `react-polling` for live data refresh on dashboards without full WebSocket overhead

---

## Deployment

```
GCP VM  →  Nginx (reverse proxy)  →  Spring Boot (port 9888)
                                  →  React Admin Dashboard (static)
PostgreSQL  (managed / Docker)
Google Cloud Storage  (media assets)
Firebase  (push notifications)
```

- `docker-compose.yaml` in server repo orchestrates app + PostgreSQL
- Flyway runs migrations on startup
- Nginx config in `deployment/` folder

---

[← Back to Portfolio](../README.md)
