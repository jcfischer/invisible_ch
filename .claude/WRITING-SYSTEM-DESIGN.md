# Multi-Context Writing Agent System

**Based on**: Alex McFarland's Claude Code Masterclass
**Target**: Multiple writing contexts for Jens-Christian Fischer
**Date**: December 17, 2025

---

## Executive Summary

This document outlines a **multi-context writing agent system** that transforms Claude Code into a personalized co-writer across different domains and voices. The system uses **context engineering** rather than prompt engineering - providing Claude with structured information about voice, audience, and content patterns to produce authentic writing for each context.

### Writing Contexts

| Context | Domain | Voice | Language |
|---------|--------|-------|----------|
| **invisible.ch** | Personal blog | Thoughtful, curious, technical | English |
| **Switch Security** | B2B professional | Formal, precise, authoritative | German/French |
| **Narratuos** | Theater social media | Playful, warm, spontaneous | German |

The system enables seamless switching between contexts while maintaining distinct voices for each.

---

## Architecture Overview

The system lives in PAI's skills directory and serves all writing contexts through a unified architecture with context-specific profiles.

```
~/.claude/skills/writer/
├── SKILL.md                     # Master writing skill
├── contexts/                    # Writing context profiles
│   ├── invisible/              # Personal blog context
│   │   ├── voice-dna.json     # Writing style fingerprint
│   │   ├── audience.json      # Reader profile
│   │   ├── identity.json      # Blog identity & themes
│   │   └── guides/            # Per-category guidance
│   │       ├── musings.md
│   │       ├── music.md
│   │       ├── code.md
│   │       └── art.md
│   │
│   ├── switch-security/        # Professional B2B context
│   │   ├── voice-dna.json     # Formal, precise voice
│   │   ├── audience.json      # University security officers
│   │   ├── identity.json      # Switch SOC brand
│   │   ├── templates/         # Report templates
│   │   │   ├── monthly-report.md
│   │   │   ├── incident-summary.md
│   │   │   └── recommendation.md
│   │   └── terminology.json   # Security jargon & translations
│   │
│   └── narratuos/              # Theater social media context
│       ├── voice-dna.json     # Playful, warm voice
│       ├── audience.json      # Theater-goers profile
│       ├── identity.json      # Brand: "Spontan · Einzigartig · Unvergesslich"
│       ├── templates/         # Social media templates
│       │   ├── show-announcement.md
│       │   ├── engagement-post.md
│       │   └── behind-scenes.md
│       └── team.json          # Member bios for mentions
│
├── shared/                      # Cross-context resources
│   ├── skills/                 # Reusable writing skills
│   │   ├── improver/          # Enhancement skill
│   │   ├── seo-optimizer/     # SEO skill
│   │   └── voice-trainer/     # Voice learning skill
│   └── knowledge/             # Reference material
│       ├── style-samples/     # Voice samples per context
│       └── patterns/          # Successful post patterns
│
└── commands/                    # Context-aware commands
    ├── write.md               # /write [context] [type] [topic]
    ├── brainstorm.md          # /write:brainstorm [context]
    ├── outline.md             # /write:outline [context] [topic]
    ├── draft.md               # /write:draft [context] [topic]
    ├── polish.md              # /write:polish [file]
    └── switch-context.md      # /write:context [name]
```

### Context-Specific Output Locations

| Context | Output Location | Format |
|---------|-----------------|--------|
| invisible.ch | `/Users/fischer/work/web/invisible_ch/content/posts/` | Hugo markdown |
| Switch Security | `~/work/reporter/drafts/` | Markdown → PDF |
| Narratuos | Clipboard / direct post | Social media text |

---

## Component Details

### 1. Voice DNA (`context/voice-dna.json`)

Captures Jens-Christian's unique writing voice by analyzing existing posts.

```json
{
  "meta": {
    "version": "1.0",
    "lastUpdated": "2025-12-17",
    "samplesAnalyzed": 50
  },
  "voice": {
    "tone": ["thoughtful", "curious", "technical-yet-accessible"],
    "perspective": "first-person singular",
    "formality": "conversational-professional",
    "humor": "occasional, dry wit",
    "verbosity": "concise, each word earns its place"
  },
  "style": {
    "sentenceLength": "varied, favoring medium",
    "paragraphLength": "short (2-4 sentences)",
    "transitionStyle": "organic, not signposted",
    "openingPatterns": ["direct statement", "question", "observation"],
    "closingPatterns": ["reflection", "invitation", "callback"]
  },
  "vocabulary": {
    "preferred": ["craft", "explore", "curious", "elegant"],
    "avoided": ["amazing", "journey", "dive into", "leverage"],
    "technicalLevel": "comfortable with jargon, explains when needed"
  },
  "signature": {
    "patterns": ["parenthetical asides", "em-dashes for emphasis"],
    "quirks": ["bilingual references (German/English)"],
    "culturalMarkers": ["Swiss context", "maker culture", "IndieWeb values"]
  }
}
```

