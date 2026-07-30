# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this is

A single static HTML page (`index.html`) — an internal "studio overview" page for Dura Digital's Digital Engineering Studio. It lists the studio's practices (Data, Web Dev, Software Dev, Agents, Automation, RPA), the team roster grouped by practice, and the recurring meeting cadence. There is no build system, no package manager, no JavaScript, and no backend — the entire site is one HTML file with an inline `<style>` block. Fonts (Space Grotesk, IBM Plex Mono, Inter) are loaded from Google Fonts via `<link>` tags.

The page is marked `<meta name="robots" content="noindex, nofollow">` and the footer says "NOINDEX — INTERNAL PUBLIC PAGE" — it's meant to be reachable by URL but not indexed by search engines.

## Sensitive data & PII

This directory also holds a private, gitignored "Studio Lead Dashboard" (`digital-engineering-studio.html`) and its data file (`de_studio_notes.json`) — an internal tool with full names, emails, reporting lines, project/client assignments, and 1:1 notes. Both are excluded via `.gitignore` and must stay that way; don't add either to git without explicit instruction.

**No sensitive or PII data should ever ship — in tracked files, in commit messages/PR titles and descriptions, or in code comments.** Concretely:

- Full names beyond first-name + last-initial, personal emails, phone numbers, reporting-chain details, internal HR/management notes, and client/project names tied to named individuals stay out of anything committed or pushed — including commit message text, even when the source file itself is gitignored.
- Before committing or opening a PR, check the diff and the commit message for this kind of content, not just the file list.
- If it's unclear whether something counts as sensitive, ask before committing or pushing rather than assuming it's fine.

## Working with this repo

There is no build, lint, or test tooling — edit `index.html` directly and open it in a browser to preview (e.g. `start index.html` on Windows, or use a simple static file server if testing things like relative paths).

## Structure of index.html

The file is organized into clearly-commented sections in document order:

1. **`:root` CSS variables** — the entire color system lives here. Each practice has a dedicated accent color variable (`--data`, `--webdev`, `--swdev`, `--agents`, `--automation`, `--rpa`) that's threaded through as a `--pc` (practice color) custom property on individual elements (`.node`, `.roster-group-head`, `.chip`) so the border/dot/chip accent matches the practice. Meetings use a similar `--mc` (meeting color) pattern.
2. **Nav** — sticky header with anchor links to `#practices`, `#team`, `#meetings`.
3. **Hero** — title plus a "titleblock" (a technical-drawing-style summary table showing practice count, member count, scale, status).
4. **`#practices` section** — the "schematic": a 6-column grid (`.schematic` / `.node`), one node per practice, each with a lead name. Collapses to 2 columns under 900px.
5. **`#team` section** — the roster, grouped into `.roster-group` blocks (one per practice, plus a "Studio-wide" group for people not tied to a single practice). Each member is a `.member` row with initials in a colored `.chip`, name, role, and location (country, or "REMOTE").
6. **`#meetings` section** — recurring meeting cards (`.meeting`), each showing status, lead, description, and the next session date.
7. **Footer** — studio name and the noindex notice.

## Editing conventions to preserve

- **Accessibility features are intentional, not incidental** — keep them when editing: the skip link (`.skip-link`), `prefers-reduced-motion` handling, visible `:focus-visible` outlines, and the roster/titleblock `role="table"`/`role="row"`/`role="cell"` semantics. The `--muted` color was deliberately lightened from `#5c7793` to its current value to hit ~5.3:1 contrast on panel backgrounds — don't darken it back down without rechecking contrast.
- **Adding a person**: add a `.member` `<li>` inside the appropriate `.roster-group`'s `.roster-grid`, using the two-letter initials chip pattern, and update that group's `.rg-count` and the studio-wide member total in the titleblock (`Members` row).
- **Adding/changing a practice**: define a new color variable in `:root`, add a `.node` in the schematic, add a matching `.roster-group`, and update the titleblock's `Practices` count.
- **Updating meeting dates**: edit the `.meeting-next .val` text; the `.tbd` class exists for showing a placeholder like "TBD" in accent color when a date isn't set yet.
- Names throughout are deliberately truncated to first name + last initial (documented in the Team section's `.section-note`) — keep this format for consistency/privacy.
