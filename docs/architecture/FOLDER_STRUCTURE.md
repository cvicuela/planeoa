# PlaneOA — Monorepo Folder Architecture

## Root Structure

```
planeoa/
├── .github/                    # GitHub CI/CD, templates
│   ├── workflows/              # GitHub Actions (CI, deploy, preview)
│   ├── ISSUE_TEMPLATE/
│   └── PULL_REQUEST_TEMPLATE/
│
├── apps/                       # All deployable applications
│   ├── web/                    # Landing + Platform (Next.js)
│   ├── admin/                  # Admin Dashboard (Next.js)
│   ├── mobile/                 # Mobile App (Expo / React Native)
│   └── api/                    # Backend API (Node.js + Express/Fastify)
│
├── packages/                   # Shared packages across apps
│   ├── config/                 # Shared configs (ESLint, TS, Tailwind)
│   ├── shared/                 # Business logic, types, validators
│   └── ui/                     # Shared UI component library
│
├── infrastructure/             # DevOps & deployment configs
│   ├── docker/
│   ├── nginx/
│   └── scripts/
│
├── docs/                       # Project documentation
│   ├── architecture/
│   ├── api/
│   └── guides/
│
├── package.json                # Root workspace config
├── turbo.json                  # Turborepo pipeline config
├── .env.example                # Environment variable template
└── README.md
```

---

## apps/web/ — Landing Website + User Platform (Next.js App Router)

```
apps/web/
├── public/
│   ├── images/
│   └── fonts/
├── src/
│   ├── app/
│   │   ├── (marketing)/            # Public-facing landing pages
│   │   │   ├── home/
│   │   │   ├── about/
│   │   │   ├── pricing/
│   │   │   ├── contact/
│   │   │   └── blog/
│   │   │       └── [slug]/
│   │   │
│   │   ├── (auth)/                 # Authentication flows
│   │   │   ├── login/
│   │   │   ├── register/
│   │   │   │   ├── organizer/      # Multi-role registration
│   │   │   │   ├── talent/
│   │   │   │   ├── venue/
│   │   │   │   └── supplier/
│   │   │   ├── forgot-password/
│   │   │   ├── reset-password/
│   │   │   └── verify-email/
│   │   │
│   │   ├── (platform)/             # Authenticated platform
│   │   │   ├── dashboard/
│   │   │   ├── explore/
│   │   │   │   ├── talents/        # Browse & search talents
│   │   │   │   │   └── [id]/
│   │   │   │   ├── spaces/         # Browse & search venues
│   │   │   │   │   └── [id]/
│   │   │   │   ├── equipment/      # Browse & search equipment
│   │   │   │   │   └── [id]/
│   │   │   │   └── media/          # Advertising inventory
│   │   │   │       └── [id]/
│   │   │   ├── bookings/
│   │   │   │   ├── [id]/
│   │   │   │   └── new/
│   │   │   ├── contracts/
│   │   │   │   └── [id]/
│   │   │   ├── payments/
│   │   │   │   └── [id]/
│   │   │   ├── messages/
│   │   │   │   └── [conversationId]/
│   │   │   ├── profile/
│   │   │   │   └── edit/
│   │   │   ├── settings/
│   │   │   ├── reviews/
│   │   │   ├── notifications/
│   │   │   └── favorites/
│   │   │
│   │   └── api/                    # Next.js API routes
│   │       ├── auth/
│   │       └── webhooks/
│   │           └── stripe/
│   │
│   ├── components/
│   │   ├── common/                 # Buttons, inputs, modals, etc.
│   │   ├── layout/                 # Header, footer, sidebar, nav
│   │   ├── marketing/              # Hero, features, testimonials
│   │   ├── auth/                   # Login/register forms
│   │   ├── explore/                # Cards, filters, search bars
│   │   ├── booking/                # Calendar, time slots, summary
│   │   ├── contracts/              # Contract viewer, signature pad
│   │   ├── payments/               # Payment forms, escrow status
│   │   ├── messages/               # Chat UI, conversation list
│   │   ├── profile/                # Profile cards, portfolio
│   │   ├── reviews/                # Star ratings, review cards
│   │   ├── map/                    # Google Maps integration
│   │   └── media-center/           # Ad inventory cards, campaign builder
│   │
│   ├── hooks/                      # Custom React hooks
│   ├── lib/                        # API client, auth helpers, utils
│   ├── services/                   # API service layer (fetch wrappers)
│   ├── store/                      # Client state (Zustand / Context)
│   └── styles/                     # Global CSS, Tailwind config
│
├── next.config.js
├── tailwind.config.js
├── tsconfig.json
└── package.json
```

