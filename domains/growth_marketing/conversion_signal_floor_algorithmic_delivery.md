---
name: Conversion Signal Floor for Algorithmic Ad Delivery
domain: growth_marketing
tier: core
confidence: high
source: Meta March 2026 AI delivery update, digitalapplied.com, adstellar.ai, Meta Business Help Center
created: 2026-03-27
reverify_by: 2026-06-27
---

## Pattern

When an ad platform transitions from proxy-metric optimization (clicks, traffic) to downstream outcome prediction, campaigns below a minimum conversion signal threshold face non-linear CPM increases as the algorithm defaults to risk-hedged broad delivery. This is structurally different from creative or targeting failure — it is a data starvation penalty.

## Evidence

Meta March 2026 AI delivery update (unannounced, identified by advertisers through sudden performance shifts, later confirmed by Meta Business Help Center):
- CPMs increased 15–40% across retail, consumer goods, and financial services
- Campaigns generating fewer than 50 weekly optimization events per ad set were deprioritized
- Click/traffic-objective campaigns saw the worst degradation
- Creative quality became the primary remaining lever since audience targeting parameters were deprioritized

## Decision Rule

- Audit all ad accounts for ad sets below 50 weekly conversion events
- Consolidate fragmented campaign structures to concentrate signal above the threshold
- Migrate remaining click/traffic-objective campaigns to conversion objectives
- This compounds with attribution reclassification (separate Core entry) — two problems hitting simultaneously: fewer reported conversions + worse delivery efficiency

## April 2026 Update: Advantage+ Threshold Dropped to 25/Week

Meta reduced the Advantage+ Shopping campaign conversion threshold from 50 to 25 conversions per week. This opens Advantage+ to smaller advertisers and lower-volume product lines. Campaigns that previously couldn't qualify for Advantage+ Shopping should be re-evaluated. The general signal floor principle still holds — below the threshold, CPMs spike — but the threshold itself has moved.

Source: SocialBee, Digital Applied (April 2026)

## Boundaries

- Threshold is Meta-specific and continues evolving (was 50, now 25 for Advantage+ Shopping)
- Google PMax has analogous signal requirements at different thresholds
- Accounts already generating 25+ weekly conversion events per ad set are insulated
- The 25-event threshold applies specifically to Advantage+ Shopping; other campaign types may retain higher thresholds
