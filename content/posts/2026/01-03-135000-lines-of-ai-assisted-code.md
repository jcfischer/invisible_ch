---
title: "135,000 Lines of AI-Assisted Code: A Month with Claude Code"
date: 2026-01-03T22:00:00+01:00
author: "Jens-Christian Fischer"
description: "What happens when you pair an AI assistant with a developer who can't stop building tools? A month of statistics, learnings, and the recursive joy of building tools that build tools."
categories: ["code"]
tags: ["claude", "ai", "cli", "productivity", "pai"]
language: en
draft: false
type: post
---

A month ago, I wrote about my [first three weeks with Claude Code](/posts/2025/12-17-three-weeks-with-claude-code/). At that point, I had a few tools working: an email CLI, a Tana integration, some calendar automation. It felt like a lot.

I just ran the numbers. It's considerably more than I thought.

## The Numbers

Here's what Claude and I have built together since early December:

| Project | Files | Lines of Code |
|---------|-------|---------------|
| Supertag CLI (Tana) | 163 | 44,116 |
| Tool for my Psychotherapist wife | 63 | 21,331 |
| Email Skill | 46 | 10,523 |
| Daily Briefing | - | 4,481 |
| PII Anonymizer | - | 2,894 |
| Calendar (ical) | - | 2,235 |
| Tado Thermostat | - | 1,551 |
| Other KAI Skills | 294 total | ~70,000 |

**Total: roughly 135,000 lines of TypeScript.**

To be clear: I didn't write any of thses 135,000 lines of code. I didn't even read them. Claude did all of the typing. But I architected, reviewed, debugged, tested, cursed at, and eventually shipped all of it. The collaboration feels like pair programming where my partner never gets tired, never gets defensive about their code, and can hold the entire codebase in memory.
In many regards, Claude feels like a mix between a jolly puppy, a junior software developer, and a totally confused person. It gets a lot of things right, but often misses the big picture. It implemented a number of different ways to access the databases in the supertag program. Luckily, it can then also look over the codebase, and find these duplications and fix them.

## What We Actually Built

The raw numbers don't tell you much. Here's what these tools actually do:

**Supertag CLI** - This one surprised me. 44,000 lines for a Tana integration? It started as a simple query tool. Then I needed semantic search, so we added vector embeddings via Ollama. Then I needed to understand meeting transcripts, so we added transcript parsing. Then I needed to create nodes, so we built a full API integration with schema validation. Then I wanted it to work as an MCP server for Claude...