---

## apps/admin/ — Admin Dashboard (Next.js App Router)

```
apps/admin/
├── public/images/
├── src/
│   ├── app/
│   │   ├── (auth)/
│   │   │   └── login/
│   │   └── (dashboard)/
│   │       ├── overview/               # KPIs, charts, metrics
│   │       ├── users/
│   │       │   └── [id]/
│   │       ├── talents/
│   │       │   └── [id]/
│   │       ├── spaces/
│   │       │   └── [id]/
│   │       ├── equipment/
│   │       │   └── [id]/
│   │       ├── bookings/
│   │       │   └── [id]/
│   │       ├── contracts/
│   │       ├── payments/
│   │       │   ├── escrow/             # Escrow management
│   │       │   └── disputes/           # Dispute resolution
│   │       ├── reviews/                # Moderation
│   │       ├── media-center/
│   │       │   ├── inventory/          # Ad inventory management
│   │       │   └── campaigns/          # Campaign tracking
│   │       ├── analytics/
│   │       ├── settings/
│   │       └── reports/
│   │
│   ├── components/
│   │   ├── common/
│   │   ├── layout/                     # Admin sidebar, topbar
│   │   ├── charts/                     # Dashboard visualizations
│   │   ├── tables/                     # Data tables, pagination
│   │   └── forms/                      # CRUD forms
│   │
│   ├── hooks/
│   ├── lib/
│   ├── services/
│   ├── store/
│   └── styles/
│
├── next.config.js
├── tailwind.config.js
├── tsconfig.json
└── package.json
```

---

## apps/mobile/ — Mobile App (Expo Router)

```
apps/mobile/
├── assets/
│   ├── images/
│   └── fonts/
├── src/
│   ├── app/
│   │   ├── (tabs)/                     # Bottom tab navigation
│   │   │   ├── home/                   # Feed, recommendations
│   │   │   ├── explore/                # Map + list view
│   │   │   ├── bookings/               # My bookings
│   │   │   ├── messages/               # Chat inbox
│   │   │   └── profile/                # My profile
│   │   │
│   │   ├── auth/
│   │   │   ├── login/
│   │   │   ├── register/
│   │   │   └── forgot-password/
│   │   │
│   │   ├── talent/[id]/                # Talent detail screen
│   │   ├── space/[id]/                 # Space detail screen
│   │   ├── equipment/[id]/             # Equipment detail screen
│   │   ├── media/[id]/                 # Media detail screen
│   │   ├── booking/
│   │   │   ├── new/                    # Create booking flow
│   │   │   └── [id]/                   # Booking detail
│   │   ├── contract/[id]/              # View & sign contract
│   │   ├── payment/[id]/               # Payment screen
│   │   ├── reviews/
│   │   ├── notifications/
│   │   └── settings/
│   │
│   ├── components/
│   │   ├── common/                     # Shared mobile components
│   │   ├── auth/
│   │   ├── explore/                    # Cards, filters
│   │   ├── booking/                    # Booking flow components
│   │   ├── map/                        # MapView, markers, clusters
│   │   ├── profile/
│   │   ├── messages/                   # Chat bubbles, input
│   │   └── media-center/
│   │
│   ├── hooks/
│   ├── lib/
│   ├── services/
│   ├── store/
│   ├── styles/
│   └── navigation/                     # Navigation helpers, types
│
├── app.json
├── tsconfig.json
└── package.json
```

---

## apps/api/ — Backend API (Node.js + Prisma + PostgreSQL)

