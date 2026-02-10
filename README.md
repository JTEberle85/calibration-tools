# Role Calibration Tools

Interactive tools for understanding role expectations and competency progressions across consulting career tracks. Built as a static-site application with password-protected access.

## Features

- **Business Strategy Track** — Calibration tool for business strategy competency progression
- **Client Delivery Track** — Role expectations across client delivery levels
- **Market Solutions Track** — Market solutions competency framework
- **Team Operations Track** — Team operations role calibration
- **AI Benchmark** — Consulting AI readiness assessment
- **Our Story** — How this project was built with AI pair programming

## Tech Stack

- Vanilla HTML with inline React (JSX via Babel)
- Tailwind CSS for styling
- [StatiCrypt](https://github.com/robinmoisson/staticrypt) for client-side password protection
- GitHub Pages hosting
- No build system or server required

## Architecture

- `index.html` — StatiCrypt-encrypted login page (gateway)
- On successful login, sets a localStorage auth token (24-hour expiry)
- All other pages check for the auth token on load and redirect to login if missing/expired

## Getting Started

1. Clone the repository
2. Deploy to GitHub Pages or open `index.html` in a browser
3. Enter the site password to access the tools

## License

All rights reserved.