### 2. Ideal Reader Profile (`context/icp.json`)

Defines who reads invisible.ch and what they care about.

```json
{
  "meta": {
    "version": "1.0"
  },
  "primaryReader": {
    "description": "Technically-minded creative professional",
    "interests": ["music production", "programming", "art", "philosophy"],
    "technicalLevel": "developer or tech-adjacent",
    "readingContext": "RSS feed, weekend reading, inspiration-seeking"
  },
  "readerGoals": {
    "musings": "perspective, provocation, reflection",
    "music": "discovery, creative process insight",
    "code": "learning, practical techniques, tool discovery",
    "art": "inspiration, aesthetic appreciation"
  },
  "expectations": {
    "depth": "substance over fluff",
    "format": "scannable but rewarding to read fully",
    "frequency": "quality over quantity",
    "interaction": "webmentions, RSS, no comments section"
  }
}
```

### 3. Blog Profile (`context/blog-profile.json`)

The blog's identity and purpose.

```json
{
  "identity": {
    "name": "InVisible",
    "tagline": "Musings. Music. Code. Art.",
    "url": "https://invisible.ch",
    "author": "Jens-Christian Fischer",
    "since": 2003
  },
  "categories": {
    "musings": {
      "description": "Reflections on technology, creativity, and life",
      "frequency": "when inspired",
      "typicalLength": "500-1500 words"
    },
    "music": {
      "description": "Album releases, production notes, musical discoveries",
      "frequency": "per release + discoveries",
      "typicalLength": "100-500 words"
    },
    "code": {
      "description": "Technical tutorials, tool reviews, development insights",
      "frequency": "when learning something worth sharing",
      "typicalLength": "800-2000 words"
    },
    "art": {
      "description": "Visual art, photography, creative projects",
      "frequency": "irregular, project-based",
      "typicalLength": "200-800 words"
    }
  },
  "values": {
    "indieweb": "Own your content, POSSE, webmentions",
    "privacy": "Self-hosted analytics, no tracking",
    "craft": "Quality over quantity",
    "openSource": "Share knowledge, give credit"
  },
  "technicalStack": {
    "platform": "Hugo",
    "theme": "Chaschper (custom)",
    "hosting": "Cloudflare Pages",
    "features": ["IndieAuth", "Webmentions", "RSS"]
  }
}
```

### 4. Category Guides

Per-category writing guidance (example for code.md):

```markdown
# Code Category Writing Guide

## What Belongs Here
- Technical tutorials with real value
- Tool discoveries that change workflows
- Development insights from actual projects
- AI/automation experiments

## What Doesn't Belong
- News aggregation without personal insight
- Pure documentation (that goes elsewhere)
- Unfinished experiments without conclusions

## Structure Template
1. Hook: The problem or discovery
2. Context: Why this matters
3. Solution: The technical meat
4. Code: With explanations, not just dumps
5. Reflection: What I learned

## Voice Notes
- Technical precision, but explain the "why"
- Include gotchas and mistakes
- Link to related posts when relevant
- Screenshots/figures for complex concepts

## SEO Considerations
- Title should include main technology/concept
- Description should answer "what will I learn?"
- Tags: technology name, concept type, difficulty
```

---

## Context: Switch Security Communications

Professional B2B communications for Swiss university security customers.

### Voice DNA (`contexts/switch-security/voice-dna.json`)

```json
{
  "meta": {
    "version": "1.0",
    "context": "switch-security",
    "description": "Professional security communications for Swiss higher education"
  },
  "voice": {
    "tone": ["professional", "authoritative", "reassuring"],
    "perspective": "institutional first-person plural (we/Switch)",
    "formality": "formal-professional",
    "humor": "none - serious domain",
    "verbosity": "precise and complete, but not verbose"
  },
  "style": {
    "sentenceLength": "medium, clear structure",
    "paragraphLength": "structured, often with headers",
    "transitionStyle": "logical, signposted",
    "openingPatterns": ["executive summary", "key findings first"],
    "closingPatterns": ["recommendations", "next steps", "contact info"]
  },
  "vocabulary": {
    "preferred": ["incident", "mitigation", "remediation", "posture"],
    "avoided": ["hack", "attacked", "breach" (unless confirmed)],
    "technicalLevel": "security professional appropriate"
  },
  "bilingual": {
    "primary": "German (Swiss German formal)",
    "secondary": "French (Swiss French formal)",
    "terminology": "consistent translation of security terms"
  }
}
```

