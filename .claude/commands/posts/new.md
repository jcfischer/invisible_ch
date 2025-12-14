---
description: Create a new blog post with Hugo frontmatter
argument-hint: <title> [--category musings|music|code|art]
---

Create a new blog post for invisible.ch:

**Arguments provided:** $ARGUMENTS

## Instructions

1. **Parse the title** from arguments (everything before `--category` if present)

2. **Determine category** (default: musings):
   - If `--category` flag provided, use that value
   - Valid categories: musings, music, code, art

3. **Generate filename**:
   - Format: `YYYY-MM-DD-slug.md`
   - Date: Use today's date
   - Slug: Convert title to kebab-case (lowercase, hyphens for spaces, remove special chars)

4. **Create the file** at `content/blog/[filename]` with this frontmatter:

```yaml
---
title: "[Title from arguments]"
date: [ISO 8601 format: YYYY-MM-DDTHH:MM:SS+00:00]
author: Jens-Christian Fischer
description: ""
categories: ["[category]"]
tags: [""]
slug: [slug-from-filename]
type: post
draft: true
---

[Write your post here]
```

5. **Open the file** for editing and show:
   - The created file path
   - Preview command: `hugo server -D`
   - Preview URL: http://localhost:1313/

6. **Suggest next steps**:
   - Add description for SEO
   - Add relevant tags
   - Write content
   - Use `/posts:publish` when ready
