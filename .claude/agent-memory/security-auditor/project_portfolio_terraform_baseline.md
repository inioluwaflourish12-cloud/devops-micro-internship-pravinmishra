---
name: project-portfolio-terraform-baseline
description: Baseline architecture and known security gaps in terraform/ for the portfolio-site (S3 + CloudFront static site)
metadata:
  type: project
---

The `terraform/` directory (as of 2026-07-13) provisions a static portfolio
site: `aws_s3_bucket.website` (private, public access block enabled) served
via `aws_cloudfront_distribution.website` using an Origin Access Control
(`aws_cloudfront_origin_access_control.s3`, sigv4) and a bucket policy scoped
with `AWS:SourceArn` condition to the specific distribution ARN. No IAM
resources, no WAF, no logging resources exist in this directory. Files:
`main.tf`, `variables.tf`, `outputs.tf`, `providers.tf`, `backend.tf`.

Known gaps found in the first full audit (2026-07-13), useful to check for
regressions/fixes in future reviews:
- No `aws_s3_bucket_server_side_encryption_configuration` (no encryption at rest).
- No `aws_s3_bucket_versioning`.
- No `aws_s3_bucket_logging` and no CloudFront `logging_config` block (no access logs).
- No CloudFront response-headers policy (missing CSP/X-Frame-Options/etc.).
- `viewer_certificate` uses `cloudfront_default_certificate = true`; the
  `domain_name` variable exists in `variables.tf` but is never referenced
  anywhere — dead code / incomplete custom-domain wiring. If a custom domain
  is added later, it will need an ACM cert in us-east-1 + `minimum_protocol_version`.
- `backend.tf` has the S3 remote backend block fully commented out with
  bootstrap instructions in comments — state is local-only until manually
  uncommented after bootstrap resources are created. This is intentional
  (documented two-step bootstrap), not an oversight, but flag if it's still
  commented out much later than expected.
- No WAFv2 web ACL attached to the CloudFront distribution.
- No IAM/OIDC resources anywhere in `terraform/`, even though CLAUDE.md says
  deploys are "automated via GitHub Actions" — verify separately (e.g. in
  `.github/workflows/`) that the deploy role uses GitHub OIDC with a
  repo/branch-scoped trust policy rather than long-lived IAM user access keys
  stored as repo secrets. As of this audit no `.github/workflows/` directory exists yet.

Positive patterns already followed correctly (don't flag as findings unless changed):
- Bucket name uses `data.aws_caller_identity.current.account_id` via a data
  source rather than a hardcoded account ID — good practice for uniqueness,
  not a leaked secret.
- S3 public access block has all four settings enabled.
- CloudFront uses modern OAC (not legacy OAI) with `signing_behavior = "always"`.
- `viewer_protocol_policy = "redirect-to-https"` is set (HTTP->HTTPS enforced).
- Bucket policy is scoped with `Condition.StringEquals["AWS:SourceArn"]` to
  the exact distribution ARN, not a wildcard.
