# Nostr Wallet Connect (NIP-47) in IronSig

**Purpose:**  
Integrate secure Lightning wallet actions (e.g., creating or paying invoices) into IronSig’s authentication and access-control system using the **Nostr Wallet Connect protocol** (NIP-47).  
This allows users to log in, prove control of a wallet, and perform microtransactions — all over decentralized relays with full user consent.

---

## 🔹 Overview

- **Protocol:** [NIP-47: Wallet Connect](https://github.com/nostr-protocol/nips/blob/master/47.md)
- **Event Kinds:**  
  - `23194` → Request  
  - `23195` → Response  
  - `13194` → Wallet Info / Supported Commands
- **Encryption:**  
  - Prefer **NIP-44** payloads; fallback to **NIP-04** if needed.  
  - Each request and response is encrypted using the app’s keypair and the wallet’s pubkey.

---

## 🔹 Example Connection URI


- `wallet_pubkey`: the Lightning wallet’s Nostr public key.  
- `relay`: the Nostr relay to send/receive events.  
- `secret`: symmetric key used to encrypt communication.  
- Optional: `lud16` for LN address association.

---

## 🔹 Initial MVP Commands

| Command | Description | Status |
|----------|--------------|--------|
| `make_invoice` | Request a Lightning invoice | ✅ |
| `get_info` | Retrieve wallet metadata | ✅ |
| `get_balance` | Get current wallet balance | 🟡 planned |
| `pay_invoice` | Pay a Lightning invoice | 🔒 gated / optional |

---

## 🔹 Demo Flow

1. **Connect Wallet**  
   - User pastes or scans NWC URI.  
   - IronSig stores wallet_pubkey, relay list, and encrypted secret.

2. **Handshake Test**  
   - IronSig sends a `get_info` request (`23194`).  
   - Wallet responds with `23195` confirming supported methods.

3. **Make Invoice**  
   - IronSig sends:  
     ```json
     { "method": "make_invoice", "params": { "amount": 1000, "description": "IronSig test" } }
     ```
   - Wallet returns BOLT11 invoice payload.  
   - App displays invoice in UI for verification.

---

## 🔹 Security & Privacy

- **No custodial keys** held by IronSig.  
- Each connection encrypted with unique secret per wallet.  
- **Relay redundancy**: multi-relay broadcast prevents censorship.  
- **User sovereignty**: wallet owner approves each command explicitly.

---

## 🔹 Integration Goals

- Seamless user experience: connect once, reuse connection securely.  
- Cross-wallet compatibility (Alby, Mutiny, Amethyst, etc.).  
- Foundation for **future license key enforcement and micropayments.**

---

## 🔹 Next Steps (Q4 2025 Sprint)

| Phase | Objective | Deliverable |
|-------|------------|-------------|
| Phase 1 | Implement connect + get_info | Working demo flow |
| Phase 2 | Add make_invoice / pay_invoice | MVP Lightning interaction |
| Phase 3 | UI polish & consent management | Live demo for CypherTank |
| Phase 4 | Open-source SDK release | 2026 |

---

## 🔹 References
- [NIP-47 Specification](https://github.com/nostr-protocol/nips/blob/master/47.md)
- [NIP-04: Encrypted Direct Message](https://github.com/nostr-protocol/nips/blob/master/04.md)
- [NIP-44: Encrypted Payloads](https://github.com/nostr-protocol/nips/blob/master/44.md)
- [Alby Docs: Wallet Connect](https://guides.getalby.com/)
