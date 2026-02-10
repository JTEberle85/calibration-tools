# CLAUDE.md

See `~/.claude/josh-profile.md` for Josh's communication preferences (casual, punchy, step-by-step CLI guidance).

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Interactive role calibration tools for Slalom career tracks. This is a static HTML site hosted on GitHub Pages with password-protected content.

**Repository:** https://github.com/JTEberle85/calibration-tools.git

## Architecture

- **Static HTML files** - Each calibration tool is a self-contained HTML file with embedded CSS and JavaScript
- **Gateway authentication** - Single password entry on `index.html`, other pages use localStorage auth check
- **No build system** - Plain HTML/CSS/JS, no bundlers or frameworks

## Authentication Flow

1. `index.html` is encrypted with StatiCrypt - this is the login page
2. On successful password entry, sets `slalom-calibration-auth` token in localStorage (expires after 24 hours)
3. All other pages check for this token on load; redirect to `index.html` if missing/expired
4. Password: See `~/.claude/josh-profile.md` (not stored in repo)

## Key Files

- `index.html` - Encrypted login page (StatiCrypt)
- `*.html` (other) - Decrypted pages with auth-check script
- `decrypted_pages/` - Working folder for decrypted source files
- `.staticrypt.json` - Contains the salt used for encryption

## Re-encrypting index.html

If you need to update the landing page content:

```bash
# Decrypt current index.html
staticrypt --decrypt -p "YOUR_PASSWORD" index.html -d decrypted_pages

# Edit decrypted_pages/index.html

# Re-encrypt
staticrypt decrypted_pages/index.html -p "YOUR_PASSWORD" --salt 9a33add92f11f72ec2c82098ef4dc579 -d .
```

## Adding Auth Check to New Pages

Add this script immediately after `<head>`:

```html
<script>
    (function() {
        var auth = localStorage.getItem('slalom-calibration-auth');
        var authTime = localStorage.getItem('slalom-calibration-auth-time');
        var maxAge = 24 * 60 * 60 * 1000; // 24 hours
        if (auth !== 'authenticated' || !authTime || (Date.now() - parseInt(authTime)) > maxAge) {
            window.location.href = 'index.html';
        }
    })();
</script>
```
