# Secure Notes Vault

A browser-based encrypted notes application built entirely with **vanilla HTML, CSS, and JavaScript** no frameworks, no backends, no dependencies. All encryption happens client-side using the native **Web Crypto API**.

---

##  Features

- ***AES-256-GCM Encryption*** — every note is encrypted before being stored in localStorage, with a fresh random IV per save. The authentication tag detects any ciphertext tampering.
- ***PBKDF2 Key Derivation*** — your master password is never stored. It is run through 200,000 iterations of PBKDF2-SHA-256 with a random 16-byte salt to derive the encryption key, which lives only in memory.
- ***Password Strength Scoring*** — a custom formula scores passwords on length, character diversity, and common pattern penalties, with four tiers: WEAK / FAIR / GOOD / STRONG.
- ***Brute-Force Protection*** — exponential backoff delays on failed attempts (1s → 8s → 16s → 32s), followed by an escalating lockout (10 min → 20 min → 40 min per lockout cycle).
- ***Metadata Checksum*** — unauthenticated localStorage fields (attempts, lockUntil) are sealed with a SHA-256 hash. Any DevTools tampering is detected on next load and triggers an immediate lockout.
- ***Attempts Mirrored Inside Vault*** — on successful login, failed attempt history is written into the encrypted payload, creating an authenticated record an attacker cannot erase.
- ***Hash-Chain Audit Log*** — every security event (login, failure, logout, expiry) is chained via SHA-256 so any log tampering breaks the chain and shows ✗ TAMPERED in the UI.
- ***Auto-Expiring Notes*** — notes can be set to expire after 1 minute, 1 hour, 24 hours, 7 days, or 30 days. Expired notes are purged automatically.
- ***Idle Session Timeout*** — after 5 minutes of inactivity the vault auto-logs out with a live countdown bar. A score penalty is applied.
- ***Clipboard Wipe Timer*** — copying text from a note starts a 30-second countdown, after which the clipboard is overwritten automatically.
- ***Security Scoring System*** — a running score tracks vault hygiene across all session events.

| Event | Score |
|---|---|
| Strong password set | +10 |
| Weak password set | -10 |
| Failed login attempt | -5 |
| Session timeout | -8 |
| Proper logout | +5 |

---

## Tech Stack

- **Vanilla HTML / CSS / JavaScript** — zero dependencies
- **Web Crypto API** — AES-GCM, PBKDF2, SHA-256 (all native browser)
- **localStorage** — encrypted blob storage only
- **IBM Plex Mono + Playfair Display** — via Google Fonts

---

## Usage

1. Download `secure-vault`
2. Open it in any modern browser
3. Set a master password to initialize your vault
4. Create, edit, and auto-expire encrypted notes

No server required. No install. No build step.
