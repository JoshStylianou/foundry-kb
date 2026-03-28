---
title: Video-to-Website Skill Pattern and Production Deployment Pipeline
domain: tools_and_software
type: pattern
source: josh_input
confidence: high
date_added: 2026-03-28
date_verified: 2026-03-28
tags: claude-code, skills, video-to-website, vercel, github, deployment, ffmpeg, web-development, business-model, self-improving-skills
related: [high_end_website_generation_workflow.md]
---

## Video-to-Website Skill

A custom Claude Code skill (markdown file) that turns a video into a premium scroll-driven animated website. Two skills work together:
1. **Front-end design skill** — modified version of Anthropic's official skill, tuned for animated 3D product sites
2. **Video-to-website skill** — the core engine that handles frame extraction, scroll-position binding, and section layout

Both are markdown files placed in `.claude/skills/`. The key pattern: **after each build, tell Claude Code to update the skill with what worked and what didn't.** The skill self-improves with every website built.

## Optimal Build Workflow

1. **Generate source images** — Use NanoBanana (via key.ai) to create start and end frames (e.g., blender empty → blender full of fruit). 16:9 aspect ratio, plain backgrounds.
2. **Generate video** — Feed start + end frames into Cling 3.0 (also via key.ai). Use Claude to write the video prompt from the two frames — better results than manual prompting.
3. **Plan mode first** — Start Claude Code in plan mode. Describe the site. Let it ask questions (product name, sections, layout). Answer those, review the plan, THEN let it build. Results in much better first iterations.
4. **Build and iterate** — Switch to bypass permissions mode. Claude Code extracts frames via ffmpeg (installs it automatically if missing), builds HTML/CSS/JS, creates scroll-position-to-frame binding.
5. **Test on localhost** — Iterate locally. Screenshot issues, describe fixes in natural language. Clear context at ~50% to avoid context rot.

## Production Deployment Pipeline

**Local → GitHub → Vercel (auto-deploy)**

1. Claude Code authenticates with GitHub CLI (`gh auth`)
2. Creates repo and pushes code
3. Import repo in Vercel dashboard → auto-deploys on every push
4. Local changes → test on localhost → push to GitHub → auto-deploys to production

**Critical gotcha:** Frame files (100+ webp images extracted from video) get excluded by .gitignore by default. The deployed site will show text/animations but no product video. Fix: explicitly tell Claude Code to include frames in the repo before pushing.

**Hosting options:** Vercel (free tier, auto-deploy from GitHub) or Netlify (free tier, global CDN). Both work. Vercel has tighter GitHub integration with automatic staging/production environments.

## Business Model for Selling AI-Built Sites

- Build a demo site for a specific niche (e.g., blender company, watch brand) in ~30 minutes
- Cold outreach: email the link or walk in and show the demo
- Charge $5,000-$10,000 per site (still cheaper than agencies, delivered in days not months)
- Add monthly hosting + maintenance as recurring revenue
- The skill improves with each build, so quality compounds over time

Target: businesses with terrible websites who won't pay agency prices or wait months. The demo site IS the sales pitch.

## Evidence

Walkthrough video demonstrating end-to-end build of a blender product landing page with scroll-driven 3D animation, from NanoBanana image generation through Cling 3.0 video through Claude Code build through Vercel deployment. First iteration was near-production quality in ~30 minutes.

## Why This Matters

This is a productizable service pattern — repeatable, skill-improving, and directly monetizable. The self-improving skill means each build raises the floor for the next one.

## Action Triggers

- When building product landing pages or demo sites for client pitches
- When deploying Claude Code-built sites to production (use the GitHub → Vercel pipeline)
- When considering website building as a service offering
- When the .gitignore frames gotcha appears (animation works locally but not deployed)
