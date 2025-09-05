# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

NotionNext is a sophisticated static blog system built with Next.js and Notion API that transforms Notion pages into a fully-featured blog platform. It supports 20+ themes, multiple comment systems, and various deployment options including Vercel, Docker, and static exports.

## Development Commands

```bash
yarn dev          # Development server with hot reload
yarn build        # Production build
yarn start        # Production server
yarn export       # Static export with sitemap generation
yarn bundle-report # Bundle analysis
yarn build-all-in-dev # Development build with production settings
```

## Architecture

### Theme System
- Themes are located in `/themes` directory with 20+ available themes (hexo, next, medium, matery, etc.)
- Each theme has its own `/components` folder with theme-specific layouts
- Themes can be switched dynamically via URL parameters or configuration
- Theme components override default components when a theme is active

### Configuration Hierarchy
1. **Notion Config Table** - Database-driven configuration (highest priority)
2. **Environment Variables** - Deployment-specific settings (`.env.local`)
3. **blog.config.js** - Default configuration file with modular imports from `/conf/` directory

### Content Management
- Uses Notion as CMS through Notion API
- Implements SSG (Static Site Generation) with ISR (Incremental Static Regeneration)
- Multi-layer caching strategy: Redis, memory cache, Next.js cache
- Supports posts, pages, notices, menus, and sub-menus through Notion properties

### Key Directory Structure
```
components/     # Shared components (80+ components)
themes/         # Theme-specific components and layouts
pages/          # Next.js pages with dynamic routing
lib/            # Core utilities and Notion API integrations
conf/           # Modular configuration files
public/         # Static assets
styles/         # Global styles with Tailwind CSS
hooks/          # Custom React hooks
```

## Development Setup

1. **Node.js Requirement**: Node.js 20+ required
2. **Environment Setup**: Copy `.env.example` to `.env.local` and configure:
   - `NOTION_PAGE_ID`: Required Notion database page ID
   - Theme selection: `NEXT_PUBLIC_THEME`
   - Language settings: `NEXT_PUBLIC_LANG`
   - Other optional configurations

3. **Package Manager**: Use Yarn (recommended)

## Key Features and Integrations

### Comment Systems
Multiple comment providers supported:
- Twikoo, Giscus, Gitalk, Waline, Valine
- Cusdis, Utterances, WebMention
- Configuration in `conf/comment.config`

### Analytics
- Vercel Analytics (built-in)
- Google Analytics
- Baidu Tongji
- Busuanzi visitor counter
- Ackee analytics

### SEO Features
- Automatic sitemap generation
- Robots.txt
- Meta tags optimization
- Google/Baidu site verification
- RSS feed generation

### Widgets and Plugins
- Live2D pet widgets
- Music player (APlayer/MetingJS)
- Chatbot integrations
- Social sharing
- Search (Algolia integration)

## Important Development Notes

### Notion Property Mapping
The system maps Notion database properties through configuration in `blog.config.js`:
- Post types: Post, Page, Notice, Menu, SubMenu
- Status: Published, Invisible
- Standard fields: title, slug, category, date, tags, summary

### Internationalization
- Built-in i18n support with locale detection
- URL-based language switching (e.g., `/zh/article/slug`)
- Language files in `/lib/lang.js`

### Performance Optimizations
- Image optimization with Next.js Image component
- Lazy loading for posts and images
- Bundle splitting and code optimization
- Caching at multiple levels

### Deployment
- **Vercel**: Recommended with automatic builds
- **Docker**: Containerized deployment available
- **Static Export**: Use `yarn export` for static hosting
- Environment-specific builds with `VERCEL_ENV` variable