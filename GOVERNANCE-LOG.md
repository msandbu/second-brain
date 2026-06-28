---
title: "Governance change log"
authority_level: 2
file_type: log
tags: ["governance", "changelog", "audit"]
staleness_threshold: stable
description: "A record of significant changes to the structure, publishing principles, and scope of this repository."
---

# Governance log

A record of significant decisions and changes to this repository. Entries are added when the structure, scope, or publishing principles change in a meaningful way.

---

## 2026-06-28 — Initial structure established

**What changed:** Repository created and initial knowledge module structure put in place.

**Decisions made:**
- Folders: `blogposts/`, `talks/`, `frameworks/`, `me/`
- `waysofthinking/` folder removed in favour of keeping mental models inside `frameworks/`
- MCP server at `https://msandbu.no/mcp` set as the live endpoint for AI access
- GitHub Actions workflow set up to auto-sync all `.md` changes to the Cloudflare Worker

**Governance files added:**
- `CLAUDE.md` and `AGENTS.md` \u2014 AI loading instructions (identical, dual-named for cross-tool compatibility)
- `GOVERNANCE.md` \u2014 publishing principles
- `COLLECTIONS.md` \u2014 thematic index for broad queries

**Identity files added:**
- `me/profile.md`, `me/voice.md`, `me/career.md`, `me/books.md`, `me/links.md`

**Publishing principles confirmed:**
- Only already-published content or faithful synthesis of published content
- No AI-generated content presented as Marius's writing
- No employer or client confidential information
- No dash character in visible text (hard rule)

---

## How to use this log

Add an entry here whenever:
- A new folder or content category is added or removed
- The publishing principles in `GOVERNANCE.md` are updated
- A significant decision is made about what is in or out of scope
- The MCP endpoint or sync infrastructure changes

Keep entries brief. Date, what changed, why.
