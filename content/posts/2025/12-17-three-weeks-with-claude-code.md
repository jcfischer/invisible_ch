---
title: "Three Weeks with Claude Code: Building a Personal AI Infrastructure"
date: 2025-12-17T17:00:00+01:00
author: "Jens-Christian Fischer"
description: "Reflections on building CLI tools and MCP servers with Claude Code"
image: ""
categories: ["code"]
tags: ["claude", "ai", "cli", "tana", "mcp"]
language: en
draft: false
type: post
---

Three weeks ago I started using [Claude Code](https://docs.anthropic.com/en/docs/claude-code), Anthropic's CLI tool that lets Claude work directly in your terminal. Shortly after, I discovered [PAI - Personal AI Infrastructure](https://github.com/danielmiessler/PAI), a framework by [Daniel Miessler](https://danielmiessler.com/) that turns Claude Code from a capable tool into something far more powerful.

The core insight of PAI is deceptively simple: apply the Unix philosophy to AI. Small tools that do one thing well. Composable. Each tool you build makes the whole system more capable. Daniel built the meta-layer - the skill system, the delegation patterns, the constitutional principles that keep Claude focused and effective. I get to build on top of that foundation.

Three weeks in, I've added my own tools to the ecosystem. And here's the recursive part: Claude helped me build them, and now Claude uses them to help me.

## The Tana Supertag Server

The tool I'm most pleased with is an MCP server for [Tana](https://tana.inc), my note-taking system. Tana exports its data as JSON, but that data is essentially a graph - nodes with references to other nodes, tagged with "supertags" that define their type (meeting, person, project, todo).

The challenge: I wanted Claude to be able to search and understand my Tana workspace. Not just keyword search, but semantic search - finding notes by meaning, not just matching words. The graph structure itself is super complicated and parsing it seems impossible (have you ever tried to make sense of a 290MB big JSON file?). Claude took a couple of minutes to make a first iteration that parsed 1.2 million nodes into a SQL database. Querying it revealed that none of the structure was preserved. But by engaging in a back and forth dialogue, "we" managed to extract meaningful structure and I can query it.

The solution took about a week of iteration (spread across evenings and weekends). The MCP server now:

- Automatically downloads the JSON file (which took a bit of handholding to get working)
- Indexes Tana exports into SQLite with FTS5 for fast text search
- Generates vector embeddings via Ollama for semantic similarity
- Resolves the graph structure - when a search matches a bullet point deep in a meeting, it returns the meeting context
- Creates new nodes via Tana's Input API

In order to test this, I created a [Book importer](https://github.com/jcfischer/gutenberg-tana) that imports books from Project Gutenberg to Tana. After importing, I could watch Claude use the provided tools to query the books and create a text that drew from the sources. This was a most astonishing feeling - like watching magic happen.

{{< youtube uEoTTmYXqNk >}}

## The Learning Curve

I won't pretend this was smooth. The first week was rough, but mostly because I had a dopamine rush that would prevent me from sleeping. My ADHD brain went into full hyperfocus mode on this. One of my strengths is, that I see possibilities in many things. And how things fit together. The more time I spent with Claude and "my" assistant, the more ideas I had (and have). Currently I'm building a meeting preparation tool, that reads my calendar, searches Tana and my emails for information about upcoming meetings and prepares a briefing document for me - in Tana, linked to the meeting notes. 

All of this is private. And I think that's one of the real great usages. Yes, Generative AI has problems with data protection. But most of the tools that I have written are not using any AI for their working, and they store information locally. When I need to send something to an AI in the cloud, it passes a PII pseudonymizer that strips names of people, email addresses, phone number etc and sends a sanitized version to the large language models. On the way back, the reverse transformation is applied.

## The Unix Philosophy, Applied

What makes PAI powerful isn't any single tool - it's how they compose.

The Tana MCP server doesn't just help me search notes. Combined with the email skill, Claude can find "what did we discuss about the security audit?" across both my meeting notes and my inbox. The calendar skill knows when I'm free; the Tana skill knows my projects; together they help me plan what to work on.

Each new tool multiplies the capabilities of the existing ones. This is the Unix philosophy: `grep` is useful, `find` is useful, but `find | xargs grep` is transformative. Daniel's insight was recognizing that AI tools follow the same pattern.


## The Cost Question

Let's talk money. Claude Code uses Claude's API, and agentic workflows burn through tokens fast. A session where Claude reads files, searches code, runs tests, and iterates on a solution can easily use 100K+ tokens.

My rough estimate after three weeks: I've spent somewhere between $100-200 on API costs before I figured out that my best option is to buy the $100 Pro license and live with the limitations it gives (my wife is happy, that I have to take breaks from time to time) That's not nothing. But I've also built:

- An email CLI with IMAP sync and semantic search
- A calendar automation that controls my apartment's heating based on booking schedules
- The Tana MCP server
- a reporting engine that sends emails with nicely formatted, company branded reports to our clients
- A multi-context writing system (which, meta-ly, helped write this post)
- and many more

Would I have built these without Claude Code? Some, eventually. But not in three weeks, and probably not to the same level of polish. The TypeScript is cleaner than I'd write solo (Actually, I don't even write TypeScript). The error handling is more thorough. Everything is Test Driven - because I told Claude to always use TDD patterns (and that's something the system forgets when too many context compactions have happened)



## What Actually Changed

The shift isn't just productivity - it's what I'm willing to attempt.

Before, I'd have an idea like "I want semantic search over my Tana notes" and file it under "someday, when I have time to learn about embeddings and vector databases." Now I describe what I want and iterate toward it. The gap between idea and implementation shrunk dramatically.

This has downsides. I'm building more things, but am I understanding them as deeply? When Claude writes the vector similarity function, do I really grasp the math? At the moment - no. I hardly read any of the written code. I try to be specific about Claude writing tests, if I detect failures and require all tests to pass. Claude sometimes forgets about that too...


## Three Weeks In

PAI is now part of how I work. Claude has access to my calendar, my notes, my email. It helps me write, research, and build. Every tool I add makes the system more capable - not just for me, but potentially for anyone building on the same foundation.

That's perhaps the most interesting aspect of Daniel's approach: PAI isn't a product, it's a pattern. The skills I build could work for anyone using the framework. The Unix philosophy scales beyond a single user.

Is this the future of personal computing? I don't know. It feels significant, but so did a lot of things that turned out to be dead ends. What I can say: for someone who likes building tools and has more ideas than time, the combination of Claude Code and PAI has been genuinely transformative.

I'll keep building. And I'll keep writing about it - with some help from my co-author (who enables me to write more)

---

*This post was written with significant AI assistance. See Daniel Miessler's [AI Label (AIL)](https://danielmiessler.com/p/the-ai-label) framework for thinking about AI involvement in content creation. I'd rate this post AIL-3: AI-assisted with human direction, editing, and personal additions.*

