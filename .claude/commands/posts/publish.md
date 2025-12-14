---
description: Publish a draft post (set draft:false, commit, push)
argument-hint: <filename or title>
---

Publish a draft blog post to invisible.ch.

**Arguments provided:** $ARGUMENTS

## Instructions

1. **Find the post**:
   - Search in `content/blog/` for a file matching the argument
   - Match by filename or title
   - If multiple matches, ask user to clarify

2. **Pre-publish checklist** - verify the post has:
   - [ ] Title set
   - [ ] Description filled in (warn if empty)
   - [ ] At least one category
   - [ ] Content (not just placeholder text)

3. **Check for broken links**:
   - Extract all URLs from the post
   - Verify each link is accessible
   - Report any broken links and ask if user wants to continue

4. **Update the post**:
   - Change `draft: true` to `draft: false`
   - Update the date to current time if it's older than today

5. **Git operations**:
   - Stage the file: `git add [filepath]`
   - Commit with message: `Publish: [post title]`
   - Push to origin

6. **Confirmation**:
   - Show the published post URL: `https://invisible.ch/YYYY/MM/DD/slug/`
   - Remind about any warnings (missing description, etc.)
