# Datio

**Datio** is a Web3 fundraising and escrow platform where campaign funds are held in an Ethereum smart contract until the campaign passes verification.

The goal is simple: make fundraising more transparent, reduce blind trust, and give donors a clear on-chain way to see what happened with their money.

## Links

| Item | Link |
| --- | --- |
| Website | https://datio.online |
| Network | Ethereum Mainnet |
| Smart contract | `0x7BE6dE3F306f12daadA256934b99d53B2F410830` |
| Etherscan | https://etherscan.io/address/0x7BE6dE3F306f12daadA256934b99d53B2F410830 |

## What The Project Is

Datio is a public fundraising interface connected to a smart contract.

A campaign creator can open a fundraising campaign. Donors can send ETH. The contract holds the funds. The creator cannot withdraw funds until the campaign receives verification.

Verification can happen through:

- moderator approval;
- donor/community voting;
- direct contract-admin verification.

If a campaign is cancelled before withdrawals, donors can claim their funds back from the contract.

## Why It Matters

Most online fundraising platforms require users to trust the platform, the campaign owner, or a payment processor. Datio moves the critical money flow into transparent contract logic.

This gives users and investors a clearer system:

- funds are visible on-chain;
- campaign status is visible on-chain;
- withdrawal rules are enforced by the smart contract;
- refunds are handled by contract logic;
- admin verification is marked in the interface;
- platform fees are transparent.

## User Journey

### 1. Campaign Catalog

Users can browse all campaigns from the contract.

Each campaign card shows:

- campaign status;
- creator address;
- amount raised;
- goal;
- donor count;
- moderator votes;
- community votes;
- verification method.

If a campaign was verified directly by the contract admin, the card displays a clear `admin verified` mark.

### 2. Campaign Page

Each campaign has a detailed page with:

- campaign title and metadata;
- current status;
- total raised;
- available payout estimate;
- donor count;
- voting state;
- report URI;
- action buttons depending on the connected wallet.

Possible actions include:

- donate;
- vote as donor;
- vote as moderator;
- verify as contract admin;
- withdraw funds as creator;
- claim refund after cancellation;
- update report URI after withdrawals.

### 3. Dashboard

The dashboard shows wallet-related activity:

- campaigns created by the connected wallet;
- campaigns where the wallet donated;
- amount raised by related campaigns;
- donor counters;
- donation activity;
- active and verified campaign counts.

There are no off-chain profiles. The dashboard is based on contract data.

### 4. Admin Page

The contract owner has a dedicated admin area for contract-level actions:

- add or remove moderators;
- pause or unpause the contract;
- suspend or unsuspend campaigns;
- cancel campaigns;
- force-verify campaigns;
- manage fee shares;
- claim platform fees.

## Verification Model

### Community Verification

Donors can support campaign verification with a community vote. This makes real donors part of the trust process.

### Moderator Verification

Verified moderators can vote to approve campaigns. Moderator votes are shown separately from community votes.

### Contract Admin Verification

The contract owner can call `ownerForceVerify`.

This immediately moves the campaign to `Verified`. The interface marks this as contract-admin verification so users understand why a campaign may be verified without normal vote counts.

## Refund Model

If a campaign is cancelled before funds are withdrawn, donors can call `claimRefund` and receive their contribution back.

Refunds are not automatically pushed to every donor. Each donor claims their own refund from the contract. This avoids gas-limit issues and keeps the refund process explicit.

## Revenue Model

Datio uses a transparent smart-contract fee model.

The current contract fee is:

```text
1% from withdrawals
```

The fee is collected only when verified campaign funds are withdrawn. This aligns platform revenue with successful verified fundraising activity.

## Investor View

Datio is positioned as infrastructure for transparent fundraising, creator funding, emergency campaigns, community financing, and Web3-native escrow flows.

### Key Strengths

- On-chain escrow instead of blind trust.
- Public campaign lifecycle.
- Built-in refund path.
- Clear fee model.
- Multirole verification.
- Admin verification is visibly disclosed.
- No dependency on internal user profiles for core state.
- Works with standard Ethereum wallets.

### Market Direction

The fundraising market continues moving toward transparency, faster global payments, and reduced platform custody. Datio fits this direction by making the escrow and verification layer public and programmable.

### Expansion Potential

Potential future directions:

- campaign deadlines;
- automatic refund eligibility after deadline;
- stablecoin support;
- organization pages;
- campaign categories;
- reputation for creators and moderators;
- analytics for donors and investors;
- multichain deployment;
- API access for partner platforms;
- institutional campaign verification.

## Current Product Status

Datio currently includes:

- live website;
- deployed Ethereum Mainnet contract;
- campaign creation;
- ETH donations;
- campaign verification;
- donor voting;
- moderator voting;
- contract-admin verification;
- refunds after cancellation;
- creator withdrawals;
- campaign dashboard;
- owner admin panel;
- Russian and English interface;
- public legal documents.

## Smart Contract Summary

The contract controls the main campaign lifecycle:

```text
Unverified -> Verified -> Completed
Unverified -> Cancelled -> Refunds
```

Important rules:

- creators cannot withdraw while a campaign is unverified;
- creators cannot vote for their own campaign;
- donors can refund only after cancellation;
- owner can cancel campaigns before withdrawals;
- owner can verify campaigns directly;
- withdrawals include a contract-defined fee.

## Trust And Transparency

Datio does not ask users to trust a hidden database for the core financial state. The important values are contract-readable:

- campaign creator;
- campaign status;
- total raised;
- total withdrawn;
- donor count;
- votes;
- user contribution;
- paused or suspended state.

The frontend is an interface to the contract, not the source of truth.

## License

This project is proprietary.

Copying, redistribution, modification, commercial reuse, or creating derivatives is not allowed without written permission.

See `LICENSE` for details.
