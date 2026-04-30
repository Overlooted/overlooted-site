# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What This Is

The official website for **Overlooted**, a cozy cart-filling dungeon crawler game. Built with Hugo (Extended) and the Blowfish theme, deployed to GitHub Pages.

## Commands

```bash
# Start dev server (hot reload)
hugo server

# Production build
hugo --minify

# Create new content
hugo new content/devlog/post-name/index.md
```

No Node.js or npm — this is a pure Hugo site. Hugo Extended is required (handles SCSS compilation in the Blowfish theme).

## Architecture

**Theme:** Blowfish lives in `themes/blowfish/` as a git submodule. Override any theme file by placing a file at the same relative path under `layouts/` or `assets/`.

**Configuration split across `config/_default/`:**
- `hugo.toml` — base URL, module mounts, main sections
- `params.toml` — Blowfish theme parameters (color scheme, layout options, feature flags)
- `languages.en.toml` — author info and social links (single source of truth for social URLs)
- `menus.en.toml` — navigation menus (social links must be manually kept in sync with `languages.en.toml`)

**Content sections:**
- `content/devlog/` — development blog; each post is a directory with `index.md` and any bundled images
- `content/_index.md` — homepage with embedded YouTube trailer and newsletter signup
- `content/about/`, `content/press/`, `content/signup/` — static sections

**Custom layouts in `layouts/`** (these override Blowfish defaults):
- `partials/home/hero.html` — hides social links when `showSocialLinks: false` in frontmatter
- `partials/header/` — custom desktop/mobile navigation components
- `shortcodes/mailchimp.html` — newsletter signup form (HTML POST to Mailchimp)
- `shortcodes/social.html` — renders social icons from `params.author.links`

**Shortcode usage:**
```
{{< mailchimp >}}   # Renders the Mailchimp signup form
{{< social >}}      # Renders social link icons
```

## Content Frontmatter

Devlog posts use TOML frontmatter:
```toml
+++
title = "Post Title"
date = 2025-01-01T00:00:00+00:00
description = "Short description"
summary = "Summary shown in list views"
tags = ["tag1", "tag2"]
+++
```

## Key Blowfish Parameters

Color scheme is `"fire"` with dark mode default. Layout options (`hero`, `background`, `card`, etc.) and feature toggles (search, TOC, code copy) are all in `config/_default/params.toml`. Refer to [Blowfish docs](https://blowfish.page/docs/) for available parameters.
