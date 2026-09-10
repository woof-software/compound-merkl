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

## Git LFS required

The large per-user audit datasets under [`audit/`](./audit) are stored with
[Git LFS](https://git-lfs.github.com). Install and initialize it **before**
cloning so you get the real files instead of small pointer stubs:

```
git lfs install
git clone git@github.com:woof-software/compound-merkl.git
```

If you already cloned without LFS, run `git lfs install` then `git lfs pull`.

---

## How the data in this repo is generated

**Generating repository:** [`woof-software/compound-aggregator`](https://github.com/woof-software/compound-aggregator) —
the open-source calculation scripts. See the
[`HOWTO.md`](https://github.com/woof-software/compound-aggregator/blob/main/HOWTO.md)
for how to run them and reproduce the snapshots in this repo.

**Address screening:** the 104 sanctioned/OFAC-flagged addresses listed in
[`blacklist.csv`](./blacklist.csv) are screened out and excluded from all allocations.

---

## Campaigns / snapshots in this repo

| File | Version | Network | Market | Start block | End block | Migrated to Merkl (COMP) |
| ---- | ------- | ------- | ------ | ----------- | --------- | ------------------------ |
| [`rewards-v2-mainnet-0xc00e94cb-7710671-25904935.merkl.json`](./snapshots/rewards-v2-mainnet-0xc00e94cb-7710671-25904935.merkl.json) | V2 | Ethereum | 18 markets | `7710671` | `25904935` | 40,419.457380 |
| [`rewards-v3-mainnet-0xc00e94cb-15331586-25935672.merkl.json`](./snapshots/rewards-v3-mainnet-0xc00e94cb-15331586-25935672.merkl.json) | V3 | Ethereum | 6 markets | `15331586` | `25935672` | 52,528.336790 |
| [`rewards-v3-arbitrum-0x354a6da3-87335214-503170370.merkl.json`](./snapshots/rewards-v3-arbitrum-0x354a6da3-87335214-503170370.merkl.json) | V3 | Arbitrum | 4 markets | `87335214` | `503170370` | 7,278.807262 |
| [`rewards-v3-optimism-0x7e7d4467-118406276-156654460.merkl.json`](./snapshots/rewards-v3-optimism-0x7e7d4467-118406276-156654460.merkl.json) | V3 | Optimism | 3 markets | `118406276` | `156654460` | 1,499.371428 |
| [`rewards-v3-base-0x9e1028f5-2197588-51059175.merkl.json`](./snapshots/rewards-v3-base-0x9e1028f5-2197588-51059175.merkl.json) | V3 | Base | 5 markets | `2197588` | `51059175` | 3,658.691270 |
| [`rewards-v3-polygon-0x8505b9d2-39412367-93468230.merkl.json`](./snapshots/rewards-v3-polygon-0x8505b9d2-39412367-93468230.merkl.json) | V3 | Polygon | 2 markets | `39412367` | `93468230` | 625.248629 |
| [`rewards-v3-unichain-0xdf78e4f0-9170496-58159371.merkl.json`](./snapshots/rewards-v3-unichain-0xdf78e4f0-9170496-58159371.merkl.json) | V3 | Unichain | 2 markets | `9170496` | `58159371` | 917.769048 |

**Total migrated to Merkl:** **106,927.681807 COMP** across 361,271 (V2) + 230,713 (V3) recipient entries.

> "Migrated to Merkl" is the **remaining** entitlement per snapshot — total COMP accrued
> over the period minus COMP already claimed through the legacy on-chain contracts. Each
> figure is reproducible from the matching [`audit/`](./audit) file
> (`total.remaining` / `allocationTotal`).

---

## Merkl campaign links

The only official Merkl app URL is **[app.merkl.xyz](https://app.merkl.xyz)**.

### Previously accrued rewards (legacy migration)

| Version | Network  | Merkl campaign | Start time            | End time              |
| ------- | -------- | -------------- | --------------------- | --------------------- |
| V2      | Ethereum | [Compound V2 Legacy Rewards — Ethereum](https://app.merkl.xyz/opportunities/240810265119821866) | 2026-09-10T22:00:00Z | 2026-11-10T22:00:00Z |
| V3      | Ethereum | [Compound V3 Legacy Rewards — Ethereum](https://app.merkl.xyz/opportunities/3376384779871485591) | 2026-09-10T22:00:00Z | 2027-03-10T22:00:00Z |
| V3      | Arbitrum | [Compound V3 Legacy Rewards — Arbitrum](https://app.merkl.xyz/opportunities/7568883014371172444) | 2026-09-10T22:00:00Z | 2027-03-10T22:00:00Z |
| V3      | Optimism | [Compound V3 Legacy Rewards — Optimism](https://app.merkl.xyz/opportunities/11731508864137097942) | 2026-09-10T22:00:00Z | 2027-03-10T22:00:00Z |
| V3      | Base     | [Compound V3 Legacy Rewards — Base](https://app.merkl.xyz/opportunities/16757461354196018516) | 2026-09-10T22:00:00Z | 2027-03-10T22:00:00Z |
| V3      | Polygon  | [Compound V3 Legacy Rewards — Polygon](https://app.merkl.xyz/opportunities/2840847057714888842) | 2026-09-10T22:00:00Z | 2027-03-10T22:00:00Z |
| V3      | Unichain | [Compound V3 Legacy Rewards — Unichain](https://app.merkl.xyz/opportunities/3642758435750332018) | 2026-09-10T22:00:00Z | 2027-03-10T22:00:00Z |

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