```
apps/api/
├── prisma/
│   ├── schema.prisma                   # Database schema
│   ├── migrations/                     # Auto-generated migrations
│   └── seeds/                          # Seed data scripts
│
├── src/
│   ├── modules/                        # Domain-driven modules
│   │   ├── auth/                       # JWT, OAuth, sessions
│   │   │   ├── auth.controller.ts
│   │   │   ├── auth.service.ts
│   │   │   ├── auth.routes.ts
│   │   │   ├── auth.validation.ts
│   │   │   └── auth.types.ts
│   │   │
│   │   ├── users/                      # User CRUD, roles
│   │   ├── talents/                    # Talent profiles, availability
│   │   ├── spaces/                     # Venue listings, availability
│   │   ├── equipment/                  # Equipment listings
│   │   ├── bookings/                   # Booking lifecycle
│   │   ├── contracts/                  # Contract generation, e-signatures
│   │   ├── payments/                   # Stripe, escrow, payouts
│   │   ├── reviews/                    # Ratings, moderation
│   │   ├── messages/                   # Real-time chat (WebSocket)
│   │   ├── notifications/              # Push, email, in-app
│   │   ├── media-center/              # Ad inventory, campaigns
│   │   ├── geolocation/              # Geo queries, distance, zones
│   │   ├── search/                    # Full-text search, filters
│   │   └── uploads/                   # Cloudinary integration
│   │
│   ├── middleware/                     # Auth, rate-limit, CORS, logging
│   ├── config/                        # Env vars, DB config, constants
│   ├── lib/                           # Prisma client, Stripe client, etc.
│   ├── jobs/                          # Background jobs (cron, queues)
│   ├── events/                        # Event emitters / domain events
│   ├── utils/                         # Pure utility functions
│   └── websockets/                    # Socket.io / WS server setup
│
├── tests/
│   ├── unit/
│   ├── integration/
│   └── e2e/
│
├── tsconfig.json
├── Dockerfile
└── package.json
```

---

## packages/ — Shared Packages

```
packages/
├── config/
│   ├── eslint/                        # Shared ESLint config
│   ├── typescript/                    # Shared tsconfig base
│   └── tailwind/                      # Shared Tailwind preset
│
├── shared/
│   ├── constants/                     # Enums, roles, statuses, categories
│   ├── types/                         # TypeScript interfaces & types
│   ├── utils/                         # Shared pure functions
│   └── validators/                    # Zod schemas (shared validation)
│
└── ui/
    ├── components/                    # Shared React components (web only)
    ├── icons/                         # Icon components / SVGs
    └── styles/                        # Design tokens, theme
```

---

## API Module Internal Pattern

Each module inside `apps/api/src/modules/<module>/` follows this convention:

| File                      | Purpose                                |
|---------------------------|----------------------------------------|
| `<module>.controller.ts`  | HTTP request handlers                  |
| `<module>.service.ts`     | Business logic                         |
| `<module>.routes.ts`      | Express/Fastify route definitions      |
| `<module>.validation.ts`  | Zod schemas for request validation     |
| `<module>.types.ts`       | Module-specific TypeScript types       |

---

## Key Architectural Decisions

| Decision                | Choice               | Rationale                                          |
|------------------------|----------------------|----------------------------------------------------|
| Monorepo tool          | Turborepo            | Fast builds, caching, minimal config               |
| Frontend framework     | Next.js App Router   | SSR, RSC, route groups, API routes                  |
| Mobile framework       | Expo (React Native)  | File-based routing, OTA updates, shared TS types    |
| API architecture       | Modular / domain-driven | Each domain is self-contained and testable       |
| ORM                    | Prisma               | Type-safe queries, migrations, introspection        |
| Database               | PostgreSQL           | PostGIS for geolocation, JSONB for flexible data    |
| Payments               | Stripe Connect       | Escrow via PaymentIntents + transfers               |
| File uploads           | Cloudinary           | Image/video optimization, transformations           |
| Maps                   | Google Maps API      | Geocoding, Places, real-time location               |
| Auth                   | JWT + refresh tokens | Stateless, scalable, role-based                     |
| Real-time              | Socket.io            | Chat, notifications, live booking updates           |
| Validation             | Zod                  | Shared between frontend & backend via packages/     |
| State management       | Zustand              | Lightweight, no boilerplate                         |
