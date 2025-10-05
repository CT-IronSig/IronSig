# Auth Demo (Bitcoin + Nostr Sign-in)

**Goal:** Passwordless login using Bitcoin (BIP-322) or Nostr (NIP-07).

## Flow
1) **Challenge**  
   Client fetches signed challenge:
   
IronSig Authentication
Domain: example.com
Nonce: <uuid>
Issued At: <iso8601>
Expires At: <iso8601>
Purpose: Prove control of this wallet for login only.

2) **Sign**
- Bitcoin wallet signs (BIP-322), OR
- Nostr signer signs (NIP-07).

3) **Verify**
Backend verifies signature → returns session/token.  
No passwords. No third-party IdP. No PII honeypot.
