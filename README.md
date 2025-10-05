## IronSig — Bitcoin-Native Authentication (with Nostr Wallet Connect)

**Mission:** Replace passwords with Bitcoin and Nostr signatures.  
IronSig integrates **Nostr Wallet Connect (NIP-47)** to let apps request Lightning wallet actions directly — enabling **censorship-resistant login, payments, and license verification** in one secure flow.

---

## 🔹 Why It Matters
- Passwords are insecure and Big Tech “passwordless” solutions are centralized.  
- Bitcoin and Nostr provide a **sovereign identity layer** owned by users.  
- IronSig bridges **identity + payments** to power the next generation of peer-to-peer applications.

---

## 🔹 MVP Scope
- **Authentication:** BIP-322 (Bitcoin) + NIP-07 (Nostr).  
- **NWC (NIP-47):** Connect wallet, request invoices, optional payments.  
- **Developer SDK:** Easy integration for web apps and enterprise systems.  

---

## 🔹 Architecture Overview
- **Frontend:** User connects wallet via QR or NWC URI.  
- **Backend:** Nostr client signs **23194** requests, listens for **23195** responses, encrypts with NIP-44 (fallback NIP-04).  
- **Storage:** Encrypted NWC secrets and relay lists per user.

---

## 🔹 Security & Sovereignty
- No custodial keys.  
- Multi-relay publishing for censorship resistance.  
- Minimal scopes and explicit consent UI.

---

## 🔹 Resources
- [Whitepaper](docs/white%20paper.md)
- [Nostr Wallet Connect Overview](docs/nwc.md) *(coming soon)*
- [Authentication Demo Flow](examples/auth-demo.md)
- [API Spec](api/spec.md)

---

## 🔹 Project Status
- **Stage:** MVP build in progress  
- **Entity:** IronSig LLC (Wyoming)  
- **Funding:** $50K self-funded seed; seeking $250–500K for acceleration  
- **Focus:** Bitcoin-native Security-as-a-Service for identity and access control  

---

## 🔹 License
[MIT License](LICENSE)
(project overview)
