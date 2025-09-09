# 🎮 ArenaX Documentation

## 1. 🏗️ Project Overview

ArenaX is a competitive gaming tournament platform designed for
**amateur gamers in Nigeria**. Players can join tournaments, compete,
report scores with proof, and receive instant payouts via local payment
methods (Opay, PalmPay, Bank transfers).

Core goals: - Make **esports accessible** to everyday mobile/console
gamers. - Provide a **secure, fair environment** (anti-cheat, score
verification). - Enable **fast payouts** with local payment systems.

------------------------------------------------------------------------

## 2. 📐 System Architecture

**Frontend (Next.js PWA)** ↔ **Backend (Rust + Axum)** ↔ **Postgres +
Redis + S3 + Payments**

-   **Frontend (Next.js PWA)** → User interface (mobile-first web app).
-   **Backend (Rust + Axum)** → API, authentication, tournaments,
    wallet, matches.
-   **PostgreSQL** → Persistent data (users, tournaments, matches,
    wallets).
-   **Redis** → OTP storage, caching, leaderboards.
-   **S3/MinIO** → Screenshot storage.
-   **Payment Gateways** → Paystack / Flutterwave for deposits &
    withdrawals.

------------------------------------------------------------------------

## 3. ⚙️ Tech Stack

-   **Frontend**: Next.js (PWA), TailwindCSS, shadcn/ui
-   **Backend**: Rust (Axum, SQLx, Tokio)
-   **Database**: PostgreSQL
-   **Cache**: Redis
-   **Storage**: S3/MinIO
-   **Payments**: Paystack / Flutterwave

------------------------------------------------------------------------

## 4. 🚀 Setup Guide

### Prerequisites

-   Rust toolchain (`cargo`, `rustup`)
-   Node.js (v18+)
-   PostgreSQL
-   Redis
-   MinIO (or AWS S3)
-   Docker (for local containers)

### Backend Setup

``` bash
# Clone repo
git clone https://github.com/arenax.git
cd backend

# Install dependencies
cargo build

# Run migrations
sqlx migrate run

# Start server
cargo run
```

### Frontend Setup

``` bash
# Clone repo
git clone https://github.com/arenax/arenax.git
cd frontend

# Install dependencies
npm install

# Run dev server
npm run dev
```

### Environment Variables

Create `.env` files:

``` env
DATABASE_URL=postgres://user:pass@localhost:5432/arenax
REDIS_URL=redis://localhost:6379
S3_ENDPOINT=http://localhost:9000
S3_ACCESS_KEY=minio
S3_SECRET_KEY=secret
PAYSTACK_SECRET=sk_test_xxx
JWT_SECRET=supersecretkey
```

------------------------------------------------------------------------

## 5. 🎮 Feature Documentation

### Authentication

-   Phone OTP login/signup.
-   JWT-based sessions.
-   Device fingerprinting to prevent multi-accounts.

### Wallet & Payments

-   Deposit via Paystack/Flutterwave.
-   Withdraw via Opay/Bank API.
-   Transaction history stored in Postgres.

### Tournaments

-   Admin creates tournaments.
-   Players join by paying entry fee.
-   Auto status transitions: upcoming → ongoing → completed.

### Matches

-   Bracket generation.
-   Score reporting with screenshot upload.
-   Dispute system for score mismatches.

### Leaderboard & Reputation

-   Weekly/monthly leaderboards.
-   Reputation points for fair play.
-   Penalties for disputes/cheating.

------------------------------------------------------------------------

## 6. 📑 API Reference (Core Endpoints)

### Auth

-   `POST /auth/signup` → register phone.
-   `POST /auth/verify` → verify OTP, create account.
-   `GET /auth/me` → get profile.

### Wallet

-   `GET /wallet` → balance + history.
-   `POST /wallet/deposit` → deposit funds.
-   `POST /wallet/withdraw` → withdraw funds.

### Tournaments

-   `GET /tournaments` → list tournaments.
-   `POST /tournaments/:id/join` → join.
-   `GET /tournaments/:id` → details.

### Matches

-   `POST /matches/:id/report` → submit score + screenshot.
-   `POST /matches/:id/dispute` → dispute result.
-   `GET /matches/:id` → match details.

### Leaderboard

-   `GET /leaderboard?period=weekly` → top players.

------------------------------------------------------------------------

## 7. 🛠️ Developer Guidelines

-   **Coding Standards**:
    -   Rust: `cargo fmt` + `clippy`
    -   JS/TS: ESLint + Prettier
-   **Git Workflow**: feature branches → dev → main.
-   **Testing**:
    -   Rust: unit + integration tests.
    -   Next.js: Jest + React Testing Library.
-   **Error Handling**: standard JSON error format.

``` json
{
  "error": "Invalid OTP",
  "code": 401
}
```

------------------------------------------------------------------------

## 8. 🔒 Security & Compliance

-   OTP rate limiting (Redis).
-   One payout account per user.
-   Encrypt sensitive data (e.g., phone numbers).
-   Logs for suspicious activity.

------------------------------------------------------------------------

## 9. 📅 Roadmap

-   **Phase 1**: Auth, Wallet, Tournaments, Matches.
-   **Phase 2**: Leaderboards, Reputation, Admin panel.
-   **Phase 3**: AI screenshot verification, community tournaments,
    sponsorships.

------------------------------------------------------------------------



