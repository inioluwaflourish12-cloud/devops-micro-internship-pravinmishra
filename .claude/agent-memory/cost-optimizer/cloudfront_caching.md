---
name: cloudfront_caching
description: CloudFront cache policy analysis for portfolio site
metadata:
  type: feedback
---

**Current:** Using managed cache policy `CachingOptimized` (ID: 658327ea-f89d-4fab-a63d-7e88639e58f6)

**TTL Configuration (CachingOptimized defaults):**
- Default TTL: 86400 seconds (1 day)
- Max TTL: 31536000 seconds (1 year)
- Minimum TTL: 0 seconds
- Caches on: GET, HEAD methods

**Analysis:** WELL-CONFIGURED
- CachingOptimized policy is designed to maximize caching and minimize origin requests
- 1-day default TTL is reasonable for portfolio sites where content changes infrequently
- High MaxTTL allows long-term caching for static assets (CSS, JS, images)
- Error caching (404 responses) set to 300 seconds (5 minutes) - appropriate for handling missing pages gracefully

**Cost Impact:** Excellent
- High TTL = fewer requests to S3 origin = lower data transfer costs and S3 request charges
- Typical portfolio sites see 90%+ cache hit rates with this configuration

**No changes recommended** - this is well-optimized for static content.
