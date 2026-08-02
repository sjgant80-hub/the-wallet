# The Wallet — a sovereign agent-wallet that cannot overspend

**▶ Live: https://sjgant80-hub.github.io/the-wallet/**

An agent that doesn't *have* a budget — it **is** one. An Ed25519 identity that carries a **signed
action-ceiling it cannot cross**, refuses forged or over-budget actions, and forks into a lineage tree
where credit flows upstream, bounded. The token-leak, made **impossible by construction**.

This is the **LINEAGE** socket of the Seal (§27 of the private framework): *"split the content-address
from a real Ed25519 keypair · verifyLineage()."* It's organ #1 of the anatomy cascade — and it **wraps
the-room's seats**: each seat gets a signed per-turn action-budget, so a runaway seat is *refused*, not
just logged after the fact.

## The four things it proves

- **The ceiling is real.** `authorize()` gates every action by capability + budget. A 100-budget wallet
  *cannot* spend 101 — the 101st action is refused. A 2.2M-cost action against a 100k budget is refused
  outright. Not a policy you can forget to apply — a property of the object.
- **Signatures have teeth.** Every authorization is an Ed25519-signed token binding {action, cost,
  spent, budget}. A flipped signature or a tampered body is rejected by verification.
- **Delegation attenuates.** A parent can grant a child only a *subset* of its capabilities and a budget
  no larger than its remaining — you cannot delegate what you do not hold.
- **Lineage is verifiable + bounded.** A fork is the child's wallet; its birth-certificate is
  parent-signed and checkable. Value realized downstream mints upstream credit that *converges* (bounded
  by value·φ) — provenance appreciates as it's forked, but the payout never runs away.

## Proven — `node test.mjs`, real Ed25519 (node:crypto), zero tokens, 23/23

The leak-impossible test, forged/tampered rejection, attenuation, verifiable fork-lineage, bounded
upstream credit, a reference monitor that never runs an unauthorized action, 5k-fuzz (spent never exceeds
total, nothing throws), determinism.

## Honest scope

The reference monitor (`guard`) is a **cooperative** sandbox — it guards code that goes *through* it (the
room's seats, an agent loop). The real cross-trust boundary is the **signed token**: a receiver verifies
it without trusting the caller. This is not a hardware/kernel sandbox against a determined attacker with
source access; it is a capability + budget discipline with cryptographic authorizations.

## Files

`wallet.mjs` (the pure capability/budget/lineage kernel — crypto injected) · `crypto-node.mjs` (real
Ed25519 for Node/tests) · `test.mjs` (the 23/23 gate) · `index.html` (the live PWA — mint, spend to the
ceiling, forge-and-reject, fork a lineage; real WebCrypto Ed25519, demo-signer fallback) · `sw.js` +
`manifest.webmanifest` (offline). No custody — the secret key never leaves the page. No cosmology on the
surface (per the framework's public/private seam).

```bash
node test.mjs                 # the proof (real Ed25519)
python -m http.server 8080    # then open http://localhost:8080  (modules + WebCrypto need http)
```
