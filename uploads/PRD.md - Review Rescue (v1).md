# PRD.md — Review Rescue (v1)

## Overview

Review Rescue is an app for small business owners that alerts them the moment a new review posts — especially a negative one — and gives them an AI-drafted, tone-matched response ready to send, edit, or dismiss. Built as part of Erica Kelly's Apps Built With AI certification, with a secondary role as a credibility-building lead generator into Erica Kelly Consulting's deeper strategic work.

## Problem Statement

Small business owners know reviews affect revenue and reputation, but responding takes time they don't have — so reviews go unanswered, especially the ones that hurt most. Nearly half of all Google reviews carry no text at all, just a star rating; when that rating is low, the business has no context to respond to and no easy way to prevent it from dragging down their average. The result: a visible, public gap in responsiveness that costs trust and revenue.

## Goals

- A new review triggers an alert to the owner within minutes.  
- The owner can review, edit, and send (or dismiss) an AI-drafted response without leaving the app.  
- One real business owner uses it on real reviews and confirms it saves them time and reduces the anxiety of an unanswered bad review.  
- No response ever goes out without a human opening and acknowledging it first.

## User Roles

- **Owner/Admin** — full access: receives alerts, approves/edits/sends responses, manages account and billing, sees full history.  
- **Manager/Staff** (optional) — same day-to-day access as Owner (alerts, drafting, sending, history) minus account and billing settings.  
- *Not in v1:* an agency role managing multiple businesses' accounts (see Out of Scope).

## Features — P0 (must exist for the product to work at all)

1. **Instant Alert** — new review (any rating) triggers a notification to the Owner (and Manager, if assigned) via SMS and email within minutes of posting.  
2. **AI-Drafted Response** — draft matched to tone/situation, with a one-tap "regenerate" option if the first draft misses the mark. Owner or Manager can send as-is, edit, or dismiss.  
3. **Acknowledgment Tracking** — every draft records who opened/approved it and when (`acknowledged_by`, `acknowledged_at`), separate from `sent_at`. Nothing sends without this step.  
4. **Escalation Path for Sensitive Reviews** — reviews flagged as legally sensitive (refund disputes, threats, discrimination claims) skip auto-drafting and go straight to escalation:  
   - Immediate: SMS \+ email to Owner (and Manager, if assigned)  
   - 4 business hours, unacknowledged: second alert sent  
   - 24 hours, unacknowledged: marked "at risk" — a persistent, visible flag  
5. **Star-Only Low-Rating Outreach** — a review with 3 stars or fewer and no text triggers a proactive outreach draft (inviting the reviewer to share more), flagged for owner attention rather than treated as "nothing to respond to."

## Features — P1 (needed soon, not required day one)

- Basic history/log of past reviews and how each was handled  
- Voice/tone settings so drafts sound like the specific business, not generic AI  
- Review platforms beyond Google (Yelp, Facebook)

## Features — P2 (explicitly deferred — real ideas, not forgotten, not built yet)

- Agency role for managing multiple client accounts (would require rethinking the product as white-label)  
- Full review dashboard with sentiment trends over time  
- Multi-location support for chains/franchises  
- Connecting review-response activity to broader client OKRs/KPIs (a consulting-layer feature, not an app feature)

## User Flows

**Flow 1 — Instant Alert \+ Response (core loop)**

1. New review posts on the business's Google profile.  
2. App detects it, sends Owner (and Manager) a notification within minutes.  
3. Notification includes review text and an AI-drafted response.  
4. Owner/Manager opens the draft (this is logged as acknowledged), then sends as-is, edits, regenerates, or dismisses.  
5. Sent response posts back to Google (directly if the API allows, otherwise copy-paste).

**Flow 2 — Escalation (sensitive review)**

1. New review is flagged as legally sensitive instead of auto-drafted.  
2. Immediate SMS \+ email alert to Owner/Manager.  
3. If unacknowledged after 4 business hours, a second alert goes out.  
4. If still unacknowledged after 24 hours, the item is marked "at risk" in the dashboard so it's never silently lost.

**Flow 3 — Star-Only Low Rating**

1. A 3-star-or-lower review posts with no written text.  
2. App generates a proactive outreach draft rather than marking it "no action needed."  
3. Flagged for Owner/Manager attention; same acknowledge-then-send rule applies.

## Data Requirements

- **Business profile** — name, industry/category, connected review platform(s)  
- **Review records** — text (if any), star rating, date, platform, status (`new` / `drafted` / `acknowledged` / `sent` / `dismissed`), sensitivity flag  
- **Response drafts** — AI-generated draft, edit history, final sent version  
- **Acknowledgment data** — `acknowledged_by`, `acknowledged_at`, `sent_at`  
- **Voice/tone settings** — per-business preferences (P1)  
- **User/account info** — Owner and Manager login and contact details for alerts

## Design Requirements

Resolved: Review Rescue uses its own standalone visual identity, not EKC's consulting brand system. Direction: approachable, calm, trustworthy, fast — full palette, typography, spacing, and tone rules documented in DESIGN-ReviewRescue.md. A light "Review Rescue — an Erica Kelly Consulting company" credibility line carries trust from EKC without borrowing its full visual system.

## Out of Scope (v1)

- Multi-location or franchise support  
- Agency accounts managing multiple clients  
- OKR/KPI tracking or any strategic performance-management layer  
- Review platforms beyond Google  
- Full analytics/sentiment dashboard beyond a basic history log  
- Fully autonomous sending without a human acknowledgment step

## Open Questions

- Should Review Rescue use EKC's existing brand system (DESIGN.md/VOICE.md) or have its own identity? No AUDIENCE.md exists yet for Review Rescue's small-business-owner audience specifically.  
- Pricing/monetization model not yet decided.  
- The 4-hour / 24-hour escalation SLA windows are a starting draft — confirm before building.  
- Google Business Profile API access/verification lead time should be confirmed early so it doesn't block the build timeline.

