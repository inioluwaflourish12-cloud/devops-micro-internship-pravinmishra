---
name: cloudfront_price_class
description: CloudFront PriceClass_200 can be reduced to PriceClass_100 for portfolio site
metadata:
  type: feedback
---

**Current:** CloudFront configured with `price_class = "PriceClass_200"` in aws_cloudfront_distribution.website resource

**Recommendation:** Change to `price_class = "PriceClass_100"`

**Why:** 
- PriceClass_100 covers North America, Europe, Asia, Middle East, and Africa (adequate for portfolio site)
- PriceClass_200 adds 100+ additional edge locations at premium pricing
- Portfolio site serves primarily India (ap-south-1 region) and potentially some Western users; PriceClass_100 fully covers both regions
- Static website has low traffic volume; additional edge locations provide diminishing returns

**How to apply:**
Edit `/terraform/main.tf` line 55: change `price_class = "PriceClass_200"` to `price_class = "PriceClass_100"`

**Impact:** MEDIUM - Estimated savings of $5-15/month (10-30% reduction in data transfer costs depending on traffic patterns and region distribution)

**Implementation:** One-line change, no breaking impacts
