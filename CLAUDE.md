# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Static website for **Kaunas JUG** (Java/JVM User Group) based in Kaunas, Lithuania, hosted at [kaunas-jug.lt](https://kaunas-jug.lt) via GitHub Pages. This is intentionally a simple HTML site — no build system, no framework, no package manager.

## Documentation

- [`docs/adding-new-event.md`](docs/adding-new-event.md) — step-by-step guide for adding a new JUG event (AI-ready, includes templates)

## Architecture

### Page structure

- `index.html` — the **current live page**, always updated to reflect the latest/upcoming event
- `index60.html` — archived snapshot of the JUG #60 event page

### Key sections in index.html

- **Header** (~line 1–75): Logo, email, social links (Facebook, Twitter, LinkedIn)
- **Sponsor bar** (~line 80–223): Active sponsors shown as `<img>` inside Bootstrap grid columns. Inactive sponsors are HTML-commented out (never deleted). Logo files live in `img/friends/`.
- **Jumbotron** (~line 229–285): The current event announcement. Toggled via `style="display: block"` (active) / `style="display: none"` (hidden). Contains the event title, ticket link, and Eventbrite checkout widget.
- **Past events table** (~line 288–end): All meetups listed newest-first, with talk titles, speaker names, and links to slides/videos/photos.

### Current event state (JUG #61)

- Last event: **#61**, 2025-11-27
- Next event number: **#62**
- Jumbotron: `display: none` (no active event)
- Last Eventbrite widget ID used: `1974743014515` (JUG #61)

### Assets

- `css/styles.css` — custom styles (Bootstrap 3 base framework)
- `img/friends/` — sponsor/partner logo files
- `material/meetupNN/` — slide decks uploaded after each meetup
- `support/index.html` — support/donation page
- `CNAME` — GitHub Pages custom domain (`kaunas-jug.lt`)

## Conventions

- Eventbrite URL pattern: `https://kaunas-jug{N}.eventbrite.com/`
- Default event time: **19:00–21:00** Europe/Vilnius; non-standard times are noted in the jumbotron `<h1>` with a `<small>` tag
- Talk links start as `javascript:alert('Comming soon...')` (note: "Comming" is the established spelling), updated to real URLs or `javascript:void(0)` after the event
- Sponsor logos: wrap inactive ones in `<!-- ... -->`, do not delete them
- No build step — edits to `index.html` are the deployment; GitHub Pages auto-deploys on push to `main`

## Currently active sponsors (JUG #61)

- Cognizant (`cognizant_logo.jpg`, 40px)
- JetBrains IntelliJ IDEA (`IntelliJ_IDEA.png`, 48px)
- Juvare (`juvare_logo.png`, 40px)
