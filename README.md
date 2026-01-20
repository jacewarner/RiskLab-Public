# RiskLab

This repository hosts the RiskLab documentation site built with
[Docusaurus](https://docusaurus.io/) for quantitative risk, markets, and
options knowledge. The docs pair narrative guidance with embedded calculators,
so each topic can move from theory to usable outputs without leaving the page.

## What RiskLab covers

**Markets**

Snapshots for equities, FX, and fixed income that frame how macro regimes,
microstructure, and policy flow through prices. Commodity Trading expands into
Energy Products (power, natural gas, crude, environmental products) with
physical vs. financial framing, storage optionality, basis risk, and delivery
constraints. Each page highlights what actually moves the tape, where liquidity
concentrates, and what can break when liquidity vanishes.

**Risk & analytics**

Volatility primers (historical vs. implied), correlation mechanics, VaR/ES
coverage (parametric, historical, and quadratic), and GMaR usage. The goal is
to connect model outputs to real risk decisions: what assumptions drive tail
losses, when correlations fail, and how to stress the inputs before you stress
the portfolio.

**Options**

Pricing model references (Black-76, Turnbull-Wakeman, Whaley, Bjerksund-
Stensland, Kirk spread, quanto) with embedded calculators, inputs guidance, and
Greek outputs. The docs focus on the tradeoffs behind each model and where
market structure forces deviations from textbook assumptions.

**Hedging playbooks**

Beta and delta hedge workflows with sizing logic, constraint handling, and
interpretation guidance. You get the difference between neutralizing risk and
neutralizing P&L noise, plus what breaks when basis moves or hedge ratios drift.

**Calculators and tooling**

Interactive components across risk, options, and fixed income (bond pricing,
duration, DV01, Treasury bills), plus scenario helpers and data-entry guides.
They are designed to surface intermediate steps, not just final numbers.

## Why RiskLab is different

- **Model clarity**: formulas are paired with the intuition for why they matter,
  plus the exact inputs the calculators expect.
- **Stress-first mindset**: each section is framed around regime shifts, jumps,
  and correlation breakdowns rather than just steady-state behavior.
- **Execution awareness**: pricing and hedging guidance calls out settlement
  conventions, liquidity cliffs, and real-world constraints.

## How the content is organized

- `docs/` holds the MDX knowledge base, organized by Markets and Risk sections.
- `src/components/` contains the reusable React calculators embedded in MDX.
- `src/pages/` powers the homepage and marketing-style content.

## Build and development

See `BUILD.md` for local development, production builds, Docker, and deployment
workflows.
