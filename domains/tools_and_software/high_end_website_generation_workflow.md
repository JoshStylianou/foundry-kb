---
title: High-End Website Generation Workflow (Claude Code + 3D Assets)
domain: tools_and_software
type: pattern
source: josh_input
confidence: high
date_added: 2026-03-28
date_verified: 2026-03-28
tags: web-development, claude-code, video-generation, cling-3.0, higsfield, netlify, taste-skill, scroll-animation, 3d-assets, one-shot-websites
related: []
---

## The Workflow (3 Steps)

1. **One-shot the website** — Feed Claude Code the "taste" skill (open-source repo that instills high-end design principles: spacing, luxury aesthetics, design schematics) + a few bullet points describing what you want. Produces a complete, high-quality site in one shot.

2. **Generate 3D animated assets** — Use Cling 3.0 model via Higsfield platform. Generate exploding views, rotating objects, panning scenes. Settings: 5 seconds, 16:9 aspect ratio, 1080p quality (~7.5 credits per generation). Generate 2-3 variants simultaneously and pick the best. For source images, use NanoBanana to generate stills, then feed into Cling 3.0.

3. **Integrate and deploy** — Tell Claude Code to integrate the video/animation into the site. Deploy to Netlify free tier (global CDN, unlimited deploys, free forever).

## Key Techniques

- **Video hero background:** Use video as hero header background with inward masking gradient so the animation doesn't interfere with the site background colour.
- **Scroll-triggered frame-by-frame animation:** Extract video frames as optimized JPEGs, tie each frame to scroll position, add preloading. Way faster than playing video on scroll. Claude Code does this automatically when you say "make it faster."
- **Iterative performance optimization:** Start with raw video, then repeatedly tell Claude Code "make it faster." It will compress (e.g. 5.3MB → 252KB), extract frames, add preloading. Accept quality tradeoffs incrementally.
- **Iterative design refinement:** Screenshot issues in the browser, paste back to Claude Code with natural language descriptions of what's wrong. "The text is hard to read" → it fixes contrast/overlays.
- **Locomotive scroll sequences:** Claude Code sets up scroll-reveal logic tying text sections to animation frames as you scroll through.

## Economics

| Component | Cost |
|-----------|------|
| Claude Code tokens | ~$1-2 |
| Higsfield video generation (2-3 variants) | ~$3-4 |
| Netlify hosting | Free |
| **Total** | **~$3-5** |
| **Time** | **~15 minutes** |

Previously this calibre of site would cost $5,000-$10,000 from a web developer.

## Evidence

Josh built 4 sites in ~15 minutes using this exact workflow: a headphones site, a forest restoration site with 3D globe, an interior design site with exploding house view, and a space station site. All with 3D scroll effects. All one-shotted.

## Why This Matters

This is a repeatable, sub-$5 workflow for producing sites that look like $10K agency work — directly applicable to client deliverables across Styfinity and TNT Growth, or rapid prototyping for any new venture.

## Action Triggers

- When Josh or a client needs a landing page or marketing site quickly
- When building showcase/portfolio sites for any business
- When a project needs impressive visual assets (3D animations, exploding views, scroll effects)
- When evaluating whether to hire a web developer vs. self-serve
