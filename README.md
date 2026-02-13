# AutoPost — Product Requirements Document

## Executive Summary

**Product Name:** AutoPost  
**Version:** 1.0 (Prototype)  
**Target Users:** Small business owners who lack time and resources to maintain consistent social media presence  
**Core Value Prop:** AI-powered social media content creation that turns product photos into platform-ready posts with captions in minutes, not hours

---

## Problem Statement

Small business owners face three critical pain points with social media:

1. **Time Scarcity:** 78% of small business owners report they don't have time to post consistently
2. **Content Creation Friction:** Writing captions, choosing hashtags, and formatting for each platform requires creative energy most don't have after running their business
3. **Platform Complexity:** Each platform (Instagram, TikTok, Facebook) has different best practices, formats, and tone expectations

**Result:** Inconsistent posting → poor algorithmic reach → missed customers → lost revenue

---

## Target User Persona

**Primary:** Sarah, 35, boutique retail owner
- Runs a small shop selling handmade goods
- 0 marketing team, does everything herself
- Posts to Instagram 1-2x/week (wants 3-5x)
- Struggles writing captions that "sound right"
- Has 100+ product photos on her phone, never posts them
- Willing to pay $20-50/mo to solve this problem

**Secondary Users:**
- Restaurant owners (food photos → daily specials)
- E-commerce sellers (product shots → promotional posts)
- Service businesses (before/after photos → testimonials)

---

## Core Features (MVP)

### 1. Photo Library Management
**User Story:** As a small business owner, I want to upload all my product photos once so I can generate multiple posts from them.

**Requirements:**
- Drag-and-drop or click-to-upload interface
- Support JPG, PNG, WEBP formats
- Display photos in grid view with thumbnails
- Allow deletion of uploaded photos
- Store photos locally in browser (no backend needed for prototype)

**Success Metric:** Users upload 3+ photos in first session

---

### 2. AI Caption Generation (Vision-Powered)
**User Story:** As a business owner who isn't a "natural writer," I want AI to look at my product photo and write a caption that sounds like me.

**Requirements:**
- Use Claude Opus 4.5 with vision API
- Analyze actual product in photo (not generic descriptions)
- Generate 2-3 sentence caption + 4-5 relevant hashtags
- Support brand tone customization:
  - Professional
  - Friendly & approachable
  - Playful & fun
  - Luxury & aspirational
- Support content style options:
  - Product showcase
  - Lifestyle & product
  - Promotional / sale
  - Educational / tips
- Platform-specific optimization (Instagram vs TikTok vs Facebook)

**Success Metric:** 80%+ of generated captions are used without major edits

---

### 3. Posting Schedule Configuration
**User Story:** As a business owner, I want to set my posting frequency once and have the app generate a queue of posts automatically.

**Requirements:**
- Frequency options: Daily, 2x/week, 3x/week, Weekly
- Time-of-day preferences: Morning, Midday, Afternoon, Evening
- Platform selection (Instagram, TikTok, Facebook)
- Toggle platforms on/off independently

**Success Metric:** Users configure schedule in under 2 minutes

---

### 4. Content Queue Dashboard
**User Story:** As a business owner, I want to see all my upcoming posts in one place so I can review, edit, or delete before they go live.

**Requirements:**
- Display all generated posts in chronological order
- Show: thumbnail, caption preview, platform, scheduled date
- Filter by: All / Scheduled / Posted
- Actions per post:
  - Edit caption (inline)
  - Regenerate caption (new AI call)
  - Copy caption to clipboard
  - Delete post from queue
  - Open platform's compose screen directly
- Display stats: # posts scheduled, # platforms active, # photos uploaded

**Success Metric:** Users edit <20% of captions (AI quality is high enough)

---

### 5. One-Click Post Flow
**User Story:** As a non-technical business owner, I want posting to be as simple as possible even without full OAuth integration.

**Requirements (Prototype):**
- Copy caption to clipboard automatically
- Open Instagram/TikTok/Facebook compose screen in new tab
- User pastes caption and uploads photo manually
- Mark post as "Posted" after completion

