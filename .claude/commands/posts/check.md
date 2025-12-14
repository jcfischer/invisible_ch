---
description: Check a post for issues (links, spelling, SEO)
argument-hint: <filename or title>
---

Check a blog post for common issues before publishing.

**Arguments provided:** $ARGUMENTS

## Instructions

1. **Find the post** in `content/blog/` matching the argument

2. **Run these checks**:

### Frontmatter Check
- [ ] Title is set and descriptive
- [ ] Description is filled in (important for SEO)
- [ ] Category is valid (musings, music, code, art)
- [ ] Tags are set (at least one recommended)
- [ ] Date is set correctly

### Content Check
- [ ] Post has actual content (not just placeholder)
- [ ] Word count (report total)
- [ ] Estimated reading time

### Link Check
- Extract all URLs (markdown links and raw URLs)
- Verify each link is accessible
- Report broken or redirecting links

### Image Check
- Find all image references
- Verify images exist in the expected location
- Check for missing alt text

3. **Generate report**:

```
Post: [filename]
Title: [title]
Status: [draft/published]

Frontmatter: [OK/Issues found]
- ...

Content: [word count] words (~[X] min read)

Links: [X] total, [Y] broken
- ...

Images: [X] total, [Y] issues
- ...

Ready to publish: [Yes/No - with reasons]
```

4. **Suggestions** for any issues found
