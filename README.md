# 🌌 Aidorap - Decentralized AI Agent Marketplace & Direct Aid on Stellar

> **Aidorap is a cutting-edge, decentralized AI agent marketplace and direct aid distribution platform built on the Stellar blockchain, featuring Soroban smart contracts, an immersive cosmic UI theme, offline PWA capabilities, and enterprise-grade security.**

The platform unites artificial intelligence creators, traders, liquidity underwriters, and humanitarian donors. Users can discover, mint, simulate, test, and trade autonomous AI agents while accessing direct-to-recipient claim-link aid distribution with zero friction, verifiable on-chain provenance, and ultra-low transaction fees (~0.00001 XLM).

---

## 📋 Table of Contents

- [Project Overview](#-project-overview)
  - [Key Benefits](#key-benefits)
  - [Target Users](#target-users)
- [Setup Instructions](#%EF%B8%8F-setup-instructions)
  - [Prerequisites](#prerequisites)
  - [Quick Start](#quick-start)
  - [Environment Setup](#environment-setup)
  - [Running Tests & Quality Gates](#running-tests--quality-gates)
  - [Network Configuration](#network-configuration)
- [Features](#-features)
- [Architecture & System Design](#%EF%B8%8F-architecture--system-design)
  - [System Flow](#system-flow)
  - [Multi-Repository Ecosystem](#multi-repository-ecosystem)
- [Project Structure](#-project-structure)
- [Usage Examples](#-usage-examples)
  - [1. Connecting a Stellar Wallet](#1-connecting-a-stellar-wallet)
  - [2. Minting an AI Agent with IPFS Metadata](#2-minting-an-ai-agent-with-ipfs-metadata)
  - [3. Calculating Technical Trading Indicators](#3-calculating-technical-trading-indicators)
  - [4. Staking & Yield Calculations](#4-staking--yield-calculations)
  - [5. Scanning Contract Security & Compliance](#5-scanning-contract-security--compliance)
- [Deployment](#-deployment)
  - [Production Next.js Build](#production-nextjs-build)
  - [Docker Setup](#docker-setup)
  - [Docker Compose](#docker-compose)
- [CI/CD Pipeline](#-cicd-pipeline)
- [Helpful Links](#-helpful-links)
- [Contribution Guidelines](#-contribution-guidelines)
- [License](#-license)
- [Support & Community](#-support--community)

---

## 🚀 Project Overview

**Aidorap** transforms how autonomous AI agents are created, validated, governed, and monetized on the **Stellar network**. By combining Soroban smart contracts, decentralized IPFS pinning, and high-frequency WebSocket telemetry, Aidorap provides a trustless environment for deploying AI agents and routing transparent humanitarian assistance.

The platform eliminates intermediaries in both algorithmic agent commerce and charitable giving, ensuring that transactions settle immutably on-chain in 3–5 seconds with near-zero network fees.

### Key Benefits

| Benefit | Description |
|---|---|
| **Autonomous Agent Marketplace** | Buy, sell, and commission verifiable AI agents with full feature filtering, Algolia search, and rating systems. |
| **On-Chain Provenance** | Immutable genealogical tree and cryptographic audit trail tracking every agent iteration, derivation, and action. |
| **Direct Aid Distribution** | Zero-friction donor-to-recipient claim links with AI-verified need assessment and transparent on-chain delivery. |
| **Soroban Staking Pools** | Lock up protocol assets in smart contract staking pools with dynamic APY tiers and automated yield distribution. |
| **Real-Time Telemetry** | High-performance WebSocket streaming dashboard providing live agent metrics, error logs, and execution traces. |
| **Cosmic Trading Terminal** | Virtualized order book and candlestick trading charts with built-in technical indicators (SMA, EMA, RSI, MACD, Bollinger Bands). |
| **Progressive Web App (PWA)** | Complete offline resilience with Workbox runtime caching, background sync, and native Web Push notifications. |
| **Enterprise Security & Audit** | Built-in vulnerability scanner, automated compliance checks, and multi-tier security scoring. |

### Target Users

- **AI Creators & Engineers**: Developers building autonomous models, plugins, and bots who want decentralized monetization, versioning, and provenance tracking.
- **Traders & Investors**: Participants analyzing agent performance metrics, trading agent shares, and monitoring price movements through technical charts.
- **Liquidity Underwriters & Stakers**: Protocol participants providing liquidity to earn yield through Soroban staking contracts.
- **Donors & Humanitarian Organizations**: Philanthropists distributing direct, verifiable aid to unbanked recipients globally without intermediaries.
- **Platform Governors**: Token and policy holders proposing, debating, and voting on protocol policies and parameters.

---

## 🛠️ Setup Instructions

### Prerequisites

Ensure you have the following installed on your machine:

- **Node.js**: `20.x` or higher ([Download Node.js](https://nodejs.org/))
- **npm**: `10.x` or higher (bundled with Node.js)
- **Git**: For version control
- **Stellar Wallet Extension / App**:
  - [Freighter](https://www.freighter.app/) (Recommended browser extension)
  - [Albedo](https://albedo.link/) (Web-based popup signer)
  - [Ledger Hardware Wallet](https://www.ledger.com/) (For cold storage signing)

---

### Quick Start

Get up and running in under 5 minutes:

```bash
# 1. Clone the repository
git clone https://github.com/rodiat7/Aidorap.git
cd Aidorap

# 2. Install dependencies
npm install

# 3. Copy the environment configuration template
cp .env.example .env

# 4. Start the local Next.js development server
npm run dev
```

Open [http://localhost:3000](http://localhost:3000) in your browser to view the application.

---

### Environment Setup

#### Option 1: Automated Template Setup
```bash
cp .env.example .env
```

#### Option 2: Manual Environment Configuration
Configure your `.env` file in the project root:

```env
# API Gateway
NEXT_PUBLIC_API_URL=http://localhost:3001
NEXT_PUBLIC_ENVIRONMENT=development

# Feature Flags & Analytics (Optional)
# NEXT_PUBLIC_ENABLE_BETA_FEATURES=false
# NEXT_PUBLIC_ANALYTICS_ID=your-analytics-id

# Agent Telemetry WebSocket (Optional — built-in mock stream used if omitted)
# NEXT_PUBLIC_TELEMETRY_WS_URL=ws://127.0.0.1:3456
# TELEMETRY_WS_PORT=3456

# Metrics & Prometheus (Server-side only)
# METRICS_PROMETHEUS_BASE_URL=http://localhost:9090
# METRICS_OTEL_PROMETHEUS_BASE_URL=http://localhost:9464

# Stellar Network RPC Overrides (Optional)
# NEXT_PUBLIC_DEFAULT_STELLAR_NETWORK=testnet
# NEXT_PUBLIC_STELLAR_TESTNET_URL=https://horizon-testnet.stellar.org
# NEXT_PUBLIC_STELLAR_MAINNET_URL=https://horizon.stellar.org
```

| Variable | Description | Default / Example |
|---|---|---|
| `NEXT_PUBLIC_API_URL` | Base URL of the backend REST service | `http://localhost:3001` |
| `NEXT_PUBLIC_ENVIRONMENT` | Active application environment | `development` / `production` |
| `NEXT_PUBLIC_TELEMETRY_WS_URL` | WebSocket URL for live agent telemetry | `ws://127.0.0.1:3456` |
| `METRICS_PROMETHEUS_BASE_URL` | Prometheus HTTP endpoint for metric scraping | `http://localhost:9090` |
| `NEXT_PUBLIC_DEFAULT_STELLAR_NETWORK` | Default active Stellar network | `mainnet`, `testnet`, or `futurenet` |

> **Note**: Variables prefixed with `NEXT_PUBLIC_*` are exposed to the client-side bundle. Never store secret keys, database credentials, or signer seeds in these variables.

---

### Running Tests & Quality Gates

Verify code correctness, linting rules, and bundle health:

```bash
# Run all unit and integration test suites with Jest
npm test

# Run tests in watch mode
npm run test:watch

# Generate code coverage report
npm run test:coverage

# Run ESLint across all TypeScript and React files
npm run lint

# Start the standalone telemetry WebSocket server
npm run telemetry:ws

# Analyze production bundle size with source-map-explorer
npm run analyze
```

---

### Network Configuration

Aidorap interacts with Stellar and Soroban across multiple deployment environments:

| Network | Horizon URL | Soroban RPC URL | Network Passphrase | Purpose |
|---|---|---|---|---|
| **Testnet** | `https://horizon-testnet.stellar.org` | `https://soroban-testnet.stellar.org` | `Test SDF Network ; September 2015` | Public testing, staging, and contract validation |
| **Futurenet** | `https://horizon-futurenet.stellar.org` | `https://rpc-futurenet.stellar.org` | `Test SDF Future Network ; October 2022` | Experimental Soroban protocol releases |
| **Mainnet (Pubnet)** | `https://horizon.stellar.org` | Custom RPC Provider | `Public Global Stellar Network ; September 2015` | Production agent trading and aid settlement |

---

## ⚡ Features

- 🧙 **Agent Minting Wizard**: Step-by-step workflow with schema validation, tag categorization, and IPFS / NFT.storage asset pinning.
- 🔍 **Discovery & Search**: Full-text instant search powered by Algolia, combined with multi-attribute filtering by rating, price, and category.
- 📈 **Trading Terminal**: High-performance candlestick charts, virtualized order book, and live indicators (SMA, EMA, RSI, MACD, Bollinger Bands).
- 🔒 **Multi-Wallet Support**: One-click connection for **Freighter**, **Albedo**, and **Ledger** hardware wallets with multi-wallet linking and session delegation.
- 📡 **Real-Time Telemetry**: WebSocket event pipeline delivering sub-second execution traces, status flags, and error logs.
- 🧪 **Simulation Runner & Benchmarking**: Sandbox runner to test agent outputs against test cases and calculate automated quality scores.
- 🌿 **Cryptographic Provenance**: Visual dependency tree tracing origin models, forks, derivations, and historical hashes on Stellar.
- 🛡️ **Security Scanner & Auditing**: Static vulnerability scanning, Stellar compliance scoring, badge issuance, and exportable markdown audit reports.
- 💰 **Soroban Staking Engine**: Dynamic APY interest models, tiered lockups, and one-click compound yield staking.
- 🏛️ **Decentralized Governance**: Proposal drafting, quorum monitoring, and on-chain vote tabulation for protocol parameters.
- 🤝 **Multi-Tier Affiliate Program**: Multi-tier referral tracking, direct aid claim links, QR code generation, and social share modals.
- 🌐 **11-Language Localization**: Full internationalization via `i18next` supporting English, Spanish, French, German, Chinese, Japanese, Arabic, Russian, Portuguese, and Korean.
- 📱 **Progressive Web App (PWA)**: Installable web application with service workers, stale-while-revalidate offline caching, and push notifications.

---

## 🏛️ Architecture & System Design

### System Flow

```
┌───────────────────────────────────────────────────────────────────┐
│                    Aidorap Web Client (Next.js)                   │
│   (App Router · Cosmic Design System · Redux Toolkit · Zustand)  │
└──────────────┬───────────────────┬──────────────────┬─────────────┘
               │                   │                  │
         REST / HTTP         WebSockets        Freighter / Albedo
               │                   │                  │
               ▼                   ▼                  ▼
┌─────────────────────────┐ ┌──────────────┐ ┌──────────────────────┐
│       Aidorap API       │ │ Telemetry WS │ │   Stellar Wallets    │
│  (Next.js Route Handlers│ │   Service    │ │ (Freighter / Albedo /│
│   & Analytics Engine)   │ │ (Port 3456)  │ │       Ledger)        │
└──────────────┬──────────┘ └──────────────┘ └──────────┬───────────┘
               │                                        │
               │            Signed XDR / RPC            │
               └───────────────────┬────────────────────┘
                                   ▼
┌───────────────────────────────────────────────────────────────────┐
│                    Stellar Network & Storage                      │
│                                                                   │
│  ┌─────────────────────────┐          ┌────────────────────────┐  │
│  │   Soroban Smart RPC     │          │      IPFS Storage      │  │
│  │  • Staking Pools        │          │  • Metadata Schemas    │  │
│  │  • Provenance Lineage   │          │  • Model Weights       │  │
│  │  • Governance Engine    │          │  • Verification Hashes │  │
│  └─────────────────────────┘          └────────────────────────┘  │
└───────────────────────────────────────────────────────────────────┘
```

### Multi-Repository Ecosystem

| Repository | Role | Stack |
|---|---|---|
| [Aidorap](https://github.com/rodiat7/Aidorap) | Core Web Frontend & Marketplace Client | Next.js 14, React 18, TypeScript, Tailwind |
| [aidorap-api](https://github.com/SourceXXL/aidorap-api) | Backend Orchestration & Microservices Gateway | Node.js, Express / Fastify, PostgreSQL |
| [aidorap-contracts](https://github.com/SourceXXL/aidorap-contracts) | Smart Contract Protocols | Rust, Soroban SDK, Stellar Core |

---

## 📂 Project Structure

```
Aidorap/
├── app/                              # Next.js App Router
│   ├── analytics/                    # Analytics dashboard and time-series charts
│   ├── api/                          # Next.js API route handlers
│   │   ├── affiliates/               # Affiliate programs & commission tracking
│   │   ├── analytics/                # Aggregated metrics endpoints
│   │   ├── bug-reports/              # Bug reporting CRUD
│   │   ├── metrics/                  # Prometheus metrics scraper
│   │   ├── security/                 # Security scan triggers & reports
│   │   ├── simulations/              # Simulation runner execution
│   │   ├── telemetry/                # Telemetry ingestion endpoint
│   │   └── waitlist/                 # Waitlist signups & leaderboards
│   ├── bug-report/                   # Bug submission form with screenshot uploads
│   ├── create/                       # Agent Minting Wizard page
│   ├── dashboard/                    # Affiliate & referral metrics dashboard
│   ├── governance/                   # On-chain proposals and voting
│   ├── marketplace/                  # Agent discovery, search, and catalogue
│   ├── portfolio/                    # User holdings and agent performance
│   ├── provenance/                   # Cryptographic lineage explorer
│   ├── security/                     # Vulnerability scanner and compliance audits
│   ├── settings/                     # Multi-wallet linking and notifications
│   ├── simulations/                  # Agent sandbox simulation suite
│   ├── staking/                      # Soroban staking pool interface
│   ├── telemetry/                    # Real-time WebSocket monitoring dashboard
│   ├── testing/                      # Test case builder and benchmark runner
│   ├── trading/                      # Technical analysis trading terminal
│   ├── waitlist/                     # Pre-launch waitlist registration
│   ├── layout.tsx                    # Root layout with global providers
│   ├── page.tsx                      # Cosmic hero landing page
│   └── globals.css                   # Tailwind directives and custom animation classes
├── components/                       # Shared UI and composite components
│   ├── analytics/                    # MetricsOverview, TimeSeriesChart
│   ├── context/                      # StellarWalletProvider
│   ├── metrics/                      # OptimizedMetricLineChart, MetricSeriesTable
│   ├── portfolio/                    # AgentCard
│   ├── providers/                    # ClientProviders, ThemeModeProvider, ReduxProvider
│   ├── simulations/                  # SimulationRunner, SimulationLogs, SimulationCard
│   ├── trading/                      # OptimizedTradingChart, VirtualizedTradingTable
│   ├── AgentMintingWizard.tsx        # Multi-step agent creation wizard
│   ├── BugReportForm.tsx             # Bug submission modal with file dropzone
│   ├── ConnectWallet.tsx             # Dropdown wallet connector (Freighter/Albedo/Ledger)
│   ├── Navigation.tsx                # Responsive navigation header
│   ├── NetworkSwitcher.tsx           # Mainnet / Testnet / Futurenet selector
│   ├── NotificationDemo.tsx          # Web push notification demonstration
│   ├── PWAInstall.tsx                # PWA install prompt banner
│   └── VirtualizedList.tsx           # High-performance react-window list
├── features/                         # Modular domain packages
│   ├── affiliate-dashboard/          # Commission breakdown, charts, payout management
│   ├── agent-discovery/              # Algolia search service and filter hooks
│   ├── agent-telemetry/              # WebSocket listeners and role-based filtering
│   ├── agent-testing/                # Benchmark dashboards and quality scorer
│   ├── agent-versioning/             # Semantic versioning and changelog diffs
│   ├── governance/                   # Proposal creation and vote signing
│   ├── plugins/                      # Dynamic plugin manager with sandboxing
│   ├── provenance/                   # Provenance explorer and audit graphs
│   ├── recommendations/              # Collaborative and algorithmic recommendation engines
│   ├── referral-sharing/             # Social share modals, QR code generator, claim links
│   ├── security/                     # Static analysis scanner and compliance engines
│   ├── soroban/                      # useSorobanContract hook
│   └── wallet/                       # WalletManager, SessionRecovery, DelegationDashboard
├── hooks/                            # Custom React hooks (useNotifications, usePWA, redux)
├── i18n/                             # Translation JSON files (11 supported languages)
├── lib/                              # Core utilities, blockchain bridges, and math
│   ├── analytics/                    # Horizon subscription and time-series aggregation
│   ├── governance/                   # Stellar governance proposal logic
│   ├── metrics/                      # Prometheus metrics exporter and CSV downloaders
│   ├── security/                     # Vulnerability database, scanner, compliance scoring
│   ├── soroban/                      # Soroban client, contract specs, transactions wrapper
│   ├── staking/                      # Yield math, tier multipliers, APY calculators
│   ├── telemetry/                    # WebSocket client, event sanitizer, role filters
│   ├── trading/                      # Technical indicators (SMA, EMA, RSI, MACD, Bollinger)
│   ├── wallet/                       # Multi-wallet linking and session delegation services
│   ├── cache-manager.ts              # Multi-tier TTL cache with localStorage fallback
│   ├── ipfs.ts                       # IPFS & NFT.storage metadata pinning
│   ├── notifications.ts              # Web Push dispatcher and permission manager
│   ├── pwa-utils.ts                  # Service worker registration and sync queues
│   ├── stellar-constants.ts          # Network configurations and passphrases
│   └── stellar.ts                    # Wallet connectors and Horizon account fetchers
├── public/                           # Static assets, manifests, and service workers
│   ├── icons/                        # PWA icons (72x72 to 512x512)
│   ├── humans.txt                    # Authors and contributors attribution
│   ├── manifest.json                 # Web App Manifest
│   ├── offline.html                  # Offline fallback page
│   ├── robots.txt                    # Search crawler indexing rules
│   └── sw.js                         # Production service worker with Workbox caching
├── scripts/                          # Build and auxiliary development scripts
│   ├── generate-icons.js             # Canvas-based PWA icon generator
│   ├── setup-pwa.sh                  # PWA environment setup script
│   └── telemetry-ws-server.mjs       # Mock WebSocket server for telemetry streaming
├── store/                            # Global state management
│   ├── redux/                        # Redux Toolkit store (search, apiMetrics)
│   ├── slices/                       # referralSlice
│   ├── useBonusStore.ts              # Zustand store for trading volume bonuses
│   └── useSimulationStore.ts         # Zustand store for agent simulations
├── tests/                            # Jest unit, integration, and E2E test suites
│   ├── __tests__/                    # 16 unit test suites (analytics, wallet, security, soroban)
│   ├── e2e/                          # End-to-end wallet interaction tests
│   ├── pwa.test.tsx                  # PWA service worker and manifest verification
│   └── trading-chart-performance.test.tsx # High-load chart rendering benchmarks
├── types/                            # Global TypeScript declarations
├── next.config.js                    # Next.js configuration with runtime PWA caching
├── package.json                      # Dependencies and npm scripts
├── tailwind.config.cjs               # Tailwind design system tokens
└── tsconfig.json                     # Strict TypeScript compiler options
```

---

## 💻 Usage Examples

### 1. Connecting a Stellar Wallet

Connect to Freighter, Albedo, or Ledger and fetch account balances:

```typescript
import { connectFreighter, getAccountBalances } from '@/lib/stellar';
import { DEFAULT_NETWORK } from '@/lib/stellar-constants';

async function handleConnect() {
  try {
    // 1. Prompt user to sign in with Freighter
    const wallet = await connectFreighter();
    console.log('Connected Public Key:', wallet.publicKey);

    // 2. Fetch XLM and asset balances on the active network
    const balances = await getAccountBalances(wallet.publicKey, DEFAULT_NETWORK);
    console.log('Account Balances:', balances);
  } catch (error) {
    console.error('Wallet connection failed:', error);
  }
}
```

---

### 2. Minting an AI Agent with IPFS Metadata

Pin an agent specification to IPFS and prepare the Soroban mint transaction:

```typescript
import { uploadMetadataToIPFS } from '@/lib/ipfs';
import { SorobanClient } from '@/lib/soroban/client';

async function mintAgent() {
  const agentMetadata = {
    name: 'Cosmic Arbitrageur v2',
    description: 'Autonomous high-frequency liquidity arbitrage agent.',
    author: 'GB...STELLAR_KEY',
    version: '1.0.0',
    capabilities: ['arbitrage', 'liquidity-provision', 'market-making'],
    createdAt: new Date().toISOString(),
  };

  // 1. Upload metadata to IPFS via NFT.storage
  const ipfsHash = await uploadMetadataToIPFS(agentMetadata);
  console.log('Pinned to IPFS:', ipfsHash);

  // 2. Invoke the Soroban agent minting contract
  const client = new SorobanClient('testnet');
  const txResult = await client.invokeContract({
    contractId: 'CA...AGENT_FACTORY_CONTRACT_ID',
    method: 'mint_agent',
    args: [agentMetadata.name, ipfsHash],
  });

  console.log('Agent successfully minted. Tx Hash:', txResult.hash);
}
```

---

### 3. Calculating Technical Trading Indicators

Compute indicators (RSI, MACD, Bollinger Bands) for agent trading charts:

```typescript
import {
  calculateRSI,
  calculateMACD,
  calculateBollingerBands,
} from '@/lib/trading/indicators';

const closingPrices = [120, 122, 121, 124, 128, 127, 130, 132, 131, 135, 138, 136, 140];

// Relative Strength Index (14 periods)
const rsiValues = calculateRSI(closingPrices, 14);
console.log('Latest RSI:', rsiValues[rsiValues.length - 1]);

// Moving Average Convergence Divergence (12, 26, 9)
const macd = calculateMACD(closingPrices, 12, 26, 9);
console.log('MACD Line:', macd.macdLine, 'Signal:', macd.signalLine);

// Bollinger Bands (20 periods, 2 std dev)
const bands = calculateBollingerBands(closingPrices, 20, 2);
console.log('Upper:', bands.upper, 'Middle:', bands.middle, 'Lower:', bands.lower);
```

---

### 4. Staking & Yield Calculations

Calculate dynamic staking rewards based on lockup period and amount:

```typescript
import { calculateStakingReward, getTierMultiplier } from '@/lib/staking/engine';

const principalXLM = 5000;
const lockupDays = 90;

// Determine tier multiplier based on staked volume
const multiplier = getTierMultiplier(principalXLM);

// Calculate projected return with interest compounding
const reward = calculateStakingReward({
  amount: principalXLM,
  durationDays: lockupDays,
  baseAPY: 0.085, // 8.5% Base APY
  tierMultiplier: multiplier,
});

console.log(`Estimated Returns: +${reward.estimatedRewardXLM} XLM (${reward.effectiveAPY}% APY)`);
```

---

### 5. Scanning Contract Security & Compliance

Execute automated vulnerability scans and generate security badges:

```typescript
import { runSecurityScan } from '@/lib/security/scanner';
import { generateSecurityReport } from '@/lib/security/report';

async function auditContract(contractSource: string) {
  // 1. Run static analysis scanner
  const scanResults = await runSecurityScan(contractSource);
  console.log(`Found ${scanResults.vulnerabilities.length} security notices`);

  // 2. Generate compliance badges and full report
  const report = generateSecurityReport(scanResults);
  console.log('Security Score:', report.overallScore);
  console.log('Badges:', report.badges.map((b) => b.label));
}
```

---

## 🚀 Deployment

### Production Next.js Build

Build and start the optimized production Next.js server:

```bash
# Compile client bundles, server routes, and PWA service workers
npm run build

# Start the Node.js production server
npm run start
```

---

### Docker Setup

Build and run Aidorap inside a standalone container:

```bash
# 1. Build the Docker image
docker build -t aidorap:latest .

# 2. Run the container on port 3000
docker run -d \
  --name aidorap-app \
  -p 3000:3000 \
  -e NEXT_PUBLIC_API_URL=http://localhost:3001 \
  aidorap:latest
```

---

### Docker Compose

Run the entire Aidorap ecosystem (frontend, backend, and cache):

```bash
# Start all containers in the background
docker-compose up -d

# View real-time container logs
docker-compose logs -f

# Stop and remove containers
docker-compose down
```

---

## 🔄 CI/CD Pipeline

The project uses GitHub Actions for continuous integration, code auditing, and build validation:

| Workflow | Trigger | Tasks Executed |
|---|---|---|
| **`ci.yml`** | Push / Pull Request on `main` | • ESLint check (`npm run lint`)<br>• TypeScript compilation check (`tsc --noEmit`)<br>• Jest unit and integration tests (`npm test`)<br>• Production Next.js build verification (`npm run build`) |
| **`security.yml`** | Scheduled weekly / PR | • Dependency vulnerability check (`npm audit`)<br>• CodeQL static security analysis |

### Local Quality Gate Check

Ensure all quality gates pass locally before pushing code:

```bash
# 1. Typecheck
npx tsc --noEmit

# 2. Linting
npm run lint

# 3. Unit and integration tests
npm test

# 4. Production build
npm run build
```

---

## 🔗 Helpful Links

### Project Documentation
- [Code of Conduct](./CODE_OF_CONDUCT.md) — Community standards and enforcement guidelines
- [Contributing Guidelines](./CONTRIBUTING.md) — Step-by-step contribution and branch rules
- [Development Roadmap](./ROADMAP.md) — Upcoming milestones, feature releases, and goals
- [GitHub Issues Bootstrap](./GITHUB_ISSUES_BOOTSTRAP.md) — Ready-to-use good first issues for contributors
- [License](./LICENSE) — MIT License agreement

### External Resources
- [Stellar Developer Documentation](https://developers.stellar.org/) — Official Stellar network docs and guides
- [Soroban Smart Contracts](https://soroban.stellar.org/docs) — Smart contract development on Stellar
- [Freighter API Documentation](https://docs.freighter.app/) — Browser extension wallet integration
- [Next.js Documentation](https://nextjs.org/docs) — Next.js App Router and SSR guides
- [Tailwind CSS](https://tailwindcss.com/docs) — Utility-first CSS documentation

---

## 🤝 Contribution Guidelines

We welcome community contributions from developers, designers, and security researchers!

### Getting Started

1. **Fork the repository** on GitHub.
2. **Clone your fork** locally:
   ```bash
   git clone https://github.com/<your-username>/Aidorap.git
   cd Aidorap
   ```
3. **Install dependencies**:
   ```bash
   npm install
   ```
4. **Create a feature branch**:
   ```bash
   git checkout -b feat/your-feature-name
   ```

### Development Workflow

```bash
# 1. Make your code modifications
# 2. Ensure test suites pass
npm test

# 3. Run linter
npm run lint

# 4. Commit changes using Conventional Commits
git commit -m "feat(marketplace): add volume filter to agent discovery"

# 5. Push branch to GitHub
git push origin feat/your-feature-name
```

### Definition of Done

Before submitting a Pull Request, verify:
- [x] Code compiles without TypeScript errors (`npx tsc --noEmit`).
- [x] All existing and new tests pass (`npm test`).
- [x] ESLint runs with zero errors (`npm run lint`).
- [x] Code adheres to the Cosmic UI theme styling.
- [x] Pull Request description references related issues.

---

## 📄 License

This project is licensed under the **MIT License** — see the [LICENSE](./LICENSE) file for details.

---

## 💬 Support & Community

- 🐛 **Bug Reports & Issues**: [GitHub Issues](https://github.com/rodiat7/Aidorap/issues)
- 💬 **Feature Discussions**: [GitHub Discussions](https://github.com/rodiat7/Aidorap/discussions)
- 📧 **Direct Email**: [support@aidorap.com](mailto:support@aidorap.com)
- 🌐 **Official Website**: [https://aidorap.com](https://aidorap.com)
- 🐦 **Twitter / X**: [@Aidorap](https://twitter.com/Aidorap)
- 💬 **Community Discord**: [Join Discord](https://discord.gg/aidorap)

<div align="center">

**Built with ❤️ for decentralized AI innovation and transparent global aid.**

[⭐ Star us on GitHub](https://github.com/rodiat7/Aidorap) • [🤝 Contribute](./CONTRIBUTING.md) • [📧 Contact](mailto:support@aidorap.com)

</div>
