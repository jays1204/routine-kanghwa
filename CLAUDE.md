# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

A password-protected static HTML invitation page for a Ganghwa Island BBQ gathering. No build system or package manager — the entire app lives in a single `index.html` file with inline CSS and JS.

## Deployment

Hosted on **Cloudflare Pages**. Deploy by pushing to the `main` branch. The `_headers` file applies `Cache-Control: no-store` to all routes to prevent caching of the invitation content.

## Architecture

Everything is in `index.html`:

- **Lock screen** — 4-digit PIN gate (hardcoded `PASSWORD` constant). Uses a visually hidden `<input>` driven by dot indicators.
- **Invitation content** — revealed after correct PIN via CSS `display` toggle with a fade-out animation on the lock screen.
- **D-Day counter** — calculates days remaining to `EVENT_DATE_KST` using KST timezone via `Intl.DateTimeFormat`. Supports a `?kstDate=YYYY-MM-DD` query param for preview/testing.
- **Pair notice** — toggled based on whether today (KST) is on or after `PAIR_ANNOUNCE_DATE_KST`.
- **Modals** — clicking the BBQ SVG opens an image modal; clicking the invitation card opens an attendee list modal. Both close on backdrop click or Escape key.

## Key Constants (in `<script>`)

| Constant | Purpose |
|---|---|
| `PASSWORD` | 4-digit PIN to unlock the invitation |
| `EVENT_DATE_KST` | BBQ event date `{y, m, d}` |
| `PAIR_ANNOUNCE_DATE_KST` | Date from which pair assignments are shown |
| `PAIR_NOTICE_BEFORE/AFTER` | Text toggled before/after announcement date |