### Audience (`contexts/switch-security/audience.json`)

```json
{
  "primaryReader": {
    "role": "Security Officer / IT Security Manager",
    "organization": "Swiss university or higher education institution",
    "technicalLevel": "security professional",
    "concerns": ["compliance", "incidents", "budget justification", "benchmarking"]
  },
  "secondaryReaders": {
    "executives": "Need high-level summaries, business impact",
    "technical_staff": "Need actionable details, IOCs, procedures"
  },
  "communicationGoals": {
    "monthly_reports": "Inform, benchmark, reassure, recommend",
    "incident_summaries": "Document, explain, advise on response",
    "recommendations": "Persuade, guide, enable action"
  }
}
```

### Content Types & Templates

| Type | Purpose | Length | Language |
|------|---------|--------|----------|
| Monthly Report | Incident summary, trends, benchmarks | 4-6 pages | DE/FR |
| Incident Summary | Single incident documentation | 1-2 pages | DE/FR |
| Recommendation | Security improvement guidance | 0.5-1 page | DE/FR |
| Executive Brief | High-level summary for leadership | 1 page | DE/FR |

### Writing Guidelines

```markdown
## Switch Security Writing Rules

1. **Lead with findings** - Busy security officers scan first
2. **Use consistent terminology** - See terminology.json for translations
3. **Include benchmarks** - "Your institution vs. community average"
4. **Be specific about severity** - Use CVSS, incident categories
5. **Always include recommendations** - Actionable, prioritized
6. **Professional tone throughout** - This represents Switch

## Anti-Patterns
- Alarmist language ("critical breach!")
- Vague recommendations ("improve security")
- Missing context ("12 incidents" - is that good or bad?)
- Inconsistent terminology between DE/FR versions
```

---

## Context: Narratuos Theater Social Media

Playful German-language social media for the impro theater group.

### Voice DNA (`contexts/narratuos/voice-dna.json`)

```json
{
  "meta": {
    "version": "1.0",
    "context": "narratuos",
    "description": "Improvisationstheater social media presence"
  },
  "voice": {
    "tone": ["playful", "warm", "inviting", "spontaneous"],
    "perspective": "first-person plural (wir) or direct address (du)",
    "formality": "casual-friendly, like talking to a friend",
    "humor": "frequent, inclusive, never mean",
    "verbosity": "short and punchy for social, slightly longer for announcements"
  },
  "style": {
    "sentenceLength": "short, energetic",
    "paragraphLength": "very short, often single sentences",
    "transitionStyle": "conversational flow",
    "openingPatterns": ["direct invitation", "playful question", "teaser"],
    "closingPatterns": ["call to action", "emoji flourish", "anticipation builder"]
  },
  "vocabulary": {
    "preferred": ["spontan", "einzigartig", "Moment", "Geschichte", "gemeinsam"],
    "avoided": ["professional", "corporate speak", "formal German"],
    "emojis": "yes! 🎭✨🎪 but not excessive"
  },
  "brand": {
    "tagline": "Spontan · Einzigartig · Unvergesslich",
    "themes": ["spontaneity", "uniqueness", "shared experience", "magic of the moment"],
    "hashtags": ["#narratuos", "#impro", "#improtheater", "#zürich"]
  }
}
```

### Audience (`contexts/narratuos/audience.json`)

```json
{
  "primaryReader": {
    "description": "Culture-curious Zürich resident",
    "age": "25-55",
    "interests": ["theater", "live entertainment", "comedy", "unique experiences"],
    "language": "German (Swiss German understood, written in Hochdeutsch)"
  },
  "platforms": {
    "instagram": "Visual focus, Stories, event announcements",
    "facebook": "Events, longer posts, community building"
  },
  "engagementGoals": {
    "show_announcement": "Drive ticket sales, create anticipation",
    "engagement_post": "Build community, increase reach",
    "behind_scenes": "Humanize the group, create connection"
  }
}
```

### Content Types & Templates

