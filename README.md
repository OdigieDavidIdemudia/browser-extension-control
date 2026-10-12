# Browser Extension Control

A practical reference for governing browser extensions across a managed Chromium estate.

Passive discovery, risk enrichment, and default-deny enforcement on Chromium-based browsers via
Active Directory Group Policy. No third-party browser management tooling required.

**Live:** https://odigiedavididemudia.github.io/browser-extension-control/

**Narrative write-up:** [Your Users Have Given a Stranger the Keys to Your Bank Account](https://medium.com/@david.odigie.ide/your-users-have-given-a-stranger-the-keys-to-your-bank-account-e0599bdb1bce) — Medium

**Authors:** David Idemudia Odige ([@OdigieDavidIdemudia](https://github.com/OdigieDavidIdemudia)) &amp; Godwin Enendu ([@enendugodwin](https://github.com/enendugodwin))

## Contents

- The problem
- The design decision: default-deny
- Layer 1 — Discovery
- Layer 2 — Risk enrichment (reference implementation: ExtSafe)
- Layer 3 — Enforcement
- Validating enforcement
- Operating it
- Limitations and out of scope

## Design

Built to the personal-design-standard-v1 design system (copied into design/standard.json):

- **Variant:** neobrutalism structure x minimalism restraint
- **Type pairing:** technicalMono — Space Grotesk / Inter / JetBrains Mono
- Hard offset shadow applied to exactly two elements; callouts reduced to left rules;
  accent restricted to numerals, links and focus

## Note

This is a generalised reference implementation. It intentionally contains no
environment-specific identifiers, detection queries, policy paths, organisation names
or personnel, and is safe to reuse as a reference.
