# Contributing to PayLink 🚀

Thank you for your interest in contributing to PayLink! We're building the no-code payment infrastructure for the Stellar ecosystem, and we'd love your help. This document will guide you through everything you need to get started.

---

## Table of Contents

- [Code of Conduct](#code-of-conduct)
- [Getting Started](#getting-started)
- [Development Workflow](#development-workflow)
- [Branch Naming Convention](#branch-naming-convention)
- [Commit Message Guidelines](#commit-message-guidelines)
- [Pull Request Process](#pull-request-process)
- [Project Structure](#project-structure)
- [Coding Standards](#coding-standards)
- [Testing](#testing)
- [Reporting Bugs](#reporting-bugs)
- [Suggesting Features](#suggesting-features)
- [Community & Support](#community--support)

---

## Code of Conduct

By participating in this project, you agree to uphold our community standards:

- Be respectful and inclusive in all interactions.
- Give constructive, specific feedback — not personal criticism.
- Welcome contributors of all experience levels.
- Focus discussions on ideas, not individuals.

Violations may be reported to the maintainers and will be addressed promptly.

---

## Getting Started

### Prerequisites

Make sure you have the following installed before contributing:

- **Node.js** v18 or higher
- **npm** v9 or higher
- **Git**
- A **Freighter Wallet** browser extension (for local testing)

### Local Setup

1. **Fork** the repository on GitHub.

2. **Clone** your fork:
   ```bash
   git clone https://github.com/YOUR_USERNAME/paylink.git
   cd paylink
   ```

3. **Add the upstream remote:**
   ```bash
   git remote add upstream https://github.com/yourusername/paylink.git
   ```

4. **Install dependencies:**
   ```bash
   npm install
   ```

5. **Configure environment variables** by creating a `.env.local` file in the root:
   ```
   NEXT_PUBLIC_STELLAR_NETWORK=testnet
   NEXT_PUBLIC_HORIZON_URL=https://horizon-testnet.stellar.org
   ```

6. **Start the development server:**
   ```bash
   npm run dev
   ```

   The app will be available at `http://localhost:3000`.

---

## Development Workflow

1. Sync your fork with the latest upstream changes before starting any work:
   ```bash
   git fetch upstream
   git checkout main
   git merge upstream/main
   ```

2. Create a new branch for your changes (see [Branch Naming Convention](#branch-naming-convention)).

3. Make your changes, following the [Coding Standards](#coding-standards).

4. Write or update tests where applicable (see [Testing](#testing)).

5. Commit your changes using the [Commit Message Guidelines](#commit-message-guidelines).

6. Push your branch and open a Pull Request.

---

## Branch Naming Convention

Use the following prefixes to keep branches organized:

| Prefix | Purpose | Example |
|---|---|---|
| `feat/` | New features | `feat/sep38-rate-quoting` |
| `fix/` | Bug fixes | `fix/freighter-connection-timeout` |
| `docs/` | Documentation updates | `docs/update-contributing-guide` |
| `chore/` | Maintenance tasks | `chore/upgrade-stellar-sdk` |
| `test/` | Adding or fixing tests | `test/checkout-flow-unit-tests` |
| `refactor/` | Code refactoring | `refactor/anchor-detection-logic` |

---

## Commit Message Guidelines

We follow the [Conventional Commits](https://www.conventionalcommits.org/) specification. Each commit message should be structured as:

```
<type>(<scope>): <short description>

[optional body]

[optional footer]
```

**Types:** `feat`, `fix`, `docs`, `chore`, `test`, `refactor`, `style`, `perf`

**Scope** refers to the area of the codebase affected (e.g., `checkout`, `dashboard`, `sep24`, `wallet`).

**Examples:**

```
feat(checkout): add geolocation-based anchor detection

fix(wallet): resolve Freighter API connection timeout on reload

docs(readme): update testnet environment variable instructions

chore(deps): upgrade @stellar/stellar-sdk to v12.1.0
```

Keep the subject line under 72 characters and write in the imperative mood ("add feature", not "added feature").

---

## Pull Request Process

1. Ensure your branch is up to date with `upstream/main` before opening a PR.

2. Fill out the PR template completely, including:
   - A clear description of what your change does and why.
   - Steps to reproduce (for bug fixes) or steps to test (for features).
   - Screenshots or screen recordings for UI changes.
   - Reference to any related issues (e.g., `Closes #42`).

3. All PRs must pass the following checks before review:
   - `npm run lint` — no linting errors
   - `npm run type-check` — no TypeScript errors
   - `npm run test` — all tests passing

4. Request a review from at least one maintainer.

5. Address all review comments before merging. Resolved conversations should be marked as resolved by the reviewer.

6. PRs are merged using **squash and merge** to keep the commit history clean.

---

## Project Structure

```
paylink/
├── app/                    # Next.js App Router pages and layouts
│   ├── dashboard/          # Merchant dashboard routes
│   └── pay/[linkId]/       # Public customer checkout pages
├── components/             # Reusable UI components
│   ├── checkout/           # Checkout flow components
│   └── dashboard/          # Dashboard-specific components
├── hooks/                  # Custom React hooks (e.g., ledger tracking)
├── lib/                    # Utility functions and Stellar SDK wrappers
│   ├── anchor/             # SEP-24 and SEP-38 integration logic
│   └── stellar/            # Horizon and network helpers
├── public/                 # Static assets
├── types/                  # Shared TypeScript type definitions
└── .env.local              # Local environment variables (not committed)
```

---

## Coding Standards

### General

- Write **TypeScript** for all new files — avoid `any` types.
- Prefer **functional components** and React Hooks.
- Keep components small and single-purpose.
- Co-locate related logic (hooks, types, utils) near the component that uses them.

### Styling

- Use **TailwindCSS** utility classes for all styling.
- Avoid inline styles and custom CSS files unless absolutely necessary.
- Follow the existing design system — do not introduce new color or spacing values outside Tailwind's config.

### Stellar & Anchor Logic

- All Stellar SDK calls must be wrapped in `try/catch` with meaningful error states surfaced to the UI.
- Never expose private keys or sensitive wallet data — always use Freighter's API for signing.
- Anchor interactions (SEP-24, SEP-38) should be isolated in `lib/anchor/` and not scattered across components.
- Default to **Testnet** in all development and PR environments. Mainnet usage is restricted to the production deployment.

---

## Testing

We use **Jest** and **React Testing Library** for unit and integration tests.

```bash
# Run all tests
npm run test

# Run tests in watch mode
npm run test:watch

# Check TypeScript types
npm run type-check

# Lint the codebase
npm run lint
```

### Guidelines

- Write tests for all new utility functions in `lib/`.
- Cover key user flows (e.g., payment link generation, checkout initiation) with integration tests.
- Mock Stellar SDK and Freighter API calls in tests — do not make real network requests in the test suite.
- Aim for meaningful coverage, not 100% line coverage at the expense of test quality.

---

## Reporting Bugs

Found a bug? Please [open an issue](https://github.com/yourusername/paylink/issues/new?template=bug_report.md) and include:

- A clear, descriptive title.
- Steps to reproduce the issue.
- Expected vs. actual behavior.
- Your environment (OS, browser, Node.js version, network: Testnet/Mainnet).
- Any relevant console errors or screenshots.

> ⚠️ **Security vulnerabilities** should **not** be reported in public issues. Please email the maintainers directly.

---

## Suggesting Features

Have an idea? We'd love to hear it. [Open a feature request](https://github.com/yourusername/paylink/issues/new?template=feature_request.md) and describe:

- The problem your feature would solve.
- Your proposed solution or approach.
- Any alternatives you've considered.
- Whether it aligns with the current [SCF Milestone Roadmap](README.md#-scf-milestone-roadmap-build-award-setup).

Feature requests are discussed openly and prioritized based on community feedback and roadmap alignment.

---

## Community & Support

- **GitHub Discussions** — for questions, ideas, and general conversation.
- **Issues** — for confirmed bugs and tracked feature requests.
- **Stellar Discord** — join the `#dev-paylink` channel for real-time discussion with the team.

We appreciate every contribution, whether it's a typo fix, a bug report, or a major feature. Thank you for helping build the future of frictionless global payments on Stellar. 🌍
