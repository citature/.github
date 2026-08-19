# Security Policy

## Reporting a vulnerability

Please **do not** open a public issue for a security vulnerability.

Report it privately via GitHub's [security advisory](https://docs.github.com/en/code-security/security-advisories/guidance-on-reporting-and-writing-information-about-vulnerabilities/privately-reporting-a-security-vulnerability)
flow on the affected repository (Security → Report a vulnerability). Include the
affected component, reproduction steps, and impact.

We aim to acknowledge within a few business days and to coordinate a fix and
disclosure timeline with you.

## Scope

citature serves public-domain US federal records through an MCP server and a set
of [Apify](https://apify.com/citature) actors. The underlying data is public by
law and carries no secrets — so the reports we care most about are the ones that
compromise **integrity or provenance** rather than confidentiality:

- **Provenance tampering** — anything that lets a citation, retrieval timestamp,
  or source locator be forged, or that makes a returned record cite a source it
  did not come from. citature's entire contract is that a claim can be
  re-fetched from the upstream government source; a break in that chain is the
  highest-severity class of bug we have.
- **MCP server** — tool-call handling, input validation on tool arguments,
  authorization between callers, and anything that lets one caller observe or
  affect another's requests.
- **Actor and pipeline code** — command construction, credential handling, and
  the ingestion path from the upstream sources (FEC, USASpending, SAM.gov,
  Grants.gov).
- **Supply chain** — the release path for actors and the MCP server, and any
  dependency that reaches the retrieval or citation layer.

Out of scope: the content of the upstream federal records themselves. If a
government source publishes something incorrect, that is an upstream data issue
rather than a vulnerability — open a normal issue and we will document it as a
coverage caveat.

## A note on personal data

citature is entity-level only and ships no individual-person products. If you
find a surface that resolves or profiles a natural person beyond what the
underlying public record already discloses, report it here — we treat that as a
security issue, not a feature request.

## Reach of this policy

This file lives in `citature/.github`, so GitHub applies it as the default to
citature repositories that do not carry their own `SECURITY.md`. That default
covers **public** repositories only; private repositories need the policy in the
repository itself. Today the practical reach is this repository, and the file is
here so the disclosure path already exists when that changes.
