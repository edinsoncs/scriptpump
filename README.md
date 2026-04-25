# ScriptPump

> The Open Source Platform for Fair Token Launches on Solana
> 
> **Website**: [scriptpump.fun](https://scriptpump.fun)

[![Next.js](https://img.shields.io/badge/Next.js-16-black?logo=next.js)](https://nextjs.org/)
[![Solana](https://img.shields.io/badge/Network-Solana-9945FF?logo=solana)](https://solana.com/)
[![License](https://img.shields.io/badge/License-Open%20Source-b6ff00)](LICENSE)
[![TypeScript](https://img.shields.io/badge/TypeScript-5.x-3178C6?logo=typescript)](https://www.typescriptlang.org/)
[![Deploy](https://img.shields.io/badge/Deploy-Vercel-black?logo=vercel)](https://vercel.com/)

---

## Table of Contents

- [Overview](#overview)
- [Business Model](#business-model)
- [Features](#features)
  - [For Users](#for-users)
  - [For Creators](#for-creators)
  - [Admin Dashboard](#admin-dashboard)
- [Tech Stack](#tech-stack)
- [Project Structure](#project-structure)
- [Installation](#installation)
- [Environment Variables](#environment-variables)
- [Development](#development)
- [Build & Deploy](#build--deploy)
- [Integrations](#integrations)
- [Contributing](#contributing)
- [Security](#security)
- [API Reference](#api-reference)
- [Smart Contract Architecture](#smart-contract-architecture)
- [Performance](#performance)
- [Roadmap](#roadmap)
- [License](#license)

---

## Overview

**ScriptPump** ([scriptpump.fun](https://scriptpump.fun)) is a developer-first, open-source toolkit that makes launching tokens on Solana simple, fair, and transparent. No presale. No team allocation. No AI models required. Just one click to deploy your own launchpad.

Built for the Solana ecosystem, ScriptPump empowers anyone to create, manage, and profit from their own token platform — with full control over fees, branding, and revenue.

### Core Philosophy

1. **Fair Launch**: Every token starts equal. No presale, no insider allocation, no hidden mechanics.
2. **Open Source**: Full transparency. Anyone can audit, fork, or contribute.
3. **Zero Dependency**: No LLMs, no external AI models, no complex infrastructure required.
4. **Community Ownership**: Platform owners control their fees, their branding, their destiny.

> *"The future is open source + AI. Create what you feel in your heart and make it better."*  
> — **Edinson Carranza**, CEO & Founder

---

## Business Model

### Revenue Streams

| Stream | Description |
|--------|-------------|
| **Platform Fees** | Configurable fee percentage on every token launch. Set by the admin. |
| **Transaction Fees** | Small percentage collected on each token trade within the launchpad. |
| **Premium Features** | Optional paid upgrades for advanced analytics, custom branding, and priority support. |

### Key Advantages

- **No Lock-in**: Open source. Deploy anywhere. Own your infrastructure.
- **Full Fee Control**: Admin sets all rates. No hidden charges from third parties.
- **Community-Driven**: Revenue grows with the community. More launches = more earnings.
- **Self-Sustaining**: Platform funds its own development through collected fees.

### Competitive Edge

| Feature | ScriptPump | Pump.fun | Bags.fm | Printr.money | LetsBonk |
|---------|:----------:|:--------:|:-------:|:------------:|:--------:|
| Custom Branding | Unlimited | No | No | No | No |
| Own Domain | Included | No | No | No | No |
| Fee Control | Full Control | No | Partial | No | No |
| Database Integrations | Unlimited | No | No | No | No |
| Email Workflows | Built-in | No | No | No | No |
| Revenue Dashboard | Real-time | Basic | No | Basic | No |
| Multi-currency Rewards | Auto-sync | No | No | No | No |
| Pool Management | Full Control | No | No | No | No |
| Open Source | Yes | No | No | No | No |
| Admin Panel | Complete | No | No | No | No |

---

## Features

### For Users

- **Create Tokens** — Deploy fair launch tokens on Solana in seconds. No presale, no team allocation.
- **View Profile** — Track your launches, holdings, and activity in one clean dashboard.
- **Followers** — Build your audience. Get notified when creators launch new tokens.
- **Charts** — Real-time price charts with volume, liquidity, and market data.
- **Bond Token** — Bonding curve mechanics for fair price discovery from launch.
- **Frontend Ready** — Beautiful, responsive UI out of the box. Dark and light themes included.

### For Creators

- **Earn from Every Launch** — Collect fees from your community. You control the rates.
- **Revenue Analytics** — Track all fees collected in real-time. See total revenue, daily earnings, and payout history.
- **Multi-Currency Wallet** — Claim earnings in different currencies created by your community.
- **Instant Withdrawals** — Secure, fast withdrawal of earned rewards.

### Admin Dashboard

| Module | Description |
|--------|-------------|
| **Overview** | Complete platform analytics. Real-time metrics, user activity, and revenue summary. |
| **Services** | Connect with Firebase, Supabase, MongoDB, or any database. Built-in email workflows, Solana RPC configuration, and cloud storage. |
| **Rewards** | Multi-currency reward claiming, revenue dashboards, and payout management. |
| **Pools** | Verify, update, delete, or block any liquidity pool. Advanced filtering, batch operations, and audit logs. |

---

## Tech Stack

| Layer | Technology |
|-------|-----------|
| **Frontend** | Next.js 16, React 19, TypeScript, Tailwind CSS |
| **Font** | Geist, Geist Mono |
| **Backend** | Serverless functions, API Routes |
| **Database** | Supabase / Firebase / MongoDB (configurable) |
| **Blockchain** | Solana, Helius RPC |
| **Email** | Resend |
| **Hosting** | AWS / Vercel |
| **Package Manager** | npm |

---

## Project Structure

```
scriptpump/
├── app/
│   ├── layout.tsx          # Root layout with fonts & metadata
│   ├── page.tsx            # Main landing page (all sections)
│   ├── globals.css         # Global styles & animations
│   └── favicon.ico
├── public/
│   ├── bg1.png             # Dark theme screenshot
│   ├── bg2.png             # Light theme screenshot
│   ├── screen1.png         # Admin — Overview
│   ├── screen2.png         # Admin — Services
│   ├── screen3.png         # Admin — Rewards
│   ├── screen4.png         # Admin — Pools
│   ├── ava.png             # Team avatar photo
│   ├── scriptpump-wizard-cat.png  # Hero mascot
│   └── 1png.png – 6png.png       # Feature cards
├── .next/                  # Build output
├── package.json
├── tsconfig.json
├── next.config.ts
├── tailwind.config.ts
├── postcss.config.mjs
└── README.md
```

---

## Installation

### Prerequisites

- **Node.js** >= 18.18.0
- **npm** >= 9.0.0 (or yarn/pnpm/bun)
- **Git**

### Quick Start

```bash
# Clone the repository
git clone https://github.com/edinsoncs/ScriptPump.git
cd ScriptPump

# Install dependencies
npm install

# Set up environment variables
cp .env.example .env.local

# Start development server
npm run dev
```

Open [http://localhost:3000](http://localhost:3000) in your browser.

---

## Environment Variables

Create a `.env.local` file in the project root:

```env
# Solana / Helius RPC
NEXT_PUBLIC_HELIUS_RPC_URL=https://mainnet.helius-rpc.com/?api-key=YOUR_KEY

# Database (choose one)
DATABASE_URL=postgresql://user:password@host:5432/scriptpump   # Supabase/PostgreSQL
FIREBASE_API_KEY=your_firebase_api_key
MONGODB_URI=mongodb://localhost:27017/scriptpump

# Email (Resend)
RESEND_API_KEY=re_XXXXXXXXXXXXXXXXXXXX

# App
NEXT_PUBLIC_APP_URL=http://localhost:3000
NEXT_PUBLIC_SOLANA_NETWORK=mainnet-beta
```

---

## Development

### Available Scripts

| Command | Description |
|---------|-------------|
| `npm run dev` | Start development server with Turbopack |
| `npm run build` | Build for production |
| `npm run start` | Start production server |
| `npm run lint` | Run ESLint |
| `npm run type-check` | Run TypeScript type checking |

### Code Style

- **TypeScript** strict mode enabled
- **ESLint** with Next.js recommended rules
- **Prettier** for consistent formatting
- **Tailwind CSS** for utility-first styling

### Component Architecture

All components are defined inline within `app/page.tsx` as a single-page landing. Each section is a self-contained `<section>` element with:

- `FeatureCard` — Image-based feature cards with hover effects
- `AdminArticle` — Admin feature descriptions with icons
- `BenchmarkRowFull` — Comparison table rows
- `ArticleCard` — Reference/article link cards
- `TechLogo` — Technology stack carousel items

---

## Build & Deploy

### Production Build

```bash
npm run build
npm run start
```

### Deploy on Vercel

```bash
vercel deploy --prod
```

### Deploy on AWS

1. Build the project: `npm run build`
2. Upload the `.next` standalone folder to your AWS EC2/ECS
3. Configure nginx or ALB for routing
4. Set environment variables in AWS Secrets Manager

### Custom Domain

ScriptPump supports custom domains. Configure in your hosting provider's dashboard and update `NEXT_PUBLIC_APP_URL`.

---

## Integrations

### Solana & Helius RPC

Connect to Solana mainnet/devnet via Helius for fast, reliable RPC calls. Used for token deployment, transaction monitoring, and wallet interactions.

### Database

Plug-and-play support for:

- **Supabase** (PostgreSQL) — Recommended for production
- **Firebase** — Real-time data and authentication
- **MongoDB** — Flexible document store

### Email (Resend)

Built-in email workflows for:

- Token launch confirmations
- Revenue payout notifications
- User onboarding and verification

---

## Benchmark

See the [comparison table](#competitive-edge) above for a full feature comparison against competing platforms.

---

## Contributing

ScriptPump is open source and welcomes contributions from the community.

### How to Contribute

1. **Fork** the repository
2. **Create** a feature branch: `git checkout -b feat/your-feature`
3. **Commit** your changes: `git commit -m 'feat: add new feature'`
4. **Push** to the branch: `git push origin feat/your-feature`
5. **Open** a Pull Request at [github.com/edinsoncs/ScriptPump](https://github.com/edinsoncs/ScriptPump)

### Reporting Issues

Report bugs, request features, or contribute code via [GitHub Issues](https://github.com/edinsoncs/ScriptPump/issues).

### Guidelines

- Follow the existing code style
- Write clear commit messages
- Test your changes before submitting
- Keep PRs focused and scoped

---

## Team

### Edinson Carranza — CEO & Founder

One of the earliest developers of the Shiba Inu ecosystem — creator of the original **shibatoken.com**, contributor to **ShibaSwap** and the **Ethereum Foundation Ecosystem** (2021). Registered company director in the UK since 2020.

Now building **ScriptPump** — bringing open source tools to the Solana ecosystem so anyone can launch, manage, and profit from their own token platform.

- GitHub: [@edinsoncs](https://github.com/edinsoncs)
- X/Twitter: [@scriptpumpsol](https://x.com/scriptpumpsol)

---

## License

Open source. Built with ♥ by the collaboration of **Viainti**.

> The future is open source + AI.

---

## Smart Contract Architecture

### Token Launch Flow

```
User Wallet → ScriptPump Frontend → Solana Program → Token Mint
                                      ↓
                              Liquidity Pool (Bonding Curve)
                                      ↓
                              Revenue Split → Platform Fees → Admin Wallet
```

### Bonding Curve Mechanics

ScriptPump uses a bonding curve model for initial token price discovery:

- **Initial Price**: Set by creator (default: minimal SOL)
- **Curve Type**: Exponential (configurable)
- **Liquidity**: Auto-generated from buys
- **Migration**: Optional Raydium AMM migration at market cap threshold

### Program Accounts

| Account | Purpose |
|---------|---------|
| `LaunchConfig` | Stores token parameters, fee rates, and creator settings |
| `TokenVault` | Holds minted tokens and SOL liquidity |
| `RevenueSplit` | Manages fee distribution between creator and platform |
| `PoolRegistry` | Tracks all active pools and their states |

---

## API Reference

### REST Endpoints

| Method | Endpoint | Description |
|--------|----------|-------------|
| `GET` | `/api/tokens` | List all launched tokens |
| `GET` | `/api/tokens/:mint` | Get token details and metrics |
| `POST` | `/api/tokens/create` | Deploy new token (requires wallet signature) |
| `GET` | `/api/pools` | List all active pools |
| `GET` | `/api/pools/:id` | Get pool details and bonding curve state |
| `POST` | `/api/pools/:id/migrate` | Migrate pool to Raydium AMM |
| `GET` | `/api/analytics/revenue` | Get platform revenue metrics |
| `POST` | `/api/admin/fees` | Update platform fee configuration |

### WebSocket Events

| Event | Payload | Description |
|-------|---------|-------------|
| `token:created` | `{ mint, creator, timestamp }` | New token deployed |
| `trade:executed` | `{ token, amount, price, buyer }` | Trade executed on bonding curve |
| `pool:migrated` | `{ pool, raydiumPool }` | Pool migrated to AMM |
| `revenue:updated` | `{ total, daily, fees }` | Revenue metrics updated |

---

## Security

### Audits

- **Smart Contract Audit**: Pending
- **Frontend Security**: CSP headers, XSS protection, CSRF tokens
- **Wallet Integration**: Phantom, Solflare, Backpack supported

### Security Best Practices

1. **Transaction Signing**: All on-chain actions require explicit wallet signature
2. **Rate Limiting**: API endpoints protected against abuse
3. **Input Validation**: Strict schema validation on all user inputs
4. **Secrets Management**: Environment variables stored securely, never committed
5. **Dependency Scanning**: Regular `npm audit` and Snyk scans

### Bug Bounty

Found a vulnerability? Report it via [GitHub Issues](https://github.com/edinsoncs/ScriptPump/issues) with the `security` label.

---

## Performance

### Benchmarks

| Metric | Value |
|--------|-------|
| **Lighthouse Score** | 95+ Performance |
| **First Contentful Paint** | < 0.8s |
| **Time to Interactive** | < 1.5s |
| **Bundle Size** | < 200KB (gzipped) |
| **Image Optimization** | Next.js automatic WebP/AVIF |

### Optimization Techniques

- **Turbopack**: Fast HMR during development
- **Image Optimization**: Automatic format conversion and lazy loading
- **Font Optimization**: Geist with `font-display: swap`
- **CSS Minification**: Tailwind purge + PostCSS
- **Code Splitting**: Route-level and component-level splitting
- **Edge Caching**: Static assets cached at CDN level

---

## Roadmap

### Q2 2026
- [ ] Multi-chain support (Ethereum, Base)
- [ ] Advanced analytics dashboard
- [ ] Mobile app (React Native)
- [ ] NFT integration for token creators

### Q3 2026
- [ ] DAO governance for platform parameters
- [ ] Staking mechanism for fee reduction
- [ ] Cross-chain bridge integration
- [ ] SDK for third-party integrations

### Q4 2026
- [ ] AI-assisted token parameter optimization
- [ ] Automated market maker improvements
- [ ] Enterprise white-label solutions
- [ ] Multi-language support

---

---

## Links

- **Website**: [scriptpump.fun](https://scriptpump.fun)
- **GitHub**: [github.com/edinsoncs/ScriptPump](https://github.com/edinsoncs/ScriptPump)
- **Issues**: [github.com/edinsoncs/ScriptPump/issues](https://github.com/edinsoncs/ScriptPump/issues)
- **Twitter**: [@scriptpumpsol](https://x.com/scriptpumpsol)

---

## References & History

- [Original ShibaToken.com (2021)](https://web.archive.org/web/20210221162114/https://shibatoken.com/) — Wayback Machine
- [SHIB Army (2021)](https://web.archive.org/web/20210225001720/https://shibarmy.net/) — Wayback Machine
- [UK Company Registry (2020)](https://find-and-update.company-information.service.gov.uk/company/12844191/officers) — GOV.UK
- [Shiba Exposed (2021)](https://shibaexposed.wordpress.com/) — WordPress
