# A2T Remote Publication Feasibility And Policy

Date: 2026-06-30

## Purpose

This note records the current remote-publication status after testing the local
publication package and the available GitHub connector path.

It deliberately stays outside `publication/a2t-null-test-report` so it does not
change the already verified local publication commit, tag, or bundle.

## Local Package Footprint

The local package prepared for publication is:

```text
publication/a2t-null-test-report
```

Current verified local publication markers:

```text
branch = main
tag = local-publication-20260630
head = 66694666bb0b9f13aa7dca2ad62cba8fe36ad643
bundle = publication/a2t-null-test-report-local-publication-20260630.bundle
bundle_sha256 = 375a97bc4fcf3930d8f1505f5388de71d21d44ee4c26c5c86afd2a9bb3b6ac4c
```

Current footprint excluding `.git`:

```text
file_count = 432
total_bytes = 125823396
largest_files = multi-MB JSON summary artifacts under data/
```

The package is therefore not a small text-only upload. The publication bundle
is the cleanest local transport artifact; a full remote mirror should normally
be done with authenticated `git push`, not by many ad hoc contents-API writes.

## GitHub Connector Status

The available GitHub connector can create and update repository files and can
create lower-level git objects such as trees and commits. It has already been
used successfully to update status files in:

```text
kokobobi/hello-world
```

That remote now contains public-safe status documents, but it is not a full
mirror of the publication package.

The current strict verifier reports:

```text
remote_verified = false
reason = remote main/tag do not resolve to the local publication head
```

This is expected: status-file upload through the contents API does not recreate
the local git history, tag, and full package tree.

## Two Valid Completion Modes

There are two possible remote-publication completion semantics. They must not be
mixed.

### Mode A: Full Git Mirror

This is the current strict requirement.

Completion marker:

```text
remote main == local_head
remote tag local-publication-20260630 == local_head
remote package tree is the local publication tree
```

Verification tool:

```text
python3 scripts/a2t_verify_remote_publication.py \
  --repository-full-name kokobobi/<repo-name> \
  --out generated/remote_publication_verification_20260630.json
```

This mode is best completed by authenticated `git push` from
`publication/a2t-null-test-report`.

### Mode B: Content-Manifest Publication

This is a possible fallback if full git mirroring is not available.

Completion marker:

```text
remote repository records a commit or release artifact
remote file list matches an explicit local content manifest
remote checksums match local package checksums
remote README clearly states this is content-publication, not git-mirror publication
```

This mode would require a new verifier that compares remote content or release
artifacts against `data/FULL_DATA_CHECKSUMS.txt` or an equivalent generated
manifest. It would not satisfy the existing strict git-mirror verifier unless
that verifier is intentionally extended with a separate content-verified field.

## Current Decision

Do not mark workstream 6 complete yet.

Reason:

```text
local publication package = complete
GitHub status-file handoff = complete enough for review visibility
full remote git publication = not verified
content-manifest remote publication = not implemented or verified
```

## Local Content-Manifest Tooling Status

The content-manifest fallback now has local tooling and a passing local
reconstruction check.

Scripts:

```text
scripts/a2t_prepare_content_publication_bundle.py
scripts/a2t_verify_content_publication_bundle.py
```

Generated local bundle-publication package:

```text
generated/content_publication_bundle_20260630/
generated/content_publication_bundle_20260630/a2t_content_publication_bundle_manifest_20260630.json
generated/content_publication_bundle_20260630/content_publication_bundle_verification_20260630.json
generated/content_publication_bundle_20260630/chunks/*.b64
```

Local content verification result:

```text
chunk_count = 17
content_publication_verified = true
reconstructed_bundle_sha256 = 375a97bc4fcf3930d8f1505f5388de71d21d44ee4c26c5c86afd2a9bb3b6ac4c
git_bundle_verify = pass
```

This proves the bundle can be transported as a checksum-verified set of base64
chunks. It still does not prove remote publication until the manifest and all
chunks are uploaded to a stable remote location and verified from that remote
location.

## Practical Next Options

1. Full mirror path:

```text
provide working GitHub push auth for kokobobi/<repo-name>
run scripts/a2t_push_publication_to_github.sh
run scripts/a2t_verify_remote_publication.py
```

2. Connector content-publication path:

```text
define a content-publication manifest
upload split artifacts or selected release assets through an approved route
write a new content verifier
record remote commit/release URLs and checksum match
```

Current local status for this path:

```text
content manifest = generated
chunk files = generated locally
local verifier = pass
remote chunk upload = not done
remote content verifier = not run
```

3. Current handoff-only path:

```text
keep kokobobi/hello-world as a public status handoff repo
do not claim it is the complete publication package
use the local bundle as the authoritative portable artifact
```

## Remaining Goal Boundary

The seven-item goal still has two hard completion blockers:

```text
item 6 = remote full publication or content-manifest publication must be verified
item 7 = real H1 apparatus data, measured calibration artifacts, and blind custody must exist
```

Until both are present, the correct project status is:

```text
simulation/report/governance package = mature local prototype
remote publication = partially handed off, not fully verified
real experiment claim = not allowed
```
