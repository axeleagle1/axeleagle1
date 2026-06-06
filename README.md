# Hi i'm Axel

**Smart Contract Auditor & Security Researcher**

Finding critical vulnerabilities in live DeFi protocols across EVM and Solana ecosystems. I specialize in access control bypasses, oracle manipulation, economic attack vectors, and SDK correctness analysis.

---

## What I Do

- **Smart Contract Audits** — Line-by-line review of Solidity and Rust/Solana programs for protocols before and after launch
- **Vulnerability Research** — Discovering high-severity bugs in production DeFi protocols
- **Security Assessments** — Comprehensive on-chain analysis of protocol architecture, trust models, and invariant enforcement
- **SDK Auditing** — Reviewing client-side code for correctness bugs that cause self-inflicted financial loss
- **Adversarial Review** — Applying maximum skepticism to validate or reject findings against first-principles constraints

---

## Audit Portfolio

### Protocols Audited

| Protocol | Chain | Type | Findings |
|----------|-------|------|----------|
| **Percolator** | Solana | Perpetuals DEX | 3 (1 Critical, 1 High, 1 Medium) |
| **Hypernova** | Arbitrum | Crypto Prop Trading Firm | 4 Confirmed + 10 Exploit Hypotheses |
| **DepositWallet / Polymarket** | Polygon (EVM) | Prediction Market Wallet | 1 Medium |
| **3F Grunt** | EVM | DeFi Lending Protocol | 1 Low-Medium |
| **CollectorRoll** | Solana | Memecoin Reward Platform | 1 Critical (Design Flaw) |
| **BulkTrade** | EVM | DEX SDK | 10 Correctness Bugs |

---

## Notable Findings

### 🔴 Critical

| Protocol | Vulnerability | Impact |
|----------|---------------|--------|
| **Percolator** | Missing admin check in `UpdateAssetLifecycle` | Any user could hijack oracle authorities, manipulate mark prices, and drain insurance funds. **Confirmed exploited on mainnet.** |
| **CollectorRoll** | Shared inventory pool between memecoin reward loop and normal users | Memecoin activity drained commons inventory, causing platform-wide pack opening failures and downtime. Design flaw persists. |

### 🟠 High

| Protocol | Vulnerability | Impact |
|----------|---------------|--------|
| **Percolator** | Missing owner verification in `fetchSlab` | Malicious RPC could feed spoofed account data, causing false liquidations and fund loss |
| **Hypernova** | PayoutReserve is a single EOA holding $880K | Total loss of payout funds if single key compromised (core contracts protected by Safe 3-of-3 multisig) |
| **Hypernova** | Opaque off-chain risk engine | Pass/breach decisions not verifiable on-chain — backend manipulation enables arbitrary payouts |

### 🟡 Medium

| Protocol | Vulnerability | Impact |
|----------|---------------|--------|
| **DepositWallet** | ERC-20/ERC-1155 approvals persist after emergency session signer revocation | Compromised session signer can grant persistent approvals that survive the recovery procedure. Owner believes compromise is contained when it isn't. |
| **Percolator** | Duplicated `getClientIp` missing `x-real-ip` fallback | Rate limit bypass — attackers get per-IP buckets while legitimate proxy users share one bucket |
| **3F Grunt** | `syncRepaidStatus()` bypasses `mintToRepaidDelay` | Compromised consumer can mint unbacked YT tokens, wait for deadline, then redeem for ~90% yield theft. No principal at risk. |

### 🔵 Correctness / Reliability

| Protocol | Vulnerability | Impact |
|----------|---------------|--------|
| **BulkTrade** | Fixed-point UB on negative f64 (Rust SDK) | All sell-side orders through binary serialization fail with zero size. UB is UB regardless of downstream validation. |
| **BulkTrade** | Python SDK crashes on basic operations | `is_terminal()` on ERROR, `get_side()` missing attr, `generate_account()` tuple destructuring, missing `os` import |
| **BulkTrade** | NaN propagation from null mark prices | `Some(NaN)` instead of `None` — silently breaks all downstream comparisons |
| **BulkTrade** | Error blast marks all concurrent orders as failed | Single server error causes bot to retry all concurrent orders, creating duplicates |

---

## Methodology

My audit approach follows a structured process:

1. **Scope Mapping** — Understand protocol architecture, entry points, and trust boundaries
2. **Access Control Review** — Verify every privileged instruction validates the signer against the expected authority
3. **Data Flow Analysis** — Trace how user-supplied data flows through the program and where it gets written
4. **Economic Modeling** — Identify attack vectors where manipulating state can extract value
5. **Edge Case Testing** — Test boundary conditions, uninitialized accounts, and re-entrancy paths
6. **Adversarial Review** — Apply maximum skepticism. Reject findings that require timing assumptions, server faults, or externally-uninducible user behavior
7. **First-Principles Validation** — Verify architectural claims against client code before accepting or rejecting findings

---

## Tools

- **Manual code review** (primary)
- **Foundry** fuzzing and testing (EVM)
- **Anchor/Solana** program analysis
- **Slither** static analysis (EVM)
- **On-chain forensics** (Etherscan, Arbiscan, Solana Explorer)
- **Bytecode analysis** (function selector extraction, opcode profiling)

---

## Currently

- Open to audit engagements and security researcher roles
- Deep diving into cross-chain bridge security and MEV
- Contributing to open-source security tooling

---

## Links

- [Audit Findings](https://github.com/axeleagle1/audit-findings) — Detailed writeups of discovered vulnerabilities
- [Twitter/X](#) https://x.com/off_leblanc

---

*"The best way to secure DeFi is to think like the attacker — then prove yourself wrong."*