**Requirements (Production):**
- Full OAuth integration with Instagram Graph API, TikTok for Business API, Facebook Graph API
- Automated posting without manual intervention
- Post scheduling with cron jobs
- Auto-upload photo + caption in single click

**Success Metric:** <30 seconds from "Generate" to post being live

---

## Technical Architecture

### Prototype (v1.0 — Current)
- **Frontend:** Single HTML file with embedded CSS/JS
- **AI:** Direct API calls to Anthropic (Claude Opus 4.5)
- **Storage:** Browser localStorage for API keys, in-memory for photos
- **Deployment:** GitHub Pages (static hosting)
- **Cost:** $0 infrastructure, pay-per-use AI API only

### Production (v2.0 — Future)
- **Frontend:** React or Next.js
- **Backend:** Node.js + Express
- **Database:** PostgreSQL (user accounts, posts, schedules)
- **Storage:** AWS S3 or Cloudflare R2 (uploaded photos)
- **Auth:** OAuth 2.0 for social platforms
- **Scheduling:** Cron jobs or BullMQ for post queue
- **Deployment:** Railway, Render, or Vercel
- **Cost:** ~$50/mo infrastructure + AI API usage

---

## User Flow

### First-Time User
1. Land on app → See "Configure API Key" banner
2. Click "Configure" → Enter Anthropic API key → Save
3. Step 1: Upload 3-5 product photos
4. Step 2: Set brand tone (e.g., "Friendly") + posting frequency (e.g., "2x/week")
5. Step 3: Select platforms (Instagram + TikTok)
6. Step 4: Click "Generate Queue" → Wait 10-15 seconds
7. Review 5 AI-generated posts with captions
8. Click "Edit & Post" on first post → Copy caption → Open Instagram → Paste & post
9. Mark as "Posted" → Move to next post

**Time to First Post:** <5 minutes

---

## Success Metrics (MVP Validation)

**User Activation:**
- 70%+ of visitors who land on the page upload at least 1 photo
- 50%+ complete the full flow (upload → schedule → generate queue)

**Product Quality:**
- 80%+ of captions are used without major edits
- Average time from photo upload to first post published: <10 minutes
- NPS score: >40

**Business Validation:**
- 30%+ of users say they would pay for this product
- Willingness to pay: $20-50/month
- Primary pain solved: "Saves me hours every week"

**Engagement:**
- Users generate an average of 5+ posts per session
- 60%+ return within 7 days to generate more posts

---

## Non-Goals (Out of Scope for MVP)

- ❌ Video editing or reel creation (photos only)
- ❌ Analytics or engagement tracking (focus on creation, not measurement)
- ❌ Team collaboration features (single-user only)
- ❌ Post performance optimization / A/B testing
- ❌ Direct messaging or comment management
- ❌ Influencer matching or sponsored content
- ❌ Multi-account management (1 business per user)

---

## Known Limitations & Future Roadmap

### Current Limitations (Prototype)
1. **Manual posting required:** Users must copy/paste to platforms (no OAuth yet)
2. **No persistence:** Photos/posts disappear on page refresh (browser storage only)
3. **Single user:** No login system or account management
4. **API key management:** Users must provide their own Anthropic API key
5. **No image generation:** Uses uploaded photos as-is (no AI lifestyle scenes yet)

### Roadmap (Post-Validation)

**v2.0 — Production MVP (if validated)**
- User accounts with login (email/password)
- Persistent storage (database + cloud storage)
- Full OAuth auto-posting to Instagram/TikTok/Facebook
- Subscription billing ($29/mo)
- Remove "bring your own API key" requirement

**v3.0 — Advanced Features**
- AI image generation (turn product photos into lifestyle scenes)
- Reel/video generation from static images
- Multi-account support (manage 3+ businesses)
- Basic analytics (posts published, platforms used)
- Calendar view for scheduled posts

