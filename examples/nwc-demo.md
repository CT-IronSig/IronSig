# NWC Demo (IronSig)

**Goal:** Show how IronSig uses Nostr Wallet Connect (NIP-47) to request Lightning actions from a user-controlled wallet.

## Prereq
- User exports an NWC URI from a compatible wallet (e.g., Alby, Mutiny).

## Flow
1) **Connect**  
   Paste/scan NWC URI → IronSig stores `wallet_pubkey`, `relays[]`, and an **encrypted** `secret`.

2) **Probe**  
   Send `get_info` (23194) → Receive 23195 with supported methods (or read kind 13194).

3) **Invoice**  
   Send `make_invoice(1000, "IronSig test")` → Receive 23195 with `bolt11` invoice → render in UI.

4) **(Optional) Pay**  
   If user opted in, send `pay_invoice(bolt11)` for sandbox demo.

## Notes
- Payloads encrypted via NIP-44 (fallback NIP-04).
- Multi-relay publishing for censorship resistance.
- No custodial keys; IronSig never holds user private keys.
