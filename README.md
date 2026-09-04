# Compound → Merkl Rewards Migration

This repository holds the **reward allocation datasets** used to distribute COMP
through [Merkl](https://app.merkl.xyz) after Compound's migration away from the
legacy on-chain reward contracts.

Each `*.merkl.json` file under [`snapshots/`](./snapshots) is a snapshot of
per-user COMP entitlements for a specific Compound version, network, and block
range. These files are the inputs consumed by Merkl to fund and open claim
campaigns.

```
snapshots/
└── rewards-<protocolVersion>-<network>-<rewardTokenPrefix>-<startBlock>-<endBlock>.merkl.json
```

> The migration changes **only the distribution layer**. The legacy reward
> **calculation methodology is unchanged** — allocations are derived
> deterministically from on-chain data and can be independently verified.

---

## Governance references

| Reference | Link |
| --------- | ---- |
| Forum post (migration overview, Season 1, FAQ, terms) | [comp.xyz — Stop Legacy On-Chain COMP Reward Accrual; Merkl Migration and Season 1 Update](https://www.comp.xyz/t/stop-legacy-on-chain-comp-reward-accrual-merkl-migration-and-season-1-update/8043) |
| Governance proposal (approves the on-chain action) | [Compound Governor — Proposal 602](https://www.tally.xyz/gov/compound/proposal/602?govId=eip155:1:0x309a862bbC1A00e45506cB8A802D1ff10004c8C0) |

---

## How the data in this repo is generated

**Generating repository:** [`woof-software/compound-aggregator`](https://github.com/woof-software/compound-aggregator) —
the open-source calculation scripts. See the
[`HOWTO.md`](https://github.com/woof-software/compound-aggregator/blob/main/HOWTO.md)
for how to run them and reproduce the snapshots in this repo.

---

## Campaigns / snapshots in this repo

| File | Version | Network | Market | Start block | End block | Accrued (COMP) | Distributed (COMP) |
| ---- | ------- | ------- | ------ | ----------- | --------- | -------------- | ------------------ |
| [`rewards-v3-mainnet-0xc00e94cb-15331586-25844234.merkl.json`](./snapshots/rewards-v3-mainnet-0xc00e94cb-15331586-25844234.merkl.json) | V3 | Ethereum | cUSDCv3 (`0xc3d6…cdc3`) | `15331586` | `25844234` | `TBD` | `TBD` |

---

## Merkl campaign links

The only official Merkl app URL is **[app.merkl.xyz](https://app.merkl.xyz)**.

### Previously accrued rewards (legacy migration)

| Version | Network  | Merkl campaign | Start time | End time |
| ------- | -------- | -------------- | ---------- | -------- |
| V2      | Ethereum | `TBD`          | `TBD`      | `TBD`    |
| V3      | Ethereum | `TBD`          | `TBD`      | `TBD`    |
| V3      | Arbitrum | `TBD`          | `TBD`      | `TBD`    |
| V3      | Optimism | `TBD`          | `TBD`      | `TBD`    |
| V3      | Base     | `TBD`          | `TBD`      | `TBD`    |
| V3      | Polygon  | `TBD`          | `TBD`      | `TBD`    |
| V3      | Unichain | `TBD`          | `TBD`      | `TBD`    |

### Season 1 (post-season claim campaign)

| Network  | Merkl campaign | Start time | End time |
| -------- | -------------- | ---------- | -------- |
| Ethereum | `TBD` (opens after Season 1 ends) | `TBD` | `TBD` |

---

## Season 1

Season 1 is the first fixed **90-day** Merkl-distributed COMP incentive campaign
on Ethereum V3 markets. Rewards **cannot be claimed during** the Season — they
accrue, a snapshot is published, and a Merkl claim campaign opens afterward.

| Market | Lending (COMP/day) | Borrowing (COMP/day) |
| ------ | ------------------ | -------------------- |
| USDC   | 55                 | 55                   |
| USDT   | 30                 | 30                   |
| WETH   | 10                 | 20                   |
| **Total** | | **200 COMP/day** |

- **Duration:** 90 days, starting at block `TBD` (`SEASON1_START_BLOCK`).
- **Max allocation:** **18,000 COMP**.
- **Claim window:** 30 days after the Season concludes.

---

## Claim windows

| Campaign type                 | Claim window after snapshot |
| ----------------------------- | --------------------------- |
| Previously accrued **V2**     | 60 days                     |
| Previously accrued **V3**     | 180 days                    |
| **Season** rewards            | 30 days                     |

Once a window closes, unclaimed COMP is returned by the TMC.

---

## Supported networks

**Migrated to Merkl:** Ethereum, Arbitrum, Optimism, Base, Polygon, Unichain.

**Excluded (still on legacy on-chain contracts):**

| Chain  | Legacy reward contract |
| ------ | ---------------------- |
| Mantle | `0xCd83CbBFCE149d141A5171C3D6a0F0fCCeE225Ab` |
| Linea  | `0x2c7118c4C88B9841FCF839074c26Ae8f035f2921` |