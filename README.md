
# Soltix — Decentralized Ticketing Platform

Soltix is a next-generation decentralized ticketing platform that resolves the systemic flaws of traditional, centralized ticketing architectures—such as ticket scalping, bot manipulation, counterfeiting, and the lack of authentic digital ownership[cite: 1]. Built on the high-throughput **Solana blockchain**, Soltix issues every event ticket as a Non-Fungible Token (NFT), providing attendees with verifiable, tamper-proof proof of ownership[cite: 1]. 

By employing a pragmatic, high-performance hybrid architecture, Soltix couples on-chain cryptographic settlement with sub-second off-chain operational efficiency.

---

## 📄 Research Paper & Academic Context
This project was submitted in May 2026 in partial fulfillment of the requirements for the award of the degree of **Bachelor of Technology (B.Tech) in Computer Science and Engineering** at **Sister Nivedita University, Newtown Kolkata**[cite: 1].

* **Full Research Paper**: **[Read the Soltix Thesis Paper](https://drive.google.com/file/d/1yJfljnzlxbvw-MZYv_nsMbJWXs-GCX-f/view?usp=sharing)**[cite: 1]

---

## 🚀 Key Features

* **True Digital Ownership (NFTs)**: Tickets are uniquely tokenized as Solana NFTs using standard verified collections, mitigating forgery and granting buyers a transferable digital asset.
* **Permanent Metadata Storage**: Ticket assets, seat data, and event details are permanently and immutably anchored to **Arweave** via the **Irys** network, eliminating reliance on vulnerable, centralized file hosts.
* **Trustless On-Chain Auctions**: Secondary resales are securely managed via a bespoke **Anchor-based decentralized auction system**. Program Derived Accounts (PDAs) act as an escrow system, providing trustless bidding, atomic settlement, and counterparty protection.
* **High-Speed Cryptographic Gate Entry**: Features an offline challenge-response validation scheme. Attendees sign a time-constrained nonce using their cryptographic wallet to prevent duplicate entry attacks at mass venues within milliseconds, bypassing slow, live on-chain check-ins.
* **Web2.5 Onboarding Experience**: Uses **Dynamic** to manage Web3 authentication, seamlessly supporting both embedded/social wallets and native extensions like Phantom and Solflare.

---

## 🛠 System Architecture & Stack

Soltix avoids the pitfalls of purely on-chain execution (high gas/latency) and fully centralized systems (opacity/scalping) through a modular hybrid design:

### 1. Functional Layers
* **Frontend UI**: Built using **Next.js** and **TypeScript**, responsive across mobile and desktop clients.
* **Blockchain Registry**: Deployed on the **Solana Devnet** to govern ownership, provenance, and final financial settlement.
* **Smart Storage Layer**: Uses **Metaplex Umi** and **Candy Machine V3** protocols for streamlined primary ticket minting, alongside **Irys/Arweave** for decentralized metadata.
* **Off-Chain Backend**: Powered by **Supabase (PostgreSQL)** to index operational, high-frequency, transient data such as live auction indices, event logs, and real-time ticket redemption/scan history.

### 2. Workflow Diagrams (As documented in Chapter 4)
The system strictly decouples transactions into distinct operational flows:
* **Authentication** (Dynamic Client + Wallet Adapter)
* **Event Creation & Metadata Upload** (Irys Integration)
* **Primary Event Ticket Minting** (Candy Machine V3)
* **On-Chain Escrow Auction** (Custom Rust Anchor Code)
* **Rapid Gate Validation** (Offline QR Cryptographic Nonce Challenge)

---

## 📦 Core Configuration Data

Primary ticket minting properties and structural parameters map directly into standardized configurations. Standard asset profiles are managed dynamically via high-level SDK tools like **Codama**, ensuring type-safe serialization and deserialization across the Rust (Anchor) and TypeScript codebases.

---

## 📊 Evaluation & Performance Metrics
As detailed in Chapter 5, empirical results indicate that Soltix scales effectively against traditional Web3 architectures:
* **Sub-second Response Latency**: Offloading transient operational variables to Supabase enables near-instant updates.
* **Economic Efficiency**: Custom Anchor auction vaults ensure users only settle on-chain during definitive ownership state changes, eliminating network fees for losing bids.
* **High-Throughput Validation**: Gate scanning functions smoothly even in low or fluctuating connectivity via local signature checks.

---

## 📝 License and Usage
This repository contains the full implementation blueprints, smart contracts, and web interfaces developed for the Soltix Undergraduate Thesis at Sister Nivedita University[cite: 1]. All work is credited to the respective authors and academic department[cite: 1].
