# Moving family media and MCP adoption

**Status:** Proposed improvement program. This is a target contract, not proof
of implementation, provider configuration, deployment, or named-client support.

## Why this belongs in Moving

Photographs are working evidence in a move: what an item is, where it began,
how it was packed, what arrived, and what needs attention. Moving already has
more media foundation than most Assist products. Its canonical MCP can deliver
a bounded private batch through `get_evidence_media`, and the app/API has a
direct upload-session flow backed by B2. The next step is not a second media
system. It is to make the existing system meet one explicit family contract and
bring the write path to the canonical chosen-AI workflow.

## Current, Partial, Later

### Current

- Canonical OAuth MCP exposes the fifteen-tool Moving workflow, including
  bounded private `get_evidence_media`. It steps down image sizes before
  omission, caps count/per-item/total bytes, and names omissions without
  returning storage URLs.
- The app and API can begin a presigned upload and finalize stored images,
  audio, and video. The provider is treated as byte storage and Convex carries
  move/photo records and upload state.
- The canonical chosen-AI MCP has no media-write tool. The legacy catalogue has
  base64-oriented `add_images` and `attach_photos`, currently governed through
  the compatibility grant gate. MOV-0040 already owns catalogue convergence
  and names `save_evidence_media` as the missing canonical capability.
- Current finalization proves useful provider facts such as declared type and
  length. The repository does not yet prove the whole family finish contract:
  required authoritative SHA-256, full decode before commit, exact provider
  version pinning, and version-complete lifecycle cleanup.
- MOV-WO-010 is Active because a real named-client lifecycle remains unproved.
  Its private media-read delivery is strong evidence, but not write proof.

### Partial target

The first tranche makes JPEG, PNG, and WebP the fully verified connected-AI
path. The existing `get_evidence_media` remains the read surface. A new
canonical `save_evidence_media` uses explicit `begin_upload`, `finish_upload`,
and `attach` actions around a direct HTTP PUT. It files a committed `mediaId`
onto an item, box, room, transport/zone, move, Queue work item, planning result,
or source check only after current grant and target authority are re-read.

### Later

- Audio/video through chosen-AI MCP after format-validation, playback,
  bandwidth, privacy, and cost policy is deliberately proved. Their existing
  app/API support does not make them Current for a connected AI.
- Public or unlisted evidence delivery beyond a separately authorized,
  revocable safe derivative. Household collaboration continues to use Moving's
  roles; the family visibility terms describe semantics, not a forced database
  vocabulary migration.
- Broad two-door/two-catalogue retirement remains MOV-0040. This program closes
  its media gap and must update that Card, but does not silently absorb its move
  creation, transport, box, Queue-table, or compatibility-migration work.

## App and agent split

The app owns the person, household/move/target authorization, grants,
visibility, provenance, exact object/version manifest, upload state,
idempotency, record attachment, archival and deletion. The AI can inspect a
bounded evidence set, take or generate a requested image, upload it through an
approved session, and file the committed media into the exact workflow the
person requested. It cannot invite a participant, widen access, infer that a
shared move shares every attachment, publish evidence, delete permanently,
override a safety hard block, or make storage possession equal authority.

## Product tool surface

- Preserve `get_evidence_media` as the private batch-read tool. Return safe
  bytes/app-delivered content, media ID, decoded type, size, dimensions,
  SHA-256, derivative kind, provenance, and one explicit omission per requested
  item. Continue step-down-before-drop and never return B2 keys or signed URLs.
- Add canonical `save_evidence_media` with:
  - `begin_upload`: authorize one move target; bind `operationId`, expected
    SHA-256, size, content type, target/role, source/provenance, visibility
    intent, and metadata fingerprint; return one short-lived direct PUT session.
  - Direct client HTTP PUT outside MCP.
  - `finish_upload`: re-read the grant, move membership, target and session;
    inspect exact stored bytes; verify length and required SHA-256; fully decode;
    create trusted sanitized derivatives; pin exact provider versions; commit a
    stable `mediaId` or return a stable family failure.
  - `attach`: file only a committed media ID onto the authorized item, box,
    room, transport/zone, move, Queue job/result, planning result, or source
    check. The save is a Moving workflow action, not raw photo-table CRUD.
- One-call action shape keeps approval/tool-call cost low while preserving the
  three-phase byte transfer. A retry of the same operation and fingerprint
  replays; changed content/target returns `operation_conflict`.

Normal uploads are `begin -> direct PUT -> finish`. Base64 remains only for a
documented tiny-image compatibility exception after a full server decode, and
legacy `add_images`/`attach_photos` become thin adapters to the same control
plane during MOV-0040's migration window. No remote-URL fetch or provider
fallback may bypass the canonical finish.

## Authority, derivatives, and visibility

- Convex is the control plane. It decides grants, move/target authority,
  sessions, manifests, visibility, provenance and cleanup. B2 stores encrypted
  bytes; its key, URL, bucket, or credential is never authorization.
- The manifest pins original plus every derivative by environment, object key,
  provider version, server-verified SHA-256 and length, decoded type,
  dimensions, derivative role, creator, source, move target, lifecycle state,
  and timestamps. Environment and visibility credentials are least-privileged;
  isolation is proved rather than inferred from a bucket name.
