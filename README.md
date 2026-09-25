![Header](https://capsule-render.vercel.app/api?type=waving&color=0:020617,100:0c4a6e&height=200&section=header&text=AYUSH%20GUPTA&fontSize=48&fontColor=ffffff&stroke=38bdf8&strokeWidth=1&animation=fadeIn&fontAlignY=36&desc=Full-Stack%20Engineer%20—%20SocialFlux%20Builder%20—%20Open%20to%20Work&descAlignY=60&descSize=14)

<p align="center">
  <a href="https://github.com/Therealayus/Metaflux"><img src="https://readme-typing-svg.demolab.com?font=Fira+Code&weight=600&pause=1000&color=38BDF8&center=true&vCenter=true&width=680&lines=SocialFlux+%E2%80%94+Talk+to+Meta.+We+handle+the+APIs.;AI-native+automation+%2B+human-in-the-loop+safety;Next.js+14+%2B+Fastify+%2B+Postgres+%2B+Redis+%2B+Workers;p95+22ms+%7C+idempotent+%7C+multi-tenant+%7C+audited" alt="SocialFlux — Talk to Meta. We handle the APIs." /></a>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/OPEN_TO_WORK-Backend_%2F_Full--Stack_%2F_AI_Platform-22c55e?style=for-the-badge&logo=briefcase&logoColor=white" alt="Open to work" />
  <br/>
  <img src="https://img.shields.io/badge/FLAGSHIP-SocialFlux__Metaflux-0f172a?style=for-the-badge&logo=rocket&logoColor=38bdf8" alt="Flagship SocialFlux" />
  <img src="https://komarev.com/ghpvc/?username=Therealayus&style=flat-square&color=0f172a&label=PROFILE+VIEWS" alt="Profile views" />
</p>

```typescript
const ayush = {
  role: "Full-Stack Engineer — AI platforms & real-time systems",
  location: "India · UTC+5:30 · Remote-ready",
  flagship: "SocialFlux (Metaflux) — AI-native Meta API automation platform",
  philosophy: "Never LLM → arbitrary call. Validate → authorize → confirm → execute.",
  stack: ["TypeScript", "Next.js 14", "Fastify", "Postgres + Prisma", "Redis Streams", "Turborepo + pnpm", "Docker"],
  hireFor: ["Backend Engineer", "Full-Stack Engineer", "Platform / Integration Engineer"],
  contact: "ayushgupta2429@gmail.com"
};
```

---

## 🌌 Flagship: SocialFlux — Talk to Meta. We'll handle the APIs.

> **[Therealayus/Metaflux](https://github.com/Therealayus/Metaflux)** — premium AI-native Meta integration & automation platform.
> Modular monolith (`apps/web · apps/api · apps/worker + packages/*`) with clean boundaries ready to extract to microservices.
>
> ![CI](https://github.com/Therealayus/Metaflux/actions/workflows/ci.yml/badge.svg?branch=main) ![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg) ![Node 20](https://img.shields.io/badge/node-20-339933?logo=node.js&logoColor=white)

**One-line employer pitch:** I built a multi-tenant, audited, rate-limited AI gateway to Meta — with safe AI execution, durable workflows, and production ops baked in.

### ⚡ System at a glance

```
Next.js 14 (landing + auth + dashboard :3000)
        ↓
Fastify /api/v1 (Zod-validated, typed DTOs, cursor pagination max 100)
        ↓
Service layer → Workers (idempotent + retries + DLQ) · Webhook gateway · AI service
        ↓
Redis Streams (queue / delays / cache / flags) → Postgres (tenant data) + S3/MinIO (>32KB payloads)
```

**Deployables:** `apps/web` · `apps/api` · `apps/worker`
**Domain packages:** `meta` (client/auth/capabilities/permissions/assets/webhooks) · `ai` (provider-neutral planner + validation gate) · `types · auth · database · workflows · queues · observability · security · ui`

```bash
cp .env.example .env
docker compose up -d            # postgres, redis, minio
pnpm install
pnpm --filter @socialflux/database push
pnpm dev                        # web :3000, api :4000, worker
```

### 🧠 AI safety — not a wrapper, a control plane

```
Natural language → LLM → Structured plan → Validation → Permission → Policy → User confirmation → Execution → Meta API
```

- Provider-neutral `AIProvider` + rule-based fallback
- Prompt-hash plan cache (1h TTL) + per-org monthly budgets + cheap-vs-strong model routing
- Endpoints: `POST /ai/plan|/explain|/diagnose`, `GET /ai/usage`
- Rule: tenant IDs come from session, never from client. Destructive calls need `x-confirm: true`.

### 🔐 Security & multi-tenancy employers ask about

- AES-256-GCM Meta token encryption, API keys `mf_…` SHA-256 hashed (shown once), scopes: `messages:send events:read workflows:* leads:read assets:read ai:use`
- Auth: httpOnly session cookie `POST /auth/signup|/signin|/signout`, `GET /auth/me`, single-use password-reset, Google/GitHub OAuth hooks
- RBAC + tenant isolation server-side, Helmet, payload limits, SSRF guard, webhook signature verification, redacting logger (no tokens in logs/frontend)

### 📈 Scale & ops numbers (measured, dev box)

- `496 req, 0 errors, p95 22ms @ 40 RPS` single API process — `300/min` rate-limit sheds with `429` before latency degrades
- Workers: stateless, `QUEUE_CONCURRENCY=5`, Redis consumer groups + `XAUTOCLAIM` reclaim after 30s
- Reads: replica via `getReplicaPrisma()` for `listEvents`/`listApiRequests`, fallback to primary
- DB: pooled Postgres, indexes on `(organizationId, createdAt/receivedAt)`, partition `WebhookEvent`/`AuditLog` by month past ~50M rows
- DR: Postgres PITR (base + WAL), Redis AOF, KMS-backed `TOKEN_ENCRYPTION_KEY`, probes `/live` `/api/v1/ready` `/api/v1/metrics`

### 🧩 Platform surface (`/api/v1`)

`connections/meta` OAuth + health/permissions · `assets` graph · `workflows` + `executions/:id/retry` · `messages` unified send `{channel, recipient, message, idempotencyKey}` · `webhooks/meta` ingress + replay · `events` (S3-resolved payloads) · `leads` · `billing` checkout/plan/webhook · `admin/overview|/dlq|/flags`

📌 **Shortlist signal:** system design + AI safety + webhooks + billing + observability in one repo — with docs: `ARCHITECTURE · AI_ARCHITECTURE · API · DATABASE · SCALING · SECURITY · WEBHOOKS · WORKFLOW_ENGINE · DEPLOYMENT`.

---

## 🛠️ Stack — futuristic but production-grade

![TypeScript](https://img.shields.io/badge/TypeScript-3178C6?style=for-the-badge&logo=typescript&logoColor=white)
![Next.js](https://img.shields.io/badge/Next.js_14-000000?style=for-the-badge&logo=next.js&logoColor=white)
![Fastify](https://img.shields.io/badge/Fastify-000000?style=for-the-badge&logo=fastify&logoColor=white)
![Postgres](https://img.shields.io/badge/Postgres-4169E1?style=for-the-badge&logo=postgresql&logoColor=white)
![Prisma](https://img.shields.io/badge/Prisma-2D3748?style=for-the-badge&logo=prisma&logoColor=white)
![Redis](https://img.shields.io/badge/Redis-DC382D?style=for-the-badge&logo=redis&logoColor=white)
![Turborepo](https://img.shields.io/badge/Turborepo-EF4444?style=for-the-badge&logo=turborepo&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logo=docker&logoColor=white)
![Node.js](https://img.shields.io/badge/Node_20+-339933?style=for-the-badge&logo=node.js&logoColor=white)
![Zod](https://img.shields.io/badge/Zod-3E67B1?style=for-the-badge&logo=zod&logoColor=white)
![Tailwind](https://img.shields.io/badge/Tailwind-06B6D4?style=for-the-badge&logo=tailwindcss&logoColor=white)
![Socket.IO](https://img.shields.io/badge/Socket.IO-010101?style=for-the-badge&logo=socket.io&logoColor=white)
![MongoDB](https://img.shields.io/badge/MongoDB-47A248?style=for-the-badge&logo=mongodb&logoColor=white)

| What employers get | How SocialFlux proves it |
|---|---|
| System design | Modular monolith → extractable services, LB-ready stateless API/web, Redis Streams workers |
| AI engineering | Gated pipeline, budget enforcement, plan cache, model routing — no unsafe tool calls |
| Backend rigor | Zod + typed DTOs + `{code,message,requestId}` errors + cursor pagination + idempotency keys |
| Data engineering | Prisma multi-tenant schema (User/Org/Membership/Workspace/Session/MetaConnection/MetaAsset/Workflow/Execution/WebhookEvent/AuditLog) |
| DevOps mindset | Docker Compose (PG/Redis/MinIO), Turbo `dev|build|test|lint|typecheck`, Prometheus metrics, ngrok `socialflux` profile |

---

## 💼 More builds

- **[Color Arena](https://github.com/Therealayus/code-arena)** — Real-time game engine, 60s rounds, deterministic lowest-bet winner, Socket.IO ticks/payouts. `MERN · TypeScript`
- **[social-media-app](https://github.com/Therealayus/social-media-app)** — Instagram-like backend. `Node.js · Drizzle · Postgres · Redis · Socket.IO`
- **[allergen-label-generator](https://github.com/Therealayus/allergen-label-generator)** — Allergen intelligence over Open Food Facts. `Node.js · Express`
- **[ayush-portfolio](https://github.com/Therealayus/ayush-portfolio)** — Portfolio. `HTML · CSS · JS`

---

## 📊 Proof of work

<p align="center">
  <img src="https://github-readme-stats.vercel.app/api?username=Therealayus&show_icons=true&theme=tokyonight&hide_border=true&rank_icon=github&include_all_commits=true" height="165" alt="stats" />
  <img src="https://streak-stats.demolab.com?user=Therealayus&theme=tokyonight&hide_border=true" height="165" alt="streak" />
</p>
<p align="center">
  <img src="https://github-readme-stats.vercel.app/api/top-langs/?username=Therealayus&layout=compact&theme=tokyonight&hide_border=true" height="130" alt="top langs" />
</p>

---

## 📫 Hire me — let's ship SocialFlux-grade systems

**Ayush Gupta — Full-Stack Engineer, SocialFlux (Metaflux) builder**

- ✉️ [ayushgupta2429@gmail.com](mailto:ayushgupta2429@gmail.com)
- 🌌 Flagship: [Therealayus/Metaflux — SocialFlux](https://github.com/Therealayus/Metaflux)
- 🌐 [github.com/Therealayus](https://github.com/Therealayus)

> Open to Backend / Full-Stack / Platform roles (remote-friendly). I bring AI-safe execution, multi-tenant APIs, durable workers, and docs employers can audit — ready for interview deep-dives on architecture, scaling, and trade-offs.

![Footer](https://capsule-render.vercel.app/api?type=waving&color=0:0c4a6e,100:020617&height=120&section=footer)
