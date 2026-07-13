---
name: user-context
description: Who the user is and what this repo is for, relevant to security audits
metadata:
  type: user
---

Repo `devops-micro-internship-pravinmishra` is a DevOps micro-internship
learning project (weekly assignments under `week-02-agentic-ai/`, etc.). The
`terraform/` directory provisions a pure HTML5/CSS3 static portfolio site
(no JS, no build step) onto S3 + CloudFront, per the project's own
CLAUDE.md. Given the learning context, findings should include concrete,
copy-pasteable Terraform fixes (not just descriptions) since the user is
likely applying these directly to learn the patterns, and severity should be
graded against a small static-site's realistic risk (e.g. don't over-index
on enterprise-scale concerns like multi-account guardrails).
