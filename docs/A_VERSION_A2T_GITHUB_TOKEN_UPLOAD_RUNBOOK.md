# A2T GitHub Token Upload Runbook

Date: 2026-06-30

## Purpose

This runbook defines the safest way to provide temporary GitHub upload
authorization for closing A2T workstream 6 under content-manifest publication
mode.

Do not provide a GitHub password. A password is broader than needed, hard to
scope, and should not be shared with Codex.

## Current Situation

The local publication bundle is already prepared and locally verified:

```text
local_publication_head = 66694666bb0b9f13aa7dca2ad62cba8fe36ad643
bundle_sha256 = 375a97bc4fcf3930d8f1505f5388de71d21d44ee4c26c5c86afd2a9bb3b6ac4c
content_publication_chunk_count = 17
local_content_publication_verified = true
```

The remaining remote publication step needs one of these:

```text
GITHUB_TOKEN
GH_TOKEN
GITHUB_PAT
or a working gh/git authenticated session
```

As of the latest check, none of these token environment variables are present
in the Codex shell.

## Recommended Token

Use a fine-grained personal access token.

Recommended scope:

```text
Repository access: Only selected repositories
Repository: kokobobi/hello-world
Permissions:
  Contents: Read and write
Expiration: 1 day or 7 days
```

No other permissions are needed for the content-publication upload path.

## Safe Usage Pattern

After generating the token, do not put it in project files.

Preferred shell pattern:

```bash
read -s GITHUB_TOKEN
export GITHUB_TOKEN
python3 scripts/a2t_upload_content_publication_to_github.py \
  --repository-full-name kokobobi/hello-world \
  --out generated/content_publication_github_upload_20260630.json
unset GITHUB_TOKEN
```

Then verify the remote raw files:

```bash
python3 scripts/a2t_verify_content_publication_bundle.py \
  --manifest https://raw.githubusercontent.com/kokobobi/hello-world/main/data/content_publication_bundle_20260630/a2t_content_publication_bundle_manifest_20260630.json \
  --chunks-root https://raw.githubusercontent.com/kokobobi/hello-world/main/data/content_publication_bundle_20260630 \
  --out generated/content_publication_remote_verification_20260630.json \
  --verify-git-bundle
```

Pass condition:

```text
content_publication_verified = true
all_chunks_ok = true
bundle_sha256_ok = true
bundle_size_ok = true
git_bundle_verify.ok = true
```

## After Upload

Immediately revoke the temporary token in GitHub settings after successful
remote verification.

The token is no longer needed once:

```text
generated/content_publication_remote_verification_20260630.json
```

contains a passing report from the remote raw URLs.

## Completion Boundary

This token upload only addresses workstream 6.

It does not address workstream 7. Real H1 readiness still requires:

```text
real apparatus event CSV
measured calibration artifacts
blind freeze/custody record
```
