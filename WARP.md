# WARP.md

This file provides guidance to WARP (warp.dev) when working with code in this repository.

## Project Overview

AstroWind is a template built with **Astro 4.0** and **Tailwind CSS** for creating fast, SEO-friendly websites. This particular instance is customized for **LaMiDesign** (lamidesign.ca), a web design service for small businesses.

## Key Commands

### Development
```bash
# Start development server (localhost:3000)
npm run dev
# or
npm start

# Build for production
npm run build

# Preview production build
npm run preview

# Format code with Prettier
npm run format

# Run ESLint
npm run lint:eslint

# Run Astro CLI commands
npm run astro -- <command>
```

### Specific Development Tasks
```bash
# Add new Astro integration
npm run astro -- add <integration-name>

# Check for build issues
npm run astro -- check

# Generate types
npm run astro -- sync
```

## Architecture Overview

### Core Structure
- **Framework**: Astro 4.0 with static site generation
- **Styling**: Tailwind CSS with custom design system
- **Content**: Markdown/MDX with Astro Content Collections
- **Build**: Vite-based with custom AstroWind integration

### Key Directories

#### `/src/components/`
- `widgets/` - Page-level components (Header, Hero, Features, Footer, etc.)
- `ui/` - Reusable UI components (Button, Form, ItemGrid, etc.)
- `common/` - Utility components (Analytics, Image optimization, etc.)
- `blog/` - Blog-specific components (Grid, Pagination, SinglePost, etc.)

#### `/src/layouts/`
- `Layout.astro` - Base layout with metadata, styles, and scripts
- `PageLayout.astro` - Standard page layout
- `MarkdownLayout.astro` - Blog post layout
- `LandingLayout.astro` - Landing page specific layout

#### `/src/content/`
- Uses Astro Content Collections for type-safe content management
- `post/` - Blog posts in Markdown/MDX format
- `config.ts` - Content schema definitions with Zod validation

#### `/src/utils/`
- `blog.ts` - Blog post fetching, pagination, and permalink generation
- `permalinks.ts` - URL structure management
- `images.ts` - Image optimization utilities
- `frontmatter.mjs` - Remark/Rehype plugins for content processing

### Configuration System

#### Main Config (`src/config.yaml`)
Central configuration file that controls:
- Site metadata and SEO settings
- Blog functionality and pagination
- Analytics integration
- UI theme settings
- URL patterns and permalinks

#### Navigation (`src/navigation.js`)
Exports `headerData` and `footerData` objects that define site navigation structure.

#### Custom Integration (`vendor/integration/`)
Custom Astro integration that:
- Loads and processes the YAML config
- Provides virtual module `astrowind:config` for accessing config throughout the app
- Handles robots.txt and sitemap generation
- Manages build-time optimizations

### Content Management
- **Blog Posts**: Stored in `/src/content/post/` with frontmatter validation
- **Images**: Optimized using Astro Assets and Unpic for CDN integration
- **SEO**: Automatic Open Graph, Twitter Cards, and structured data
- **RSS**: Automatically generated from blog posts

### Styling System
- **Tailwind CSS** with custom color variables defined in CSS custom properties
- **Design tokens** managed through CSS variables (`--aw-color-*`)
- **Dark mode** support with class-based toggling
- **Typography plugin** for blog content styling

### Development Features
- **Hot reload** for config changes via file watching
- **TypeScript** support with strict type checking
- **ESLint** configuration for Astro, TypeScript, and accessibility
- **Prettier** for code formatting
- **Content schema validation** with Zod

## Important Files to Understand

- `astro.config.mjs` - Main Astro configuration with integrations
- `src/config.yaml` - Site-specific configuration (current: LaMiDesign)
- `src/navigation.js` - Site navigation structure
- `src/utils/blog.ts` - Blog post processing and pagination logic
- `vendor/integration/index.mjs` - Custom Astro integration for config management

## Content Workflow

### Adding Blog Posts
1. Create new `.md` or `.mdx` file in `/src/content/post/`
2. Include required frontmatter (title, publishDate, etc.)
3. Content is automatically processed and added to blog listings
4. Permalinks generated based on config pattern (`/%slug%`)

### Modifying Site Configuration
1. Edit `src/config.yaml` for site-wide settings
2. Update `src/navigation.js` for navigation changes
3. Changes automatically reload in development

### Component Development
- Follow existing patterns in `/src/components/widgets/`
- Use TypeScript for props and utilities
- Leverage Astro's component composition patterns
- Import styles and utilities from the design system