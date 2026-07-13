---
name: infrastructure_summary
description: Summary of portfolio site infrastructure and cost drivers
metadata:
  type: project
---

**Infrastructure Overview:**
- Static HTML/CSS portfolio website
- Deployed to ap-south-1 (India)
- S3 bucket for content storage
- CloudFront distribution for global caching
- Origin Access Control (OAC) for secure S3 access
- No custom domain configured (using CloudFront default)

**Cost-Driving Resources:**
1. CloudFront: Data transfer out ($0.085/GB in PriceClass_200)
2. S3: Storage ($0.023/GB/month) + GET requests ($0.0004 per 10,000)
3. CloudFront: Invalidation requests (not being used)

**Annual Cost Estimate (low-traffic portfolio):**
- CloudFront data transfer: $30-60/year
- S3 storage (500MB): $0.12/year
- S3 requests: <$1/year
- **Total: ~$30-65/year**

**Key Characteristics:**
- Low traffic volume (typical portfolio)
- Static content (no dynamic computation needed)
- Global reach via CloudFront (but could optimize for PriceClass_100)
- Terraform-managed infrastructure (good for cost control)