**v4.0 — Scale Features**
- Team collaboration (assign roles, approve posts)
- Brand voice training (upload past posts to learn your tone)
- Competitor analysis (see what similar businesses post)
- Integrations (Shopify, WooCommerce, Squarespace)

---

## Open Questions & Risks

### Questions to Answer via User Research
1. **Pricing:** Is $29/mo the right price point? Or should it be usage-based (e.g., $1 per post)?
2. **Platform Priority:** Do users care more about Instagram vs TikTok vs Facebook? Should we focus on one first?
3. **Content Mix:** Do users want variety (different caption styles) or consistency (same brand voice every time)?
4. **Editing Frequency:** How often do users edit captions? What's missing that makes them edit?
5. **Trust:** Will users trust AI-generated content enough to post without heavy editing?

### Known Risks
1. **Platform API Restrictions:** Instagram/TikTok OAuth approval can take weeks-months; may be rejected
2. **AI Cost:** If caption generation costs $0.10/post and users generate 50 posts/mo, margins are tight at $29/mo price point
3. **Content Quality:** AI captions may feel generic; users might churn if quality isn't high enough
4. **Market Saturation:** Buffer, Later, Hootsuite already exist — differentiation must be clear (AI content creation, not just scheduling)
5. **Compliance:** Need privacy policy, terms of service, GDPR compliance before monetizing

---

## Go-to-Market Strategy

### Phase 1: Prototype Validation (Current)
- Share link with 20-30 small business owners
- Collect feedback via Google Form after they try it
- Key question: "Would you pay $29/mo for this?"
- Goal: 10+ users say "yes" = validation signal

### Phase 2: Paid Beta
- Rebuild with user accounts + OAuth
- Launch on Product Hunt, Indie Hackers, Reddit (r/smallbusiness)
- Charge $19/mo (early adopter discount)
- Goal: 50 paying users in 60 days = product-market fit signal

### Phase 3: Scale
- Add referral program (give 1 month free for each referral)
- Content marketing (blog posts on small business social media tips)
- Partnerships with e-commerce platforms (Shopify app store)
- Goal: $10K MRR within 12 months

---

## Competitive Landscape

| Product | Positioning | Pricing | Key Differentiator |
|---------|-------------|---------|-------------------|
| **Buffer** | Social media scheduler | $6-120/mo | Multi-platform scheduling, analytics |
| **Later** | Visual planner for Instagram | $25-80/mo | Grid preview, hashtag suggestions |
| **Hootsuite** | Enterprise social management | $99-739/mo | Team collaboration, multi-account |
| **Canva** | Design tool with scheduler | Free-$30/mo | Design templates, visual editing |
| **Copy.ai** | AI copywriting tool | $49/mo | General copywriting, no social focus |
| **AutoPost** | AI social content generator | $29/mo (planned) | **Vision-based caption generation from product photos** |

**Unique Value Prop:** Only tool that looks at your actual product photo and writes a custom caption for it. Competitors either schedule pre-written content (Buffer, Later) or generate generic copy without seeing your product (Copy.ai).

---

## Appendix: API Requirements

### Anthropic API
- **Endpoint:** `/v1/messages`
- **Model:** `claude-opus-4-5-20251101`
- **Features Used:** Vision (base64 image input)
- **Average Cost:** ~$0.05-0.10 per caption
- **Rate Limit:** 50 requests/min (Claude Opus tier)

### Future APIs (Post-MVP)
- **Instagram Graph API:** For auto-posting to Instagram Feed + Reels
- **TikTok for Business API:** For auto-posting videos (invite-only)
- **Facebook Graph API:** For auto-posting to Facebook Pages
- **Stability AI (optional):** For lifestyle image generation

---

## Contact & Feedback

**Product Owner:** Tony Nghiem  
**Prototype URL:** https://tonyn15665.github.io/Social-Media-app-test/  
**Feedback:** [Open GitHub Issues](https://github.com/tonyn15665/Social-Media-app-test/issues)

---

**Document Version:** 1.0  
**Last Updated:** February 12, 2026  
**Status:** Prototype — Seeking Validation
