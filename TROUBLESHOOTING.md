# Troubleshooting Guide

Common issues and solutions for Eldar Translate.

## Table of Contents

- [Installation Issues](#installation-issues)
- [Server Setup Problems](#server-setup-problems)
- [Translation Issues](#translation-issues)
- [Browser Compatibility](#browser-compatibility)
- [Performance Issues](#performance-issues)
- [Error Messages](#error-messages)
- [Data Loading Problems](#data-loading-problems)
- [Development Issues](#development-issues)

## Installation Issues

### Problem: "Cannot find module" or "Module not found"
**Symptoms:** Error messages about missing modules or files
**Solutions:**
1. Ensure you're serving the project over HTTP (not file://)
2. Check that all files are in the correct directory structure
3. Verify the `js/` and `data/` directories exist with required files

### Problem: Batch script won't run on Windows
**Symptoms:** Double-clicking `start-server.bat` does nothing
**Solutions:**
1. Right-click the batch file and select "Run as administrator"
2. Check if Python, Node.js, or PHP is installed: `python --version`, `node --version`, `php --version`
3. Try running the batch file from Command Prompt to see error messages

### Problem: Permission denied errors
**Symptoms:** Cannot access files or start server
**Solutions:**
1. Run terminal/command prompt as administrator
2. Check file permissions in the project directory
3. Ensure the port (3015) is not already in use

## Server Setup Problems

### Problem: "Port 3015 is already in use"
**Symptoms:** Server fails to start with port conflict message
**Solutions:**
1. Kill existing process using port 3015:
   ```bash
   # Windows
   netstat -ano | findstr :3015
   taskkill /PID <PID> /F
   
   # Mac/Linux
   lsof -ti:3015 | xargs kill -9
   ```
2. Use a different port:
   ```bash
   python -m http.server 3016
   ```

### Problem: "Command not found" errors
**Symptoms:** Terminal doesn't recognize python, node, or php commands
**Solutions:**
1. **Python not found:**
   - Windows: Install from python.org or Microsoft Store
   - Mac: Install via Homebrew: `brew install python`
   - Linux: `sudo apt install python3`

2. **Node.js not found:**
   - Install from nodejs.org
   - Or use package managers: `brew install node`, `sudo apt install nodejs npm`

3. **PHP not found:**
   - Windows: Install XAMPP or download from php.net
   - Mac: `brew install php`
   - Linux: `sudo apt install php`

### Problem: Server starts but page won't load
**Symptoms:** Server runs but browser shows "This site can't be reached"
**Solutions:**
1. Check if you're using the correct URL: `http://localhost:3015`
2. Try `http://127.0.0.1:3015` instead
3. Disable firewall temporarily to test
4. Try a different browser
5. Check if antivirus is blocking the connection

## Translation Issues

### Problem: Translations show as "[word]" in brackets
**Symptoms:** Untranslated words appear in square brackets
**Solutions:**
1. This is normal behavior for words not in the dictionary
2. Check if you're using the correct language (Quenya/Sindarin/Grey Company)
3. Try alternative spellings or synonyms
4. Check the Master Alphabet Browser to see if the word exists

### Problem: Translation appears incorrect or nonsensical
**Symptoms:** Translation doesn't match expected meaning
**Solutions:**
1. Remember this is dictionary-based translation, not AI translation
2. Check the word-by-word translation in the Master Alphabet Browser
3. Try simpler sentences with common words
4. Verify the direction (English→Elvish or Elvish→English)

### Problem: Auto-translation is too slow or too fast
**Symptoms:** Translation delays or happens too quickly while typing
**Solutions:**
1. The debounce delay is set to 500ms by default
2. For slower typing, this can be adjusted in the code
3. Clear the browser cache and reload the page
4. Check if other browser tabs are using excessive resources

### Problem: Copy function doesn't work
**Symptoms:** Copy button doesn't copy text to clipboard
**Solutions:**
1. Modern browsers require HTTPS for clipboard access
2. Use Ctrl+C to copy selected text manually
3. Check if browser permissions are blocking clipboard access
4. Try a different browser

## Browser Compatibility

### Problem: Page doesn't load or shows errors
**Symptoms:** Blank page, console errors, or layout issues
**Solutions:**
1. **Browser too old:** Requires Chrome 61+, Firefox 60+, Safari 12+, Edge 79+
2. **JavaScript disabled:** Enable JavaScript in browser settings
3. **ES6 modules not supported:** Update browser or use a compatibility layer
4. **CORS issues:** Ensure you're serving over HTTP, not opening the file directly

### Problem: Fonts don't display correctly
**Symptoms:** Text appears in default fonts instead of medieval styling
**Solutions:**
1. Check internet connection (fonts loaded from Google Fonts)
2. Clear browser cache and reload
3. Check if content blockers are preventing font loading
4. Try a different browser

### Problem: Icons don't appear
**Symptoms:** Missing or broken icons throughout the interface
**Solutions:**
1. Check internet connection (Lucide icons loaded from CDN)
2. Verify the Lucide CDN is accessible
3. Check browser console for loading errors
4. Try reloading the page

## Performance Issues

### Problem: Page loads slowly or freezes
**Symptoms:** Long loading times or unresponsive interface
**Solutions:**
1. **Initial load is slow:** Normal, loading 6,500+ vocabulary entries
2. **Ongoing performance issues:**
   - Close other browser tabs
   - Disable browser extensions
   - Clear browser cache
   - Restart browser
3. **Memory issues:** Check if system has sufficient RAM (translator uses ~50-100MB)

### Problem: Translations take too long
**Symptoms:** Noticeable delay between typing and translation
**Solutions:**
1. Check if running on a slow device
2. Reduce text length for testing
3. Check browser developer tools for errors
4. Try refreshing the page to reload vocabularies

## Error Messages

### "Failed to load ancient dictionaries"
**Symptoms:** Error dialog appears on page load
**Solutions:**
1. Check internet connection
2. Verify all files in `/data/` directory exist
3. Check browser console for specific file loading errors
4. Try the "Retry" button in the error dialog
5. Check if files are corrupted by comparing file sizes

### "Translation Error"
**Symptoms:** Error message appears in translation output
**Solutions:**
1. Check browser console for detailed error messages
2. Try translating a simple word like "star" or "friend"
3. Verify the translator is fully initialized
4. Refresh the page and try again

### "Module not found" or "Cannot resolve module"
**Symptoms:** Console errors about missing modules
**Solutions:**
1. Ensure serving over HTTP (not file://)
2. Check that `js/translator.js` exists
3. Verify file paths in the HTML match actual file locations
4. Try serving from a different HTTP server

## Data Loading Problems

### Problem: Vocabularies fail to load
**Symptoms:** Empty dictionary search results or failed translations
**Solutions:**
1. **Check data files exist:**
   ```
   data/
   ├── eldamo.json
   ├── ardalambion.json
   ├── hisweloke.json
   └── [other vocabulary files]
   ```
2. **Verify file permissions:** Ensure web server can read files
3. **Check file integrity:** Compare file sizes with repository
4. **Network issues:** Try downloading fresh copies of vocabulary files

### Problem: "Priority" or "Source" errors
**Symptoms:** Console errors about missing priority or source fields
**Solutions:**
1. This indicates corrupted vocabulary files
2. Re-download the vocabulary files from the repository
3. Check if any files were edited manually
4. Verify JSON syntax is valid

## Development Issues

### Problem: Code changes don't take effect
**Symptoms:** Modifications to code don't appear in browser
**Solutions:**
1. **Browser cache:** Hard refresh with Ctrl+F5 or Cmd+Shift+R
2. **Module caching:** Add `?v=timestamp` to module imports
3. **Service worker:** Disable service worker in browser dev tools
4. **Development server:** Restart the HTTP server

### Problem: Cannot debug or inspect code
**Symptoms:** Browser dev tools don't show source code
**Solutions:**
1. Open browser dev tools (F12)
2. Check the "Sources" tab for your files
3. Ensure source maps are enabled
4. Try a different browser for debugging

### Problem: Integration with other frameworks fails
**Symptoms:** Cannot import or use translator in React/Vue/etc.
**Solutions:**
1. **ES6 modules:** Ensure your build system supports ES6 modules
2. **Fetch polyfill:** Add fetch polyfill for older browsers
3. **File loading:** Adjust file paths for your build system
4. **Webpack/Vite:** Configure module resolution properly

## Getting Help

If you're still experiencing issues:

1. **Check browser console** for detailed error messages
2. **Test with minimal setup** using just the basic HTML file
3. **Try different browsers** to isolate browser-specific issues
4. **Check network connectivity** for CDN resources
5. **Verify file permissions** and directory structure
6. **Create an issue** on the repository with:
   - Operating system and version
   - Browser and version
   - Error messages from console
   - Steps to reproduce the issue
   - Expected vs actual behavior

## Diagnostic Commands

### Check server status:
```bash
# Check if port 3015 is in use
netstat -ano | findstr :3015  # Windows
lsof -i :3015                 # Mac/Linux

# Test if server is responding
curl http://localhost:3015    # Should return HTML
```

### Check file integrity:
```bash
# Verify critical files exist
ls -la js/translator.js
ls -la data/eldamo.json
ls -la debug-pronouns.json

# Check file sizes (should not be 0 bytes)
du -h data/*.json
```

### Browser debugging:
```javascript
// Test in browser console
console.log(window.eldarApp);  // Should show app instance
console.log(window.eldarApp.translator.isReady);  // Should be true
```

## Common File Permission Issues

### Linux/Mac:
```bash
# Fix permissions
chmod 755 .
chmod 644 *.html *.md *.js *.json
chmod 755 js/ data/
chmod 644 js/* data/*
```

### Windows:
- Right-click project folder → Properties → Security
- Ensure "Everyone" has read permissions
- For IIS/Apache: ensure web server user has read access

---

*If none of these solutions work, please create an issue on the repository with detailed information about your setup and the specific error messages you're seeing.* 