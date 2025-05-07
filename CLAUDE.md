# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a personal blog built with Astro, a modern static site generator. The site uses Markdown for content, TailwindCSS for styling, and TypeScript for type safety.

## Commands

### Development

- `npm install` - Install project dependencies
- `npm run dev` - Start the development server (http://localhost:4321)
- `npm run build` - Build the production site to `./dist/`
- `npm run preview` - Preview the production build locally before deploying
- `npm run astro ...` - Run Astro CLI commands

## Architecture

### Content Management

The blog content is stored as Markdown files in the `src/content/blog/` directory. Each post has frontmatter with metadata like title and publication date.

Content is fetched using Astro's Content Collections API:
```typescript
// Example from src/pages/index.astro
import { getCollection } from "astro:content";

// Get all blog posts sorted by publication date (newest first)
const posts = (await getCollection("blog")).sort(
  (a, b) => b.data.pubDate.valueOf() - a.data.pubDate.valueOf()
);
```

### Routing

- `src/pages/index.astro` - Home page that displays a list of blog posts
- `src/pages/about.astro` - About page
- `src/pages/blog/[...slug].astro` - Dynamic route for individual blog posts
- `src/pages/rss.xml.js` - Generates RSS feed

### Components

The site uses a component-based architecture with reusable Astro components:
- `BaseHead.astro` - Contains common head elements and meta tags
- `Header.astro` - Site navigation
- `Footer.astro` - Site footer
- `FormattedDate.astro` - Formats dates consistently throughout the site
- `Prose.astro` - Applies consistent typography to content

### Configuration

- `astro.config.mjs` - Astro configuration (plugins, site URL, etc.)
- `src/consts.ts` - Global constants like site title and description