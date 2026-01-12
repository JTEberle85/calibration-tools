# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Interactive role calibration tools for Slalom career tracks. This is a static HTML site hosted on GitHub Pages with password-protected content using StatiCrypt.

**Repository:** https://github.com/JTEberle85/calibration-tools.git

## Architecture

- **Static HTML files** - Each calibration tool is a self-contained HTML file with embedded CSS and JavaScript
- **StatiCrypt encryption** - Most HTML files are encrypted client-side using StatiCrypt (AES-256-CBC with PBKDF2 key derivation)
- **No build system** - Plain HTML/CSS/JS, no bundlers or frameworks
- **`encrypted/` folder** - Contains unencrypted source versions of files for editing

## Key Files

- `*.html` (root) - Password-protected encrypted versions served to users
- `encrypted/*.html` - Unencrypted source files for development/editing
- `.staticrypt.json` - Contains the salt used for encryption

## Encryption Workflow

StatiCrypt is installed globally via npm. To encrypt a file:

```bash
staticrypt <input.html> -p "***REDACTED***" --salt 9a33add92f11f72ec2c82098ef4dc579
```

To work on calibration tools:
1. Edit the unencrypted version in `encrypted/`
2. Re-encrypt with StatiCrypt using the same password and salt
3. Replace the encrypted file in the root directory
