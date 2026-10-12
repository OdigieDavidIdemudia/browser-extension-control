# Browser Extension Control

A practical reference for governing browser extensions across a managed Chromium estate.

Passive discovery, risk enrichment, and default-deny enforcement on Chrome and Edge via
Active Directory Group Policy. No third-party browser management tooling required.

**Live:** https://odigiedavididemudia.github.io/browser-extension-control/

## Contents

- The problem
- The design decision: default-deny
- Layer 1 — Discovery
- Layer 2 — Risk enrichment
- Layer 3 — Enforcement
- Validating enforcement
- Operating it
- Limitations and out of scope

## Note

This is a generalised reference implementation. It intentionally contains no
environment-specific identifiers, detection queries, policy paths, organisation names
or personnel, and is safe to reuse as a reference.
