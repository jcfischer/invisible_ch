---
description: Build the site for production
---

Build the Hugo site for production deployment.

## Instructions

1. **Clean previous build**:
   ```bash
   rm -rf public/
   ```

2. **Build the site**:
   ```bash
   hugo --gc --minify
   ```

   Flags:
   - `--gc`: Run garbage collection after build
   - `--minify`: Minify output (HTML, CSS, JS)

3. **Report**:
   - Number of pages generated
   - Build time
   - Any warnings or errors
   - Output directory: `public/`

4. **Deployment reminder**:
   - Built files are in `public/`
   - Ready for upload to hosting provider
