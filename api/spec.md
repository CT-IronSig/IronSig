# IronSig API (Draft)

High-level endpoints for the MVP covering **passwordless authentication** and **Nostr Wallet Connect (NIP-47)**.

---

## 🔐 Authentication

### POST /api/auth/nonce
Return a signed challenge message used for wallet-based login.

**Response (text block):**
IronSig Authentication
Domain: <your-domain>
Nonce: <uuid>
Issued At: <iso8601>
Expires At: <iso8601>
Purpose: Prove control of this wallet for login only.

**Notes**
- Bind `Domain` to the frontend host to mitigate phishing.  
- Short TTL (5–10 minutes). Deny replay.  

---

### POST /api/auth/verify
Verify a Bitcoin (BIP-322) or Nostr (NIP-07) signature over the challenge.

**Body (one of):**
```json
{ "address": "btcAddress", "signature": "base64|hex", "message": "<challenge>" }
```
```json
{ "pubkey": "npub...", "signature": "base64|hex", "message": "<challenge>" }
```
```json
{ "ok": true, "session": "jwt-or-cookie", "user_id": "..." }
```
---

### POST /api/nwc/connect
Parse and store a Nostr Wallet Connect (NWC) URI.  
Persists: `wallet_pubkey`, `relays[]`, **encrypted** `secret`, and `scopes[]`.

**Body:**
```json
{ "uri": "nostr+walletconnect://<wallet_pubkey>?relay=wss://...&secret=<hex>[&lud16=...]" }
```
**Response:**
```json
{ "ok": true, "wallet_pubkey": "npub...", "relays": ["wss://..."], "scopes": ["get_info","make_invoice"] }
```
Notes
Encrypt secret at rest (KMS or OS keyring).
Never log raw secrets or decrypted payloads.
Allow users to edit the relay list.

