# A2T Remote Publication Handoff Checklist

Date: 2026-06-30

## Purpose

This checklist defines the remaining evidence required to close workstream 6:
remote GitHub publication of the A2T null-test package.

Local publication readiness is already complete. This checklist is only for
remote publication evidence.

## Local Package To Publish

```text
local_repo = publication/a2t-null-test-report
branch = main
tag = local-publication-20260630
bundle = publication/a2t-null-test-report-local-publication-20260630.bundle
bundle_clone_verified = true
current_head_and_bundle_sha256 = see generated/remote_upload_readiness_final_20260630.json
```

## Required User Input

Provide the target repository full name:

```text
kokobobi/<repo-name>
```

Recommended default if you approve it:

```text
kokobobi/a2t-null-test-report
```

## Remote Publish Procedure

After the repository exists and is authorized, run:

```text
bash scripts/a2t_push_publication_to_github.sh git@github.com:kokobobi/<repo-name>.git
```

If HTTPS credentials are configured instead of SSH:

```text
bash scripts/a2t_push_publication_to_github.sh https://github.com/kokobobi/<repo-name>.git
```

## Evidence Required To Mark Workstream 6 Complete

The remote publication is complete only when these fields are recorded:

```text
remote_repository_full_name
remote_url
remote_default_branch
remote_commit_sha
remote_tag_or_release_id
local_head_at_upload
bundle_sha256_at_upload
remote_readme_verified
remote_paper_verified
remote_artifacts_index_verified
checksum_or_release_hash_match
```

## Post-Upload Verification Commands

Use the verifier after the push:

```text
python3 scripts/a2t_verify_remote_publication.py \
  --repository-full-name kokobobi/<repo-name> \
  --out generated/remote_publication_verification_20260630.json
```

The verifier reads `generated/remote_upload_readiness_final_20260630.json` and
checks that remote `main` and `local-publication-20260630` resolve to the same
expected local head.

Manual fallback commands:

```text
git -C publication/a2t-null-test-report remote -v
git -C publication/a2t-null-test-report ls-remote --heads origin main
git -C publication/a2t-null-test-report ls-remote --tags origin local-publication-20260630
```

The expected remote commit for both `main` and `local-publication-20260630`
must match:

```text
generated/remote_upload_readiness_final_20260630.json.local_head
```

## Current Status

```text
workstream_6_local_status = complete
workstream_6_remote_status = blocked_on_repository_full_name
```
