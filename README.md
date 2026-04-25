# ScriptPump.fun - Solana Token Launchpad

> **Created by:** [viainti](https://github.com/viainthi) & [edinsoncs](https://github.com/edinsoncs)

Professional Solana token launchpad platform with dynamic bonding curves (Meteora DBC), rewards system, AI-powered whitepaper generator, social authentication, complete admin dashboard, and integrated social feed.

---

## Table of Contents

1. [Business Model](#business-model)
2. [Key Features](#key-features)
3. [Technical Architecture](#technical-architecture)
4. [Project Structure](#project-structure)
5. [Installation & Configuration](#installation--configuration)
6. [API Endpoints](#api-endpoints)
7. [Environment Variables](#environment-variables)
8. [Database - Firebase](#database---firebase)
9. [Bonding Curve System](#bonding-curve-system)
10. [Rewards System](#rewards-system)
11. [Whitepaper Generator](#whitepaper-generator)
12. [Installer - Setup Wizard](#installer---setup-wizard)
13. [Authentication](#authentication)
14. [Internationalization (i18n)](#internationalization-i18n)
15. [Deployment](#deployment)
16. [Tech Stack](#tech-stack)

---

## Business Model

ScriptPump.fun is a **pump.fun-style token launchpad** operating on the **Solana** network using the **Meteora Dynamic Bonding Curve (DBC) SDK**. The business model is built on multiple revenue streams:

### 1. Token Launch Fees
- Each launched token generates a configurable commission (`feePercent` 1-5%)
- The fee is distributed between the **creator** (50% default) and the **host/partner** (50% default)
- Fees accumulate in the pool and can be claimed at any time

### 2. Pool Creation Fee
- Fixed fee in lamports for each pool created (`poolCreationFee`)
- Configurable by the host administrator

### 3. Migration to Meteora DAMM v2
- When reaching the migration threshold (`migrationQuoteThreshold` default: 50 SOL), liquidity automatically migrates to Meteora DAMM v2
- A percentage of supply (`percentageSupplyOnMigration` default: 10%) is reserved for migration
- Configurable migration fee (`migrationFeeOption: FixedBps25`)

### 4. Host Rewards (Partner Fees)
- The host/administrator receives partner fees on every pool transaction
- Partner fees accumulate and can be claimed from the admin dashboard
- Host wallet configurable via `METEORA_HOST_SECRET_BASE64` and `METEORA_HOST_RECEIVER`

### 5. Vanity Token Address (Premium)
- Generation of token addresses with custom suffix (e.g., `...tkl`)
- Configurable via `TOKEN_ADDRESS_SUFFIX` and `TOKEN_ADDRESS_MAX_ATTEMPTS`
- Premium functionality for projects wanting branding on their contract address

### 6. Additional Services
- **AI Whitepaper Generator**: Automatic generation of professional whitepapers using OpenAI GPT-4o-mini
- **Social Feed**: Creators can publish updates about their tokens
- **Website Builder**: Tool for creating token landing pages
- **Staking**: Integrated staking system (component ready)

### Revenue Flow

```
User creates token → Pays fee (1-5%) → 50% creator / 50% host
       ↓
Active pool on bonding curve → Each swap generates fees
       ↓
Threshold reached (50 SOL) → Migration to Meteora DAMM v2
       ↓
Host claims rewards periodically → Recurring revenue
```

---

## Key Features

### For Users
- **Token creation in minutes**: No code, intuitive interface
- **Built-in wallet**: Solana wallet generation and management from the browser
- **Optional Initial Buy**: Automatic token purchase at launch time
- **Social links**: Up to 12 configurable social networks per token
- **Image upload**: Logo and cover with IPFS storage (Pinata)
- **Whitepaper generator**: AI-powered generation in 8 languages
- **Social feed**: Post updates and promote tokens
- **Profile with rewards**: View and claim rewards from all created tokens
- **Multi-wallet**: Support for multiple stored wallets

### For Administrators (Host)
- **Complete admin dashboard**: Overview, services, rewards, pools, bonds, templates, addons
- **Installer wizard**: 3-step guided setup to configure the platform
- **Mass rewards claiming**: Claim all partner fees from all pools
- **Real-time metrics**: Tokens launched, total liquidity, active users
- **Bonding curve configuration**: Customizable parameters per configuration
- **Service management**: Firebase/Supabase/MongoDB, email, RPC

### Technical
- **Vanity addresses**: Generation of contract addresses with custom suffix
- **Email verification**: Mandatory verification for email/password auth
- **Social auth**: Twitter, Google, Telegram
- **i18n**: Multi-language support (EN, ES, PT, FR, DE, ZH, JA, KO)
- **Responsive**: Mobile-first, works on all devices
- **Dark theme**: Professional design with dark theme and green accents (#A3FF12)

---

## Technical Architecture

```
┌─────────────────────────────────────────────────────────────────┐
│                        Frontend (Next.js)                        │
│  ┌──────────┐  ┌──────────┐  ┌──────────┐  ┌──────────────────┐ │
│  │ Home     │  │ Create   │  │ Token    │  │ Admin Dashboard  │ │
│  │ Dashboard│  │ Token    │  │ Detail   │  │ (Overview, Pools,│ │
│  │          │  │ Wizard   │  │ Page     │  │  Rewards, Bonds) │ │
│  └──────────┘  └──────────┘  └──────────┘  └──────────────────┘ │
│  ┌──────────┐  ┌──────────┐  ┌──────────┐  ┌──────────────────┐ │
│  │ Feed     │  │ Profile  │  │ White-   │  │ Installer Wizard │ │
│  │ Social   │  │ & Rewards│  │ paper    │  │ (3-step setup)   │ │
│  │          │  │          │  │ Builder  │  │                  │ │
│  └──────────┘  └──────────┘  └──────────┘  └──────────────────┘ │
└─────────────────────────────────────────────────────────────────┘
                              │
                    API Routes (Next.js)
                              │
┌──────────────┬──────────────┼──────────────┬─────────────────────┐
│              │              │              │                     │
▼              ▼              ▼              ▼                     ▼
┌──────────┐ ┌──────────┐ ┌──────────┐ ┌──────────┐ ┌──────────────┐
│ Solana   │ │ Meteora  │ │ Firebase │ │ OpenAI   │ │ Pinata IPFS  │
│ Network  │ │ DBC SDK  │ │ (Auth,   │ │ (GPT-4o  │ │ (Metadata    │
│ (RPC)    │ │ (Pools,  │ │  DB,     │ │  -mini)  │ │  Storage)    │
│          │ │  Curves) │ │ Storage) │ │          │ │              │
└──────────┘ └──────────┘ └──────────┘ └──────────┘ └──────────────┘
```

---

## Project Structure

```
tokenfun/
├── app/
│   ├── page.tsx                    # Home - Main dashboard with tokens, stats, rewards
│   ├── layout.tsx                  # Root layout with providers (theme, i18n, auth)
│   ├── globals.css                 # Global styles + Tailwind
│   │
│   ├── create/
│   │   └── page.tsx                # Token creation page (full wizard)
│   │
│   ├── token/[address]/
│   │   ├── page.tsx                # Token detail page (SSR)
│   │   └── token-details-client.tsx # Interactive detail client
│   │
│   ├── feed/
│   │   ├── page.tsx                # Main social feed
│   │   └── post/[id]/page.tsx      # Individual post detail
│   │
│   ├── profile/
│   │   ├── page.tsx                # User profile + rewards
│   │   └── [handle]/page.tsx       # Public profile by handle
│   │
│   ├── host-dashboard/
│   │   └── page.tsx                # Host dashboard (global rewards)
│   │
│   ├── settings/
│   │   └── page.tsx                # User settings
│   │
│   ├── white-paper/
│   │   └── page.tsx                # AI whitepaper generator
│   │
│   ├── build/
│   │   ├── page.tsx                # Builder hub
│   │   ├── website/page.tsx        # Website builder
│   │   └── whitepaper/page.tsx     # Whitepaper builder
│   │
│   ├── installer/
│   │   └── page.tsx                # Installation wizard (3 steps)
│   │
│   ├── admin/
│   │   ├── page.tsx                # Admin dashboard overview
│   │   ├── services/page.tsx       # Service management
│   │   ├── rewards/page.tsx        # Host rewards
│   │   ├── pools/page.tsx          # Pool management
│   │   ├── bonds/page.tsx          # Bonding curve configuration
│   │   ├── templates/page.tsx      # Templates
│   │   └── addons/page.tsx         # Addons (feed, staking, etc)
│   │
│   └── api/
│       ├── launch-token/
│       │   └── route.ts            # MAIN ENDPOINT: launch, claim, rewards, admin
│       ├── create/
│       │   └── route.ts            # Proxy for launch-token (public action)
│       ├── tokens/
│       │   └── route.ts            # List all created tokens
│       ├── token/ca/[address]/
│       │   └── route.ts            # Token info + rewards by CA
│       ├── token-metadata/
│       │   └── route.ts            # Upload metadata to IPFS (Pinata)
│       ├── pool-mcap/
│       │   └── route.ts            # Pool market cap
│       ├── generate-whitepaper/
│       │   └── route.ts            # Generate whitepaper with OpenAI
│       ├── generate-whitepaper-pdf/
│       │   └── route.ts            # Generate whitepaper PDF
│       ├── generate-content/
│       │   └── route.ts            # Generate content with AI
│       ├── stream/
│       │   └── route.ts            # WebSocket stream
│       ├── installer/env/
│       │   └── route.ts            # Generate .env.local from installer
│       ├── creator/[handle]/
│       │   ├── route.ts            # Creator info by handle
│       │   └── follow/route.ts     # Follow/unfollow creator
│       └── auth/
│           ├── twitter/
│           │   ├── route.ts        # Init Twitter OAuth
│           │   └── callback/route.ts # Twitter OAuth callback
│           ├── twitter/username/route.ts  # Get Twitter username
│           ├── telegram/route.ts   # Telegram WebApp auth
│           ├── verify-email/route.ts # Email verification
│           └── reset-password/route.ts   # Password reset
│
├── components/
│   ├── app-shell.tsx               # Main shell with sidebar
│   ├── main-header.tsx             # Header with rewards badge
│   ├── sidebar.tsx                 # Navigation sidebar
│   ├── premium-sidebar.tsx         # Premium sidebar
│   ├── mobile-nav.tsx              # Mobile navigation
│   ├── theme-provider.tsx          # Theme provider
│   ├── theme-toggle.tsx            # Dark/light toggle
│   ├── settings-modal.tsx          # Settings modal
│   ├── settings-modal-context.tsx  # Modal context
│   ├── profile-card.tsx            # Profile card
│   ├── live-stream.tsx             # Live stream component
│   ├── rewards-success-modal.tsx   # Rewards success modal
│   ├── claim-error-modal.tsx       # Claim error modal
│   │
│   ├── auth/
│   │   ├── twitter-auth-provider.tsx # Twitter auth provider
│   │   ├── email-verification-alert.tsx # Email verification alert
│   │   └── profile-menu.tsx        # Profile menu
│   │
│   ├── i18n/
│   │   ├── language-provider.tsx   # Language provider
│   │   └── language-switcher.tsx   # Language selector
│   │
│   ├── builder/                    # Website builder components
│   │   ├── builder-toolbar.tsx
│   │   ├── context-menu.tsx
│   │   ├── editable-button.tsx
│   │   ├── editable-icon.tsx
│   │   ├── editable-image.tsx
│   │   ├── editable-logo.tsx
│   │   ├── editable-nav-item.tsx
│   │   ├── editable-text.tsx
│   │   ├── editable-wallet-button.tsx
│   │   ├── editor-panel.tsx
│   │   ├── onboarding-screen.tsx
│   │   └── text-card.tsx
│   │
│   ├── landing/                    # Landing page components
│   │   ├── about-section.tsx
│   │   ├── blog-section.tsx
│   │   ├── footer-section.tsx
│   │   ├── header.tsx
│   │   ├── hero-section.tsx
│   │   ├── how-to-buy-section.tsx
│   │   ├── marquee-section.tsx
│   │   ├── roadmap-section.tsx
│   │   └── tokenomics-section.tsx
│   │
│   ├── staking/
│   │   └── staking-panel.tsx       # Staking panel
│   │
│   └── whitepaper/
│       ├── format-card.tsx         # Format card
│       ├── module-selector.tsx     # Module selector
│       ├── template-card.tsx       # Template card
│       └── wp-language-selector.tsx # Language selector
│
├── hooks/
│   └── use-wallet.ts               # Solana wallet management hook
│
├── lib/
│   ├── firebase.ts                 # Firebase client config
│   ├── firebase-admin.ts           # Firebase Admin SDK
│   ├── installer.ts                # Installer logic
│   ├── i18n.ts                     # Translations and i18n utilities
│   ├── templates.ts                # Content templates
│   ├── avatar.ts                   # Avatar generation
│   └── utils.ts                    # General utilities (cn, etc)
│
├── types/
│   └── html2pdf.d.ts               # Types for html2pdf.js
│
├── public/                         # Static assets
├── styles/                         # Additional styles
│
├── .env.local                      # Environment variables (generated by installer)
├── .gitignore
├── next.config.mjs                 # Next.js config
├── package.json
├── tsconfig.json
├── postcss.config.mjs
└── components.json                 # shadcn/ui config
```

---

## Installation & Configuration

### Prerequisites

- **Node.js** 22+ (recommended)
- **npm** or **pnpm** as package manager
- **Firebase** account (for auth, DB, storage)
- **Helius** account or Solana RPC provider
- **Pinata** account (for IPFS)
- **OpenAI** account (for whitepaper generation)
- **Resend** account or other email provider
- Solana wallet with SOL for transaction fees (host wallet)

### Step 1: Clone the repository

```bash
git clone <repo-url>
cd tokenfun
```

### Step 2: Install dependencies

```bash
npm install
# or with pnpm
pnpm install
```

### Step 3: Initial configuration (Installer Wizard)

The platform includes an **Installer Wizard** that guides configuration in 3 steps:

1. Navigate to `http://localhost:3000/installer`
2. **Step 1**: Configure launcher name, language, admin email/password
3. **Step 2**: Configure database (Firebase/Supabase/MongoDB), email provider, RPC
4. **Step 3**: Review and generate installation

The installer automatically generates the `.env.local` file and saves configuration to `localStorage`.

### Step 4: Manual environment variable configuration

If you prefer manual configuration, edit `.env.local`:

```bash
# Database (Firebase)
INSTALLER_DATABASE_PROVIDER="firebase"
NEXT_PUBLIC_FIREBASE_API_KEY="your-api-key"
NEXT_PUBLIC_FIREBASE_AUTH_DOMAIN="your-project.firebaseapp.com"
NEXT_PUBLIC_FIREBASE_PROJECT_ID="your-project-id"
NEXT_PUBLIC_FIREBASE_STORAGE_BUCKET="your-project.firebasestorage.app"
NEXT_PUBLIC_FIREBASE_MESSAGING_SENDER_ID="your-sender-id"
NEXT_PUBLIC_FIREBASE_APP_ID="your-app-id"
FIREBASE_SERVICE_ACCOUNT_KEY='{"type":"service_account",...}'

# Email
EMAIL_PROVIDER="resend"
EMAIL_API_KEY="re_your-api-key"
EMAIL_FROM_EMAIL="info@yourdomain.com"

# Solana RPC
NEXT_PUBLIC_RPC_PROVIDER="helius"
NEXT_PUBLIC_RPC_URL="https://mainnet.helius-rpc.com/?api-key=your-api-key"

# Meteora Host (for admin rewards)
METEORA_HOST_SECRET_BASE64="base64-secret-key-of-your-host-wallet"
METEORA_HOST_RECEIVER="wallet-address-to-receive-rewards"
HOST_DASHBOARD_SECRET="secret-to-protect-admin-dashboard"

# Token Vanity Address
TOKEN_ADDRESS_SUFFIX="tkl"
TOKEN_ADDRESS_MAX_ATTEMPTS="250000"
TOKEN_ADDRESS_SUFFIX_REQUIRED="true"

# IPFS (Pinata)
PINATA_JWT="your-pinata-jwt"
PINATA_GATEWAY_BASE="https://gateway.pinata.cloud/ipfs/"

# OpenAI (for whitepapers)
OPENAI_API_KEY="sk-your-api-key"
```

### Step 5: Run in development

```bash
npm run dev
```

The application will be available at `http://localhost:3000`

### Step 6: Build for production

```bash
npm run build
npm run start
```

---

## API Endpoints

### POST /api/launch-token

**Main endpoint** - Handles multiple actions related to tokens and rewards.

#### Available actions:

| Action | Description | Authentication |
|--------|-------------|----------------|
| `create-wallet` | Generates new Solana wallet | Public |
| `check-balance` | Checks wallet balance | Public |
| `launch-token` | Creates token + pool on Solana | Requires auth + verified email |
| `get-rewards` | Gets pending rewards for a user | Requires ownerUid |
| `claim-rewards` | Claims rewards from all user's pools | Requires secretKey + ownerUid |
| `host-dashboard` | Gets stats for all pools | Requires x-admin-key header |
| `claim-host-rewards` | Claims partner fees from all pools | Requires x-admin-key header |
| `admin-all-rewards` | Global rewards view + earnings chart | Requires x-admin-key header |

#### Example: Launch token

```json
POST /api/launch-token
{
  "action": "launch-token",
  "secretKey": "base64-secret-key",
  "tokenConfig": {
    "tokenName": "My Token",
    "tokenSymbol": "MTK",
    "tokenUri": "https://.../metadata.json",
    "description": "Project description",
    "website": "https://mywebsite.com",
    "twitter": "@mytoken",
    "telegram": "https://t.me/mytoken",
    "image": "https://.../logo.png",
    "coverImage": "https://.../cover.png",
    "initialBuy": 0.5,
    "feePercent": 1,
    "decimals": 9,
    "totalSupply": 1000000000,
    "migrationThreshold": 50,
    "percentageSupplyOnMigration": 10,
    "creatorTradingFeePercent": 50,
    "creatorPermanentLockedPercent": 100,
    "partnerLiquidityPercent": 0,
    "partnerPermanentLockedPercent": 0,
    "poolCreationFee": 0
  },
  "user": {
    "uid": "user_123",
    "handle": "@myuser",
    "avatar": "https://.../avatar.png",
    "provider": "twitter"
  },
  "idToken": "firebase-id-token"
}
```

#### Successful response:

```json
{
  "success": true,
  "data": {
    "tokenAddress": "ABC123...tkl",
    "poolAddress": "DEF456...",
    "configAddress": "GHI789...",
    "signature": "tx-signature",
    "configSignature": "config-tx-signature",
    "tokenName": "My Token",
    "tokenSymbol": "MTK",
    "totalSupply": 1000000000,
    "decimals": 9,
    "bondingCurve": {
      "migrationQuoteThreshold": 50,
      "percentageSupplyOnMigration": 10,
      "migratesTo": "Meteora DAMM v2"
    }
  }
}
```

### POST /api/create

Public endpoint for creating tokens (proxy to launch-token with predefined action).

### GET /api/tokens?search=<query>

Lists all created tokens, descending order by date. Optional search.

### GET /api/token/ca/<address>

Gets token information and rewards breakdown by contract address or pool address.

### POST /api/token-metadata

Uploads token metadata to IPFS via Pinata. Accepts `FormData` with name, symbol, description, logo, and cover.

### POST /api/generate-whitepaper

Generates whitepaper with OpenAI GPT-4o-mini.

```json
{
  "tokenName": "My Token",
  "ticker": "MTK",
  "description": "Project description",
  "blockchain": "Solana",
  "totalSupply": "1000000000",
  "format": "document",
  "modules": 9,
  "language": "en"
}
```

Supported formats: `document`, `presentation`, `social`
Supported languages: `en`, `es`, `pt`, `fr`, `de`, `zh`, `ja`, `ko`

### POST /api/installer/env

Generates/updates the environment variable block in `.env.local` from the installer wizard.

---

## Environment Variables

| Variable | Required | Description |
|----------|----------|-------------|
| `INSTALLER_DATABASE_PROVIDER` | Yes | Provider: `firebase`, `supabase`, `mongodb` |
| `NEXT_PUBLIC_FIREBASE_API_KEY` | Yes* | Firebase API Key |
| `NEXT_PUBLIC_FIREBASE_AUTH_DOMAIN` | Yes* | Firebase Auth Domain |
| `NEXT_PUBLIC_FIREBASE_PROJECT_ID` | Yes* | Firebase Project ID |
| `NEXT_PUBLIC_FIREBASE_STORAGE_BUCKET` | Yes* | Firebase Storage Bucket |
| `NEXT_PUBLIC_FIREBASE_MESSAGING_SENDER_ID` | Yes* | Firebase Messaging Sender ID |
| `NEXT_PUBLIC_FIREBASE_APP_ID` | Yes* | Firebase App ID |
| `FIREBASE_SERVICE_ACCOUNT_KEY` | Yes* | Firebase Service Account JSON (Admin SDK) |
| `EMAIL_PROVIDER` | Yes | `resend`, `sendgrid`, `ses`, `mailgun`, `postmark` |
| `EMAIL_API_KEY` | Yes | Email provider API key |
| `EMAIL_FROM_EMAIL` | Yes | Sender email |
| `NEXT_PUBLIC_RPC_PROVIDER` | Yes | `helius`, `quicknode`, `alchemy`, `custom` |
| `NEXT_PUBLIC_RPC_URL` | Yes | Solana RPC URL |
| `METEORA_HOST_SECRET_BASE64` | Yes | Host wallet base64 secret key |
| `METEORA_HOST_RECEIVER` | No | Destination wallet for host rewards |
| `HOST_DASHBOARD_SECRET` | Yes | Secret to protect admin dashboard |
| `TOKEN_ADDRESS_SUFFIX` | No | Vanity suffix for token addresses |
| `TOKEN_ADDRESS_MAX_ATTEMPTS` | No | Max attempts for vanity address (default: 250000) |
| `TOKEN_ADDRESS_SUFFIX_REQUIRED` | No | If `true`, fails if vanity not found |
| `PINATA_JWT` | Yes | Pinata JWT for IPFS |
| `PINATA_GATEWAY_BASE` | No | Custom IPFS gateway |
| `OPENAI_API_KEY` | Yes | OpenAI API key |

*Required if `INSTALLER_DATABASE_PROVIDER=firebase`

---

## Database - Firebase

### Collections

#### `tokensList`
Stores all launched tokens.

```typescript
{
  name: string
  symbol: string
  tokenAddress: string
  poolAddress: string
  configAddress: string
  signature: string
  configSignature: string
  ownerUid: string
  ownerHandle: string
  ownerAvatar: string
  description: string
  website: string
  twitter: string
  telegram: string
  discord: string
  image: string
  coverImage: string
  initialBuy: number
  feePercent: number
  totalSupply: number
  creatorWallet: string
  creatorSecret: string  // base64 of secret key
  migrationQuoteThreshold: number
  percentageSupplyOnMigration: number
  creatorTradingFeePercentage: number
  creatorPermanentLockedLiquidityPercentage: number
  partnerLiquidityPercentage: number
  partnerPermanentLockedLiquidityPercentage: number
  poolCreationFee: number
  hostWallet: string
  usedConfigName: string
  createdAt: serverTimestamp()
}
```

#### `feedPosts`
Social feed posts.

```typescript
{
  posterHandle: string
  posterAvatar: string
  ownerHandle: string
  text: string
  imageUrl: string
  tokenName: string
  tokenSymbol: string
  tokenAddress: string
  tokenImage: string
  createdAt: Timestamp
}
```

---

## Bonding Curve System

The platform uses **Meteora Dynamic Bonding Curve SDK** to create liquidity pools with dynamic bonding curves.

### Configurable Parameters

| Parameter | Default | Description |
|-----------|---------|-------------|
| `migrationQuoteThreshold` | 50 SOL | Threshold to migrate to DAMM v2 |
| `percentageSupplyOnMigration` | 10% | Supply reserved for migration |
| `creatorTradingFeePercent` | 50% | % of fees going to creator |
| `creatorPermanentLockedPercent` | 100% | % of creator liquidity permanently locked |
| `partnerLiquidityPercent` | 0% | % of liquidity for partner |
| `partnerPermanentLockedPercent` | 0% | % permanently locked for partner |
| `poolCreationFee` | 0 lamports | Fixed fee per pool creation |
| `feePercent` | 1-5% | Dynamic fee per transaction |
| `tokenDecimals` | 6-9 | Token decimals |
| `totalSupply` | 1B | Total supply (100K - 1B) |

### Token Creation Flow

1. **Generate keypairs**: Config + Base Mint (with optional vanity suffix)
2. **Build curve config**: Bonding curve configuration
3. **Create config**: Transaction on Solana with `client.partner.createConfig`
4. **Create pool**: Transaction with `client.pool.createPool` or `createPoolWithFirstBuy`
5. **Initial buy** (optional): Automatic purchase in the same sequence
6. **Save to DB**: Persist metadata to Firebase `tokensList`

### Automatic Migration

When the pool reaches `migrationQuoteThreshold` (default 50 SOL):
- Liquidity automatically migrates to **Meteora DAMM v2**
- `percentageSupplyOnMigration` (default 10%) of supply is reserved
- Migration fee: `FixedBps25` (0.25%)

---

## Rewards System

### Creator Rewards

Token creators receive a percentage of fees generated by transactions in their pool:

- **Creator Trading Fee**: Configurable percentage (default 50%) of trading fees
- Accumulates in the pool and can be claimed at any time
- Requires `creatorSecret` (stored in Firebase when creating the token)

### Host/Partner Rewards

The host/administrator receives partner fees from all pools:

- **Partner Trading Fee**: Configurable percentage of trading fees
- Accumulable from all platform pools
- Claimable from admin dashboard or via API

### Claim Flow

1. Authenticated user clicks "Claim Rewards"
2. Backend searches all user's pools (by `ownerUid` and `creatorWallet`)
3. For each pool, gets fee breakdown via Meteora SDK
4. If pending fees exist, signs and sends claim transaction
5. Host also claims their partner fees automatically
6. Result: confirmed transactions + claimed amounts

### Multi-Wallet Support

The system supports multiple wallets stored in `localStorage`:
- `tokenlab_wallet_*`
- `tokenlab_imported_*`
- `tokenlab-wallet`

When claiming, pools are searched across all stored wallets and the correct keypair is used for each claim.

---

## Whitepaper Generator

Professional whitepaper generation system using **OpenAI GPT-4o-mini**.

### Features

- **8 languages**: English, Spanish, Portuguese, French, German, Chinese, Japanese, Korean
- **3 formats**:
  - `document`: Detailed professional document (3-4 paragraphs per section)
  - `presentation`: Concise slides (bullet points, 4-6 per slide)
  - `social`: Social media thread posts (tweet-length)
- **1-10 sections**: Configurable
- **PDF Export**: PDF generation via html2pdf.js

### Typical Sections

1. Executive Summary
2. Introduction
3. Problem Statement
4. Solution & Technology
5. Tokenomics
6. Roadmap
7. Team & Governance
8. Security & Audits
9. Legal Disclaimer

---

## Installer - Setup Wizard

The installer is a 3-step wizard that configures the platform without needing to edit files manually.

### Step 1: Basic Configuration

- Launcher name
- Default language (EN/ES)
- Token mode: new or existing
- Admin email and password

### Step 2: Technical Services

- **Database**: Firebase, Supabase, or MongoDB
- **Email**: Resend, SendGrid, SES, Mailgun, Postmark
- **RPC**: Helius, QuickNode, Alchemy, Custom

### Step 3: Review and Generate

- Full configuration summary
- Automatic `.env.local` generation
- Configuration saved to `localStorage`
- Redirect to admin dashboard

---

## Authentication

### Supported Methods

1. **Twitter OAuth**: Full authentication with OAuth 1.0a
2. **Google OAuth**: Via Firebase Auth
3. **Email/Password**: Firebase Auth with mandatory verification
4. **Telegram WebApp**: Auto-login via Telegram WebApp SDK

### Email Verification

For users registering with email/password, email verification is **mandatory** before launching tokens:

- Verifies the `email_verified` claim in the Firebase ID Token
- Forces token refresh to get the latest claim
- Returns 403 error if not verified

### Twitter Auth Flow

1. User clicks "Connect Twitter"
2. Redirect to `/api/auth/twitter` (init OAuth)
3. Twitter callback → `/api/auth/twitter/callback`
4. User authenticated with Firebase via Twitter credential
5. Twitter username obtained via `/api/auth/twitter/username`

---

## Internationalization (i18n)

The platform supports multiple languages with a key-based translation system.

### Supported Languages

| Code | Language |
|------|----------|
| `en` | English |
| `es` | Spanish |
| `pt` | Portuguese |
| `fr` | French |
| `de` | German |
| `zh` | Chinese |
| `ja` | Japanese |
| `ko` | Korean |

### Usage

```typescript
import { useI18n } from "@/components/i18n/language-provider"

const { t } = useI18n()
const title = t("create.title")
```

Translations are defined in `lib/i18n.ts`.

---

## Deployment

### Vercel (Recommended)

```bash
vercel
```

Environment variables to configure in Vercel:
- All listed in the Environment Variables section

### Docker

```dockerfile
FROM node:22-alpine
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .
RUN npm run build
EXPOSE 3000
CMD ["npm", "start"]
```

### Production Considerations

- Use paid RPC for better reliability (Helius paid plan)
- Configure strong `HOST_DASHBOARD_SECRET`
- Periodically rotate `METEORA_HOST_SECRET_BASE64`
- Enable rate limiting on public endpoints
- Monitor failed transactions

---

## Tech Stack

### Frontend
- **Next.js 16** - React framework with App Router
- **React 19** - UI library
- **TypeScript 5** - Type safety
- **Tailwind CSS 4** - Styling
- **shadcn/ui** - UI components (Radix UI primitives)
- **Lucide React** - Icons
- **React Icons** - Social network icons
- **Recharts** - Charts and graphs
- **Sonner** - Toast notifications
- **React Hook Form + Zod** - Form validation

### Blockchain
- **@solana/web3.js** - Solana interaction
- **@solana/spl-token** - Token management
- **@meteora-ag/dynamic-bonding-curve-sdk** - Dynamic bonding curves
- **bn.js** - BigInt operations

### Backend / Infrastructure
- **Firebase Admin SDK** - Auth, Firestore, Storage (server)
- **Firebase Client SDK** - Auth, Firestore, Storage (client)
- **OpenAI** - AI content generation
- **Pinata** - IPFS storage

### Email
- **Resend** / SendGrid / SES / Mailgun / Postmark - Transactional email

### Development
- **PostCSS** - CSS processing
- **ESLint** - Linting
- **Vercel Analytics** - Analytics

---

## Available Scripts

```bash
npm run dev       # Start development server
npm run build     # Build for production
npm run start     # Start production server
npm run lint      # Run ESLint
```

---

## Public API for Third Parties

The following endpoints are **public** (no session required):

- `POST /api/create` - Create token
- `GET /api/tokens?search=<query>` - List tokens
- `GET /api/token/ca/<address>` - Token info + rewards

They are designed for external integration and can be consumed by other applications.

---

## Credits

**Developed by:**
- [viainti](https://github.com/viainthi)
- [edinsoncs](https://github.com/edinsoncs)

**Key Technologies:**
- [Meteora](https://meteora.ag/) - Dynamic Bonding Curve SDK
- [Solana](https://solana.com/) - Blockchain
- [Firebase](https://firebase.google.com/) - Backend as a Service
- [Next.js](https://nextjs.org/) - React Framework
- [OpenAI](https://openai.com/) - AI Whitepaper Generator

---

## License

Property of viainti & edinsoncs. All rights reserved.