| Type | Platform | Length | Tone |
|------|----------|--------|------|
| Show Announcement | IG/FB | 100-200 chars + details | Excited, inviting |
| Story Post | IG Stories | <50 chars | Punchy, visual |
| Engagement Post | IG/FB | 50-150 chars | Playful, interactive |
| Behind the Scenes | IG/FB | 100-200 chars | Warm, personal |
| Event Reminder | IG/FB | 50-100 chars | Urgent, friendly |

### Team References

```json
{
  "members": [
    {"name": "Karin", "emoji": "🐱", "style": "warmth, observation"},
    {"name": "Luki", "emoji": "🔬", "style": "analytical surprises"},
    {"name": "Sebi", "emoji": "💪", "style": "physical comedy, depth"},
    {"name": "Jens-Christian", "emoji": "🎹", "style": "musical, connections"}
  ],
  "collective": "Narratuos",
  "venue": "Töpferei"
}
```

### Example Posts

**Show Announcement:**
```
🎭 Wintergeschichten - 21. Dezember

Wenn die Tage kürzer werden, werden unsere Geschichten länger.
Und spontaner. Und vielleicht auch etwas verrückter. ❄️

Bringt eure Ideen mit - wir machen daraus Magie! ✨

📍 Töpferei
⏰ 19:00 Uhr
🎟️ Link in Bio

#narratuos #impro #zürich #wintergeschichten
```

**Engagement Post:**
```
Welches Wort beschreibt euren Tag heute mit nur einem Emoji?

Wir starten: 🎲

(Vielleicht wird daraus ja eine Szene am Samstag... 😏)
```

**Behind the Scenes:**
```
Probe gestern: Luki als Baum. Sebi als Wind. Karin als...
wir wissen es immer noch nicht.

Das ist Impro. 🌳💨❓

#behindthescenes #narratuos
```

---

## Writing Skills

### Skill 1: Blog Writer (`skills/blog-writer/SKILL.md`)

```markdown
---
name: blog-writer
description: Generate blog posts matching the invisible.ch voice. USE WHEN user wants to write a post, draft content, create an article, OR needs help starting a blog piece.
---

# Blog Writer Skill

Generates blog content that sounds authentically like Jens-Christian.

## Activation
This skill activates automatically when writing for invisible.ch.

## Process

1. **Load Context**
   - Read `context/voice-dna.json`
   - Read `context/icp.json`
   - Read category guide for target category
   - Load relevant examples from `knowledge/best-posts/`

2. **Understand Intent**
   - What category? (musings/music/code/art)
   - What's the core message?
   - Who specifically benefits from reading this?
   - What makes this worth publishing?

3. **Generate Draft**
   - Apply voice DNA constraints
   - Match category patterns
   - Include personal perspective
   - Vary sentence structure

4. **Self-Check**
   - Does this sound like JCF or generic AI?
   - Is there a clear point?
   - Would the target reader share this?

## Anti-Patterns (Never Do These)
- "In this post, I will discuss..."
- "Let's dive into..."
- Numbered lists for everything
- Excessive hedging ("I think maybe perhaps...")
- Generic conclusions ("In conclusion...")
```

### Skill 2: Post Improver (`skills/post-improver/SKILL.md`)

```markdown
---
name: post-improver
description: Enhance existing drafts while preserving voice. USE WHEN user has a draft to improve, wants feedback on writing, OR needs help refining a post.
---

# Post Improver Skill

Refines drafts without overwriting the author's voice.

## Process

1. **Analyze Current Draft**
   - Identify voice consistency issues
   - Find structural problems
   - Note unclear sections
   - Check against category norms

2. **Suggest, Don't Replace**
   - Offer alternatives, not rewrites
   - Explain why changes help
   - Preserve intentional style choices

3. **Enhancement Categories**
   - Clarity: Ambiguous → precise
   - Flow: Jarring → smooth
   - Impact: Weak → strong (openings, closings)
   - Voice: Generic → distinctive

4. **Output Format**
   - Show original → suggested side by side
   - Explain reasoning
   - Let author choose
```

### Skill 3: SEO Optimizer (`skills/seo-optimizer/SKILL.md`)

```markdown
---
name: seo-optimizer
description: Optimize posts for search without compromising voice. USE WHEN user needs SEO help, wants better descriptions, OR is preparing to publish.
---

# SEO Optimizer Skill

Handles SEO so the writer can focus on writing.

## Focus Areas

1. **Title Optimization**
   - Include primary keyword naturally
   - Keep under 60 characters
   - Make it compelling, not clickbait

2. **Description Generation**
   - 150-160 characters
   - Answer "what will I learn/feel?"
   - Include secondary keyword

3. **Tag Suggestions**
   - Primary technology/topic
   - Content type (tutorial, reflection, announcement)
   - Skill level if applicable

4. **Content Structure**
   - Suggest H2/H3 structure
   - Identify keyword opportunities
   - Recommend internal links
```

### Skill 4: Voice Trainer (`skills/voice-trainer/SKILL.md`)

```markdown
---
name: voice-trainer
description: Learn and refine voice DNA from examples. USE WHEN user wants to update voice profile, analyze writing patterns, OR train on new samples.
---

# Voice Trainer Skill

Improves voice DNA accuracy over time.

## Process

1. **Collect Samples**
   - User provides URLs or files
   - Extract text content
   - Note category and date

2. **Analyze Patterns**
   - Sentence structure distributions
   - Vocabulary frequency
   - Opening/closing patterns
   - Paragraph lengths

3. **Update Voice DNA**
   - Merge new patterns with existing
   - Note contradictions for review
   - Version the changes

4. **Validation**
   - Generate sample paragraph
   - User confirms accuracy
   - Iterate if needed
```

---

## New Commands

### `/posts:brainstorm`

```markdown
---
description: Generate blog post ideas based on recent interests
argument-hint: [topic area] [--category musings|music|code|art]
---

Generate blog post ideas that fit invisible.ch.

## Process
1. Load context profiles
2. Consider recent posts (avoid repetition)
3. Generate 5-10 ideas with:
   - Working title
   - One-line premise
   - Suggested category
   - Why it matters to readers
4. Let user select or combine ideas
```

### `/posts:outline`

```markdown
---
description: Create a structured outline for a post
argument-hint: <title or topic> [--category]
---

Create a detailed outline before writing.

## Process
1. Load category guide
2. Determine optimal structure
3. Generate:
   - Hook options (3 alternatives)
   - Section breakdown with key points
   - Potential examples/code/images
   - Closing approach
4. Get user approval before drafting
```

### `/posts:expand`

```markdown
---
description: Expand an outline or notes into a full draft
argument-hint: <filename>
---

Turn an outline into a draft.

## Process
1. Read outline/notes file
2. Activate blog-writer skill
3. Generate full prose
4. Maintain outline structure
5. Flag sections needing author input
6. Save as draft, show for review
```

### `/posts:polish`

```markdown
---
description: Final refinement pass before publishing
argument-hint: <filename>
---

Final polish before publishing.

## Process
1. Read draft
2. Activate post-improver skill
3. Run SEO optimizer
4. Generate:
   - Line-edit suggestions
   - Final description
   - Tag recommendations
   - Checklist for /posts:check
5. Show diff for approval
```

---

## Workflows by Context

### invisible.ch Blog Flow

```
1. /write:brainstorm invisible music
   → "5 ideas for music posts..."
   → User picks: "Production notes for upcoming album"

2. /write:outline invisible "Production notes for Analog Dreams"
   → Structured outline with sections
   → User refines, adds details

3. /posts:new "Production notes for Analog Dreams" --category music
   → Creates file with frontmatter
   → Paste/merge outline

4. /write:draft invisible content/posts/2025/...
   → Generates full draft in JCF voice
   → User reviews, edits

5. /write:polish content/posts/2025/...
   → Final suggestions + SEO
   → Ready to publish
```

### Switch Security Flow

```
1. /write:context switch-security
   → Loads professional voice, DE/FR terminology

2. /write:draft switch-security monthly-report
   → Pulls data from reporter tool
   → Generates structured report
   → Applies DE/FR translations

3. /write:polish [draft file]
   → Terminology consistency check
   → Professional tone verification
   → Ready for PDF generation
```

### Narratuos Social Flow

```
1. /write:context narratuos
   → Loads playful voice, team info

2. /write:draft narratuos show-announcement
   → Interactive: asks about show details
   → Generates post with emojis, hashtags

3. Copy to clipboard → paste to Instagram/Facebook
```

---

## Unified Commands

| Command | Purpose | Example |
|---------|---------|---------|
| `/write:context [name]` | Switch active context | `/write:context narratuos` |
| `/write:brainstorm [ctx] [topic]` | Generate ideas | `/write:brainstorm invisible AI` |
| `/write:outline [ctx] [topic]` | Create structure | `/write:outline switch-security report` |
| `/write:draft [ctx] [type]` | Generate content | `/write:draft narratuos engagement` |
| `/write:polish [file]` | Refine any draft | `/write:polish draft.md` |
| `/write:translate [file] [lang]` | Translate (Switch) | `/write:translate report.md fr` |

---

## Implementation Phases

### Phase 1: Core Infrastructure
- [ ] Create `~/.claude/skills/writer/` directory structure
- [ ] Implement master SKILL.md with context switching
- [ ] Set up context-specific subdirectories

### Phase 2: invisible.ch Context (Personal Blog)
- [ ] Analyze 20+ existing posts for voice-dna.json
- [ ] Write audience.json and identity.json
- [ ] Create category guides (musings, music, code, art)
- [ ] Curate 5 best-posts examples per category
- [ ] Test with real blog post creation

### Phase 3: Switch Security Context (Professional)
- [ ] Create voice-dna.json for formal/professional tone
- [ ] Build terminology.json (DE/FR security terms)
- [ ] Create report templates (monthly, incident, recommendation)
- [ ] Integrate with ~/work/reporter tool
- [ ] Test with mock security report

### Phase 4: Narratuos Context (Social Media)
- [ ] Create voice-dna.json for playful German voice
- [ ] Build team.json with member info
- [ ] Create social media templates
- [ ] Add emoji and hashtag guidance
- [ ] Test with show announcement post

### Phase 5: Shared Skills & Polish
- [ ] Implement post-improver skill (works across contexts)
- [ ] Implement voice-trainer skill
- [ ] Create unified /write:* commands
- [ ] Add context auto-detection (by working directory)
- [ ] Documentation and examples

---

## Technical Notes

### Context Auto-Detection

The system can auto-detect context based on working directory:
- `~/work/web/invisible_ch/` → invisible context
- `~/work/reporter/` → switch-security context
- `~/work/web/narratuos-website/` → narratuos context

### File Locations

| Context | Output Location | Format |
|---------|-----------------|--------|
| invisible.ch | `content/posts/YYYY/YYYY-MM-DD-slug.md` | Hugo markdown |
| Switch Security | `~/work/reporter/drafts/` | Markdown → PDF |
| Narratuos | Clipboard (pbcopy) | Plain text for social |

### invisible.ch Fix
The existing commands reference `content/blog/` but active posts are in `content/posts/YYYY/`. Update commands to use correct path.

### Voice Consistency
The most critical aspect is maintaining distinct voices per context. Every skill must:
1. Load the correct context's voice-dna.json before generating
2. Self-check against context-specific anti-patterns
3. Never mix voices across contexts (German formality ≠ blog casual ≠ theater playful)

### Language Handling

| Context | Primary | Secondary | Notes |
|---------|---------|-----------|-------|
| invisible.ch | English | German (occasional) | Technical terms often in English |
| Switch Security | German | French | Must maintain parallel DE/FR versions |
| Narratuos | German | - | Hochdeutsch, but Swiss-friendly |

---

## Success Metrics

### invisible.ch
- **Voice Fidelity**: Can readers tell which posts had AI assistance?
- **Time Savings**: Faster from idea to published post
- **Quality Consistency**: Fewer posts abandoned mid-draft

### Switch Security
- **Professional Tone**: Passes review without "sounds like AI" feedback
- **Terminology Consistency**: DE/FR versions use same technical terms
- **Efficiency**: Reports generated faster with less manual editing

### Narratuos
- **Engagement**: Posts that feel authentic get more interaction
- **Brand Consistency**: Every post sounds like Narratuos
- **Output Speed**: From show details to ready-to-post in minutes

---

## Next Steps

1. **Approve this design** - Review contexts and architecture
2. **Decide starting context** - Which context to build first?
   - invisible.ch (most content to analyze)
   - Narratuos (simplest, quick win)
   - Switch Security (most structured)
3. **Implement Phase 1** - Core infrastructure
4. **Build first context** - Full implementation and testing
5. **Iterate** - Add remaining contexts

---

## Summary: Three Voices, One System

| | invisible.ch | Switch Security | Narratuos |
|---|---|---|---|
| **Tone** | Thoughtful, curious | Formal, precise | Playful, warm |
| **Language** | English | German/French | German |
| **Length** | 100-2000 words | Structured reports | 50-200 chars |
| **Emojis** | Rare | Never | Frequent |
| **Output** | Hugo blog | PDF reports | Social posts |

The system maintains these distinct voices while sharing common infrastructure for improvement, training, and workflow management.

---

*This design adapts Alex McFarland's co-writing system architecture for multiple writing contexts, enabling authentic voice switching between personal blog, professional communications, and creative social media.*
