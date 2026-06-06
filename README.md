# Axel Eagle

**Smart Contract Auditor & Security Researcher**

Focused on finding critical vulnerabilities in live DeFi protocols across EVM and Solana ecosystems. I specialize in access control bypasses, oracle manipulation, and economic attack vectors.

---

## What I Do

- **Smart Contract Audits** — Line-by-line review of Solidity and Rust/Solana programs for protocols before and after launch
- **Vulnerability Research** — Discovering high-severity bugs in production DeFi protocols
- **Security Tooling** — Building tools for automated vulnerability detection and fuzz testing

---

## Notable Findings

| Severity | Protocol | Vulnerability | Impact |
|----------|----------|---------------|--------|
| **Critical** | Percolator (Solana) | Missing admin check in `UpdateAssetLifecycle` | Any user could hijack oracle authorities, manipulate mark prices, and drain insurance funds on mainnet |
| **High** | Percolator (Solana) | Missing owner verification in `fetchSlab` | Malicious RPC could feed spoofed account data, causing false liquidations and fund loss |
| **Medium** | Percolator (Solana) | Duplicated `getClientIp` missing fallback | Rate limit bypass — attackers get per-IP buckets while legitimate proxy users share one bucket |

> The critical `UpdateAssetLifecycle` finding was **confirmed exploited on live mainnet** before disclosure.

---

## Tech Stack

**Security:** Solidity, Rust (Solana/Anchor), Slither, Mythril, Foundry, Echidna, Halmos
**Languages:** TypeScript, Python, Go
**Infra:** EVM (Ethereum, Arbitrum, Base), Solana, Supabase, Docker

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

*"The best way to secure DeFi is to think like the attacker."*
