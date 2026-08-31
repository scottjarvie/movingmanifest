---
id: MOV-WO-011
title: Let a chosen AI file private move photos through the same trusted evidence system
execution: proposed
audit: not-audited
cards: MOV-0043 MOV-0044 MOV-0045 MOV-0046
created: 2026-08-30
updated: 2026-08-30
proposed-by: Codex
---

## Goal

Turn Moving's existing private media read and direct-upload foundations into
one verified chosen-AI workflow: bounded evidence in, direct image upload out,
and a stable photo attached to the exact move record or Queue result the person
approved.

## Current truth

`get_evidence_media` is a deployed bounded private batch read. The app/API has
direct B2 upload sessions and legacy MCP has photo-write compatibility tools.
Canonical OAuth MCP cannot write media, and the existing finish path does not
yet prove required server SHA-256, full image decode, exact provider-version
pinning, and all-version cleanup. MOV-WO-010 still lacks a real named-client
lifecycle. MOV-0040 owns broad catalogue convergence and already identifies
canonical `save_evidence_media` as a gap.

The phased truth, tool contract, visibility semantics, known grant/gateway
pitfalls, proof ladder, non-goals, and copyable worker prompt live in
`docs/planning/moving-family-media-and-mcp-adoption.md`. This Work Order changes
documentation only; no capability, provider, deployment or live proof exists.

## Sequence

1. MOV-0043 upgrades the existing upload/media records into one authoritative,
   exact-version, hash/decode-verified lifecycle with complete cleanup.
2. MOV-0044 adds canonical `save_evidence_media` begin/finish/attach actions,
   routes compatibility tools through the same control plane, and preserves
   `get_evidence_media` as the bounded read.
3. MOV-0045 implements explicit visibility/derivative semantics and the narrow
   read/write grant boundary without weakening Moving's shipped protections.
4. MOV-0046 records every proof rung through one named-client round trip and
   cleans all synthetic state.

## Dependencies

- The existing photo/upload/derivative actions, move membership resolvers,
  `get_evidence_media`, grant rows, operation receipts, and Queue/planning saves.
- MOV-WO-010's chosen-AI authority and MOV-0042's shipped grant fixes.
- MOV-0040 remains the catalogue-convergence authority; completion here marks
  only its media-write gap satisfied, not the rest of that Card.
- Family standards at `assist-with-life` commit `ee63aaf` and the Moving
  adoption brief.

## Exclusions

No replacement media system; audio/video chosen-AI claim; remote URL ingestion;
generic storage CRUD; automatic sharing; participant/access change; public
publishing; permanent delete; move creation, transport, box or Queue-table
convergence; provider, secret, bucket, billing, DNS, production-data, real-user,
or deployment action under this proposal.

## Stop rules

Stop if work would expose provider keys/URLs, trust client derivatives, commit
before required hash/type/full-decode verification, authorize from storage
possession, union grants, widen a selected-move grant, silently share evidence,
remove a live MCP capability, or cross an access/provider/secret/money/DNS/
production-data/publication/irreversible boundary without Scott.

## Verification

Follow the adoption brief's proof ladder. Prove direct upload, readback,
malformed/mismatched bytes, replay/conflict, revoke/expiry and cross-owner/move/
target denial, batch ceilings/step-down/omission, sanitized derivatives,
explicit visibility and original-download separation, exact-version cleanup,
legacy adapter parity, both dialects, token 401/503, stale reconnect, and one
named compatible client. Run full type, lint, unit/contract, build, MCP/docs,
tracker, Project Philosophy and representative browser gates.

## Human gates

Scott moves Proposed → Ready and records whether the recommended raised
`moving.media.write` tier is accepted. Provider/account configuration, secrets,
buckets, costs, DNS, production identity/data, public publishing and deployment
remain separate explicit gates. Routine source/schema/UI/test/fixture/PR/preview
decisions inside approved scope belong to the executor.

## Independent audit

Not audited. A separate AI must reconcile implementation and truth claims
against the family standards, this Work Order, MOV-WO-010 and MOV-0040.

## Execution evidence

Not started; proposed documentation only.

## History

- 2026-08-30 · Codex — proposed from current `origin/main` after reconciling
  Moving's deployed media read, existing direct upload, MOV-WO-010, MOV-0040,
  MOV-0042, and the family MCP/media standards at commit `ee63aaf`.