You see how this goes. And I still have quite a few ideas on how that tool can become even better. The great thing for me is that people in the Tana space are actually using it (and it's working for them) - that makes me very happy.

**Healthcare Report Automation** - A system for my wife's psychotherapy practice. It fills official Swiss insurance forms (AFP-Formulare), manages patient data, syncs with Google Calendar, and handles document uploads with OCR. Started as "can you help me fill out this PDF?" and became a full production application. I thought about turning this into a SaaS product, tut I think it will be a one-off solution for her alone. This vibes with a blog post I read recently, about the threat of agentic coding to SaaS.

**Email Skill** - IMAP sync, semantic search across 10+ years of email, draft composition. The semantic search alone changed how I work. "Find that email about the security audit from someone at the bank, sometime last spring" actually works now.

**Daily Briefing** - Pulls calendar, email, tasks, and weather into a morning summary. Sounds simple. The devil is in the edge cases (recurring events, timezone handling, determining what's "important"). There's an additional **Meeting Prep** that looks at my upcoming meetings, researches the mail conversations I had with the attendees, looks at notes from previous meetings and creates a briefing for the meeting. It puts these (together with the entries for the meetings themselves) in my Tana early in the morning. That is hugely helpful for me.

## The Productivity Question

Everyone asks: "Is it actually faster?" The honest answer: it depends.

For me speedup is dramatic. I have no way of measuring the actual speedup, but writing 135k lines of code in 6 weeks (part time as well) is insance. Claude generates working code faster than I can type, and the iteration cycles are measured in seconds rather than minutes.

The bigger shift isn't speed—it's scope. I'm building things I wouldn't have attempted before. A 44,000-line CLI tool? A full healthcare application? These would have been months of work. Now they're weeks.

## Making it work

I have always been using TDD, so having code that isn't tested is a red flag for me. Luckily the PAI Infrastructure by Daniel Miessler already had TDD in mind and I was able to strengthen the whole development process by start to use a variation of SpecKit by Github. (I saw that in Daniel's [December 2025 PAI walkthrough video](https://danielmiessler.com/blog/personal-ai-infrastructure) where he briefly mentioned it). Here's [an example spec](https://github.com/jcfischer/supertag-cli/tree/main/.specify/specs/063-unified-query-language) from the supertag-cli project showing how this works in practice. And here's where work with the AI shines. I asked Claude Code to write the necessary skill and command to use that kind of structure and it did it within minutes.

## The Recursive Part

Here's what delights me most: I built tools that help Claude help me build more tools.

The Tana integration lets Claude search my notes and meeting transcripts. The email skill lets it find relevant correspondence. The calendar skill knows when I'm free. When I say "prepare for my meeting with Thomas next week," Claude can:

1. Find the meeting in my calendar
2. Search Tana for previous meetings with Thomas
3. Search email for recent correspondence
4. Generate a briefing document

Each tool makes the next tool more useful. It's Unix philosophy applied to AI: small tools that compose into larger capabilities.

## What I Learned

**Test-Driven Development matters more with AI.** When Claude generates 500 lines of code, the only way I know it works is to run the tests. I've become religious about writing tests first.

**Architecture decisions are still human decisions.** Claude will happily implement whatever architecture you suggest, even bad ones. The skill is knowing what to ask for.

**Documentation is for future-Claude.** I write detailed CLAUDE.md files in each project. They're not for me—they're so Claude can understand the codebase when we return to it later.

**The cost is real but manageable.** I've settled on the $100/month Pro plan. The rate limits force breaks, which my ADHD brain actually needs. When the limit hits, I step away. Review what we built. Think about what's next.

## What's Next

The skill system keeps growing. I've migrated the core tools from scattered directories into a unified structure at `~/.claude/skills/`. There are now 15 indexed skills with proper triggers and workflows.

But the list of "wouldn't it be nice if..." ideas grows faster than I can build. Meeting preparation. Automated code review. A writing assistant that knows my voice (it helped write this post, actually). Financial tracking. Research automation.

The constraint isn't capability anymore. It's attention. What deserves focus?

For now: consolidation. Making what exists more robust. Writing documentation. Building tests. The boring work that makes the exciting work possible.

After all, 135,000 lines of code is meaningless if it doesn't actually solve problems. The goal was never to write code—it was to build tools that give me time back.

By that measure, we're doing alright.

---

*The tools mentioned in this post are part of my [Personal AI Infrastructure](https://github.com/danielmiessler/PAI) setup, building on Daniel Miessler's framework. The supertag-cli is [open source](https://github.com/jcfischer/supertag-cli) if you're curious about the Tana integration.*

## Further Reading: Tools and Frameworks

- [Building a Personal AI Infrastructure (December 2025 Update)](https://danielmiessler.com/blog/personal-ai-infrastructure) - Daniel Miessler's 40-minute video walkthrough of his PAI v2 setup
- [Personal AI Infrastructure (PAI)](https://github.com/danielmiessler/PAI) - Daniel Miessler's framework for building AI-augmented workflows
- [spec-kit](https://github.com/github/spec-kit) - GitHub's spec-driven development approach that turns specifications into executable artifacts
- [supertag-cli](https://github.com/jcfischer/supertag-cli) - My Tana integration with semantic search and MCP server

## Further Reading: Agentic AI and the Future of SaaS

- [AI agents are starting to eat SaaS](https://martinalderson.com/posts/ai-agents-are-starting-to-eat-saas/) - Martin Alderson
- [The End of Rented Software: Why Smart Companies Are Taking SaaS In-House with Agentic Development](https://mweinberger-proactivemgmt.medium.com/the-end-of-rented-software-why-smart-companies-are-taking-saas-in-house-with-agentic-development-fbe18a1d6c91) - Michael Weinberger
- [Why SaaS is Dead and the Future is Agentic](https://www.ema.co/blog/agentic-ai/why-saas-is-dead-and-the-future-is-agentic) - EMA
- [Will Agentic AI Disrupt SaaS?](https://www.bain.com/insights/will-agentic-ai-disrupt-saas-technology-report-2025/) - Bain & Company
- [Has Agentic AI Disrupted SaaS Yet? What Really Happened in 2025](https://medium.com/@jannadikhemais/has-agentic-ai-disrupted-saas-yet-what-really-happened-in-2025-215d02f299cb) - Khmaïess Al Jannadi
