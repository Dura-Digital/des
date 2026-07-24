# Digital Engineering Studio

[![pages-build-deployment](https://github.com/Dura-Digital/des/actions/workflows/pages/pages-build-deployment/badge.svg)](https://github.com/Dura-Digital/des/actions/workflows/pages/pages-build-deployment)

A single-page internal site for Dura Digital's Digital Engineering Studio. It's a lightweight overview of the studio: the practices that make it up, the team roster, and the recurring meeting cadence.

The page is marked `noindex, nofollow` — it's meant to be reachable by direct link, not indexed by search engines.

## Viewing locally

There's no build step or dependencies. Just open `index.html` in a browser:

```
start index.html
```

## What's on the page

- **Practices** — the six practices in the studio (Data, Web Dev, Software Dev, Agents, Automation, RPA), each with a practice lead.
- **Team** — the full roster, grouped by practice, showing name (first name + last initial), role, and location.
- **Meetings** — the recurring meetings that keep the studio in sync, including who leads them and the next scheduled session.

## Making changes

This is a single static HTML file (`index.html`) with all styling inline. See `CLAUDE.md` for a detailed breakdown of the page structure and conventions to follow when editing it (adding team members, practices, or updating meeting dates).
