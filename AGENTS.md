# Single-Page Browser Tool Guidelines

Rules and patterns for creating self-contained, single-page HTML tools that run entirely in the browser.

## Core Principles

1. **No server-side component** - All processing must happen client-side via JavaScript
2. **Single HTML file** - CSS and JavaScript should be inline, not in separate files
3. **Minimal dependencies** - Prefer vanilla JavaScript; use CDN-hosted libraries only when necessary (e.g., JSZip for ZIP file creation)

## File Structure

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Tool Name</title>
    <!-- CDN dependencies if needed -->
    <style>
        /* All CSS inline */
    </style>
</head>
<body>
    <!-- Minimal HTML structure -->
    <script>
        // All JavaScript inline
    </script>
</body>
</html>
```

## Styling Guidelines

- Use a dark theme with good contrast
- Keep the interface minimal and focused
- Use system fonts for fast loading
- Provide clear visual hierarchy

```css
body {
    font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
    max-width: 800px;
    margin: 0 auto;
    padding: 40px 20px;
}
```

## Recommended Libraries (CDN)

| Library | Use Case | CDN |
|---------|----------|-----|
| JSZip | Creating ZIP files | `https://cdnjs.cloudflare.com/ajax/libs/jszip/3.10.1/jszip.min.js` |

## Adding a New Tool

When adding a new tool to the repository:

1. **Create the tool folder and file**
   ```
   /new-tool-name/
   └── index.html
   ```

2. **Update the landing page** (`/index.html`)

   Add a new card to the `.tools-grid` section:
   ```html
   <a href="new-tool-name/" class="tool-card">
       <h2>Tool Display Name</h2>
       <p>Brief description of what the tool does.</p>
   </a>
   ```

3. **Update the README** (`/README.md`)

   Add a row to the Available Tools table:
   ```markdown
   | [Tool Display Name](https://hjoliveira.github.io/tools/new-tool-name/) | Brief description |
   ```
