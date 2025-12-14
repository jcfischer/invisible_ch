---
description: Create a new photo gallery
argument-hint: <gallery title>
---

Create a new photo gallery for invisible.ch.

**Arguments provided:** $ARGUMENTS

## Instructions

1. **Generate directory name**:
   - Format: `YYYY-MM-DD` (today's date)
   - Location: `content/galleries/[date]/`

2. **Create the gallery structure**:
   ```
   content/galleries/YYYY-MM-DD/
   ├── index.md
   └── (images will go here)
   ```

3. **Create index.md** with this frontmatter:

```yaml
---
title: "[Title from arguments]"
date: [ISO 8601 format]
tags: [""]
type: gallery
---

[Gallery description here]
```

4. **Show next steps**:
   - Created directory path
   - Instructions to add images:
     - Copy images to the gallery directory
     - Supported formats: jpg, png, gif
     - Images will be automatically resized
   - Preview command: `hugo server -D`
   - Preview URL: http://localhost:1313/galleries/

5. **Image tips**:
   - Hugo will generate responsive thumbnails automatically
   - Original images should be high quality (1200px+ width recommended)
   - Use descriptive filenames for accessibility