- Trusted server code generates display/card/thumb derivatives and strips
  EXIF/GPS. Client-supplied derivative bytes are not authoritative.
- `Private` is the default owner-only draft. Existing move collaborators map to
  `Trusted` view-only semantics according to their role; original download is a
  separate capability. `Unlisted` is a revocable app link to a safe derivative.
  `Public` requires an explicit human publish action and rights basis. Sharing
  a move/recipient link never automatically includes media; inclusion is
  explicit per attachment and uses the safest useful derivative.

The family recommendation is ordinary `moving.media.read` and raised,
explicitly enabled `moving.media.write`, because a write lands permanently and
spends stored bytes. That is the recommended resolution of MOV-0042's Q9, not a
claim that Scott has approved the change. Scott's Ready decision for this Work
Order should record the final tier. Product scopes stay in Moving's grant model,
not the provider's OAuth `scopes_supported` identity list.

## Known MCP and grant traps to preserve against

- Moving has two dialects and two doors. Pre-authorize at the product boundary
  before any gateway can flatten the error; preserve modern and legacy
  pre-grant method behavior, explicit `tools` capability even for an empty list,
  discovery filtering and call-time enforcement.
- Preserve three token outcomes: invalid → 401; introspection/JWKS unavailable
  → 503 with retry guidance; valid → product grant. Carry opaque-token support
  and stable client identity into the canonical door before retiring legacy.
- Never regress the fixes for bounded-scan revocation resurrection, flat scope
  union, unidentified-client collapse, expired-grant starvation, or split
  issuer normalization. A selected-move grant is checked against the target of
  each call.
- Sign-in-as-approval is Moving's recorded soft-launch ruling. It does not make
  raised media write implicit, and it does not permit participant changes,
  permanent deletion, public publishing, or another move.
- Refusals say reconnect or enable the exact capability and who can do it. They
  do not tell a compatible client Moving “cannot” perform an authorized action.

## Acceptance and proof ladder

Record each rung separately: specified; implemented; locally verified;
provider configured; exact source deployed; real bytes; authorization; named
client; operational cleanup/recovery. Existing read proof cannot substitute for
write proof, and MOV-WO-010's SDK/deploy receipts cannot substitute for this
media lifecycle.

Prove valid upload and readback; altered hash/length/type; malformed/polyglot
image rejected by full decode; replay/conflict; expired/revoked/cross-owner/
cross-move/cross-target refusal; batch ceilings and named omissions; metadata
stripping; explicit attachment and visibility; original-download separation;
legacy adapter parity; both MCP dialects; token unavailable vs invalid; stale
client reconnect; and deletion/expiry of every original, derivative, provider
version, session, receipt and product row.

## Explicit non-goals

No new media subsystem; raw database/storage CRUD; remote-URL ingestion;
unbounded export; automatic evidence sharing; participant or access changes;
permanent delete; AI-controlled public publishing; audio/video chosen-AI claim;
move creation, transport, box-lifecycle or Queue-table convergence; provider,
secret, bucket, billing, DNS, production-data, real-user, or deploy action in
this Proposed Work Order.

## Copyable ambitious worker prompt

> Build MOV-WO-011 as one coherent Moving outcome on fresh `origin/main`.
> First read AGENTS.md, the Project Philosophy, tracker Guide, MOV-WO-010,
> MOV-0038, MOV-0040, MOV-0042, the API/MCP guide and stateless foundation,
> this adoption brief, and the four Assist family standards named here. Keep
> the existing direct-upload and `get_evidence_media` foundations; converge
> their authority and validation instead of creating a parallel media store.
> Deliver a canonical `save_evidence_media` workflow with Convex-authorized
> begin, direct client PUT, server-verified finish, stable media ID, sanitized
> derivatives, and explicit attachment to real Moving targets. Preserve
> bounded batch read, move-scoped grants, sign-in-as-approval, both MCP
> dialects/doors during migration, and every shipped grant-lifecycle fix. Make
> routine technical decisions and improve adjacent code where needed for this
> outcome, while leaving MOV-0040's unrelated convergence gaps out. Prove
> server-required hash, length, type, full decode, replay/conflict, version
> pinning, revoke/expiry/cross-owner/move/target denial, batch step-down and
> omissions, safe visibility, exact-version cleanup, token 401/503 outcomes,
> stale-client reconnect, legacy adapter parity, and one named compatible AI
> lifecycle with marked synthetic data. Return separate source, local,
> provider, deployment, real-byte, authorization, named-client, cleanup and
> docs-truth receipts. Stop only for a real provider/account/secret, money,
> production-data/identity, access, public-publish, rights, DNS or irreversible
> boundary.

## Authority and related work

This brief applies the family standards from `assist-with-life` commit
`ee63aaf`: `assist-media-storage-standard.md`, `mcp-connector-playbook.md`,
`bring-your-ai-mcp-oauth-standard.md`, and `personal-ai-success-scenarios.md`.
MOV-WO-011 is the proposed execution record. MOV-WO-010 remains authority for
the chosen-AI lifecycle and MOV-0040 for catalogue convergence.
