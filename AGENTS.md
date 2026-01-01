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

## User Interface

### File Upload
- Provide a drop zone for drag-and-drop file upload
- Also support click-to-browse as a fallback
- Use visual feedback for drag states (hover, dragover)

```javascript
dropZone.addEventListener('dragover', (e) => {
    e.preventDefault();
    dropZone.classList.add('dragover');
});

dropZone.addEventListener('drop', (e) => {
    e.preventDefault();
    dropZone.classList.remove('dragover');
    processFile(e.dataTransfer.files[0]);
});
```

### Status Feedback
- Show processing state while working
- Display success message with summary (e.g., "Converted 42 books")
- Show clear error messages when something fails

## Data Processing

### CSV Parsing
When parsing CSV files, handle:
- Quoted fields containing commas
- Escaped quotes (doubled quotes `""`)
- Fields containing newlines
- Different line endings (CRLF, LF)

```javascript
function parseCSV(text) {
    // First pass: split into lines, respecting quoted fields
    // Second pass: parse each line into fields
}
```

### File Output
- For multiple output files, use JSZip to create a ZIP archive
- Trigger download automatically when processing completes
- Use descriptive filenames for the output

```javascript
const zip = new JSZip();
zip.file('filename.md', content);
const blob = await zip.generateAsync({ type: 'blob' });

const url = URL.createObjectURL(blob);
const a = document.createElement('a');
a.href = url;
a.download = 'output.zip';
a.click();
URL.revokeObjectURL(url);
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

## Error Handling

- Validate file type before processing
- Check for required columns/data structure
- Wrap processing in try-catch
- Display user-friendly error messages

```javascript
try {
    // Processing logic
} catch (error) {
    console.error(error);
    showStatus('Error: ' + error.message, 'error');
}
```

## Recommended Libraries (CDN)

| Library | Use Case | CDN |
|---------|----------|-----|
| JSZip | Creating ZIP files | `https://cdnjs.cloudflare.com/ajax/libs/jszip/3.10.1/jszip.min.js` |
