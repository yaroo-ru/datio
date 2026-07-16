# Datio

**Datio** is an Ethereum-based escrow fundraising platform for transparent campaign funding, donor participation, moderator review, and contract-owner verification.

The project combines a Solidity smart contract with a Next.js frontend. Funds are held on-chain until a campaign is verified, cancelled, refunded, or withdrawn according to the contract rules.

## Live Project

- Website: https://datio.online
- Network: Ethereum Mainnet
- Smart contract: `0x7BE6dE3F306f12daadA256934b99d53B2F410830`
- Explorer: https://etherscan.io/address/0x7BE6dE3F306f12daadA256934b99d53B2F410830

## What Datio Solves

Traditional fundraising pages often depend on trust in the platform or campaign owner. Datio moves the critical financial flow into a public smart contract:

- donations are sent directly to the contract;
- campaign state is visible on-chain;
- withdrawals require campaign verification;
- cancelled campaigns allow donor refunds;
- platform fees are calculated by contract logic;
- admin verification is visibly marked in the interface.

## Core Flow

1. A creator opens a campaign with a name, metadata URI, and funding goal.
2. Donors send ETH to the campaign through the contract.
3. Verification can happen through moderator votes, community votes, or direct contract-owner approval.
4. After verification, the creator can withdraw available funds minus the contract fee.
5. If the campaign is cancelled before withdrawals, donors can claim refunds.
6. After funds are used, the creator can publish or update a report URI.

## Roles

| Role | Capabilities |
| --- | --- |
| Creator | Creates campaigns, withdraws after verification, updates report URI, can cancel before withdrawals. |
| Donor | Donates ETH, can cast a community verification vote, can claim refund after cancellation. |
| Moderator | Can vote to verify campaigns if granted moderator status on-chain. |
| Contract owner | Admin role that can manage moderators, pause the contract, cancel/suspend campaigns, force-verify campaigns, and manage fee shares. |

## Verification Modes

Datio distinguishes normal voting-based verification from contract-owner verification.

### Voting Verification

A campaign can be verified through moderator and community approval. The frontend shows moderator votes and community votes separately.

### Contract Owner Verification

The contract owner can call `ownerForceVerify(campaignId)`. This immediately moves a campaign to `Verified` without requiring the normal voting quorum.

The frontend marks this case with a dedicated badge such as:

```text
Verified by contract owner
```

This makes it clear to users why a verified campaign may have zero moderator or community votes.

## Smart Contract Features

- Campaign lifecycle: `Unverified`, `Verified`, `Cancelled`, `Completed`.
- ETH donations per campaign.
- Unique donor counter.
- Moderator voting.
- Community voting by donors.
- Owner force-verification.
- Refund claims after cancellation.
- Creator withdrawals after verification.
- 1% withdrawal fee.
- Fee share accounting.
- Pause and unpause controls.
- Campaign suspension controls.
- Ownership transfer.
- Reentrancy protection.

## Frontend Features

- Wallet connection through RainbowKit and wagmi.
- Ethereum Mainnet targeting.
- Campaign catalog with filtering and status cards.
- Campaign detail page with donation, voting, refund, withdrawal, and report actions.
- Dashboard for wallet activity.
- Admin panel for contract owner actions.
- Russian and English UI.
- Yandex.Metrika integration.
- Legal document downloads.

## Tech Stack

| Layer | Technology |
| --- | --- |
| Frontend | Next.js 14, React, TypeScript |
| Styling | Tailwind CSS |
| Wallets | RainbowKit, wagmi |
| Ethereum Client | viem |
| Smart Contract | Solidity `^0.8.x` |
| Network | Ethereum Mainnet |

## Project Structure

```text
app/                    Next.js App Router pages
components/             Shared UI components
contracts/              Solidity contracts
documents/              Markdown legal documents
hooks/                  Contract read/write hooks
lib/                    ABI, contract config, format helpers
public/                 Static assets and generated documents
scripts/                Deploy and document generation scripts
tests/                  Frontend smoke and Solidity tests
```

## Local Development

Install dependencies:

```bash
npm install
```

Create `.env.local`:

```env
NEXT_PUBLIC_CONTRACT_ADDRESS=0x7BE6dE3F306f12daadA256934b99d53B2F410830
NEXT_PUBLIC_ETHEREUM_RPC_URL=https://ethereum-rpc.publicnode.com
NEXT_PUBLIC_WALLETCONNECT_PROJECT_ID=your_walletconnect_project_id
NEXT_PUBLIC_APP_URL=https://datio.online
```

Run the development server:

```bash
npm run dev
```

Build for production:

```bash
npm run build
```

Run smoke tests and production build:

```bash
npm test
```

Generate DOCX legal documents:

```bash
npm run docs:docx
```

## Contract Safety Notes

- A creator cannot withdraw while the campaign is `Unverified`.
- Donors do not receive refunds automatically; after cancellation, each donor calls `claimRefund`.
- The contract owner cannot delete a deployed contract from Ethereum.
- A previous contract version can only be abandoned, paused, or removed from the frontend configuration.
- On-chain state is the source of truth; the frontend only displays and triggers contract calls.

## License

This repository is proprietary and unlicensed for public copying, redistribution, modification, or reuse without written permission.

See `LICENSE` for details.
