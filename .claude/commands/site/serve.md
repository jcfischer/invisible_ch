---
description: Start Hugo dev server with drafts
---

Start the Hugo development server to preview the site.

## Instructions

1. **Start the server**:
   ```bash
   hugo server -D --navigateToChanged
   ```

   Flags:
   - `-D`: Include draft posts
   - `--navigateToChanged`: Auto-navigate to changed content

2. **Report**:
   - Server URL: http://localhost:1313/
   - Show any build warnings
   - Remind user to press Ctrl+C to stop

3. **Quick links**:
   - Home: http://localhost:1313/
   - Blog: http://localhost:1313/categories/musings/
   - Galleries: http://localhost:1313/galleries/
