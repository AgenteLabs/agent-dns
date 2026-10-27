<!-- estate-hygiene:begin — emitted by tools/estate-hygiene-files.mjs in AgenteLabs/flashyos; regenerate, never edit -->
# Security

## Reporting a vulnerability

Report it privately, never in a public issue, pull request or chat channel.
Two routes, and both reach the same people:

- **Email michael@flashygroup.com** — the estate's one disclosure address, the same one
  published at https://flashynetwork.com/security/
  and in https://flashynetwork.com/.well-known/security.txt.
  One route across every repository is deliberate: a researcher who finds two
  addresses and picks the worse one has been failed by us, not by their choice.
- **GitHub → Security → Report a vulnerability** on this repository, which
  opens a private advisory only the maintainers can read. If that button is
  missing, private vulnerability reporting has not been enabled on this
  repository yet; use the email route and say so in the report.

Include what you found, how to reproduce it and what you believe the impact
is. Do not include real credentials, private keys or production data: nothing
here needs them to reproduce a finding.

## What to expect

| | |
|---|---|
| Acknowledgement | within 72 hours |
| An assessment, and what we are doing | agreed with you, in writing |
| Publication | a window agreed with you, never imposed |

If we miss the acknowledgement window, say so publicly. A window nobody is
held to is worse than none, because it asks a reporter to wait on a promise
that was never load-bearing.

## Supported versions

The default branch only. There is no maintained release line behind it: a
finding against the default branch is in scope, a finding against an older
tag or a fork is a reason to update.

## A committed credential is rotated, never removed

If a report is that a secret reached this repository, the fix is rotation at
the issuer. Deleting the file, rewriting history or force-pushing is not a
fix: the value is burned the moment it lands and stays burned, because
history, forks, caches and mirrors keep it. Say which secret, and we rotate
it before anything else.

## About this document

The sections above are emitted by [`tools/estate-hygiene-files.mjs`](https://github.com/AgenteLabs/flashyos/blob/main/tools/estate-hygiene-files.mjs)
in AgenteLabs/flashyos from one template the whole estate shares, and
`--check` fails when they drift.
Regenerate them; never edit them here. Anything below the marker is this
repository's own and is kept as written.
<!-- estate-hygiene:end — everything below is this repository’s own -->

## What counts

For a specification and reference resolver, a security problem is any of:

- a record, redirect or document that the reference resolver **accepts** and the specification says it must refuse — in particular any way to make a resolver fetch a url whose host is not `<domain>` or a subdomain of it, or any non-https url;
- any path by which `unreachable` is reported as `absent`, or either as an empty result;
- a way to make the resolver read more than the size cap, wait past the timeout, or follow more than one redirect;
- a way to make a valid-looking record parse to a different `url` than the one written (parser confusion);
- a credential shape, secret or personal data committed anywhere in the tree.

A disagreement about what the specification *should* say is a spec change, not a security report — see `CONTRIBUTING.md`.

## What this specification does not defend against

`SPEC.md` §6 is the full account. In short: `agent-dns/1` does not authenticate DNS. A spoofed or poisoned TXT answer can produce a wrong `absent` or `invalid` finding, or point a consumer at a different path on the same domain; it cannot, under a conforming resolver, point the consumer off the domain, because the same-domain rule and the https requirement are applied to the record and to every redirect. Consumers needing more should validate DNSSEC where the zone is signed.

## Scope

This repository holds no service, no keys and no data. There is nothing here to rotate.
