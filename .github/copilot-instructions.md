# Copilot Instructions for Thoughts by Gio

This is an Astro blog project using the official blog starter template, customized for personal thoughts and insights.

## Architecture Overview

- **Static Site Generator**: Astro v5 with TypeScript strict mode
- **Content Management**: Astro Content Collections with MDX support
- **Blog Structure**: File-based routing with frontmatter-driven metadata
- **Styling**: Scoped CSS in .astro components, global styles in `src/styles/global.css`

## Key Patterns

### Content Schema
Blog posts use a strict schema defined in `src/content.config.ts`:
```typescript
schema: ({ image }) => z.object({
  title: z.string(),
  description: z.string(),
  pubDate: z.coerce.date(),
  updatedDate: z.coerce.date().optional(),
  heroImage: image().optional(),
})
```

### Component Structure
- `BaseHead.astro`: Centralized SEO, meta tags, and Google Fonts (Crimson Text + Source Sans 3)
- `BlogPost.astro`: Layout with 65ch max-width, responsive design, and hero image support
- Components import global CSS via BaseHead for consistent styling

### Content Flow
1. Blog posts in `src/content/blog/` (Markdown/MDX)
2. Collection queried via `getCollection('blog')` and sorted by pubDate
3. Rendered through `BlogPost.astro` layout with typed props
4. File-based routing via `[...slug].astro` dynamic route

### Asset Management
- Static assets in `public/` directory
- Blog images imported from `src/assets/` using Astro's Image component
- Optimized images with width/height attributes (e.g., 1020x510 for hero images)

## Development Workflow

### Commands
- `npm run dev`: Development server on localhost:4321
- `npm run build`: Production build to `./dist/`
- `npm run preview`: Preview production build locally

### Site Configuration
- Site URL configured in `astro.config.mjs` (currently example.com)
- RSS feed and sitemap generation enabled
- MDX integration for enhanced Markdown

### Content Creation
- Add new posts to `src/content/blog/` with required frontmatter
- Images should be placed in `src/assets/` and imported properly
- Use FormattedDate component for consistent date formatting

## Customization Points

- Site branding: Update `SITE_TITLE` and `SITE_DESCRIPTION` in `src/consts.ts`
- Styling: Modify CSS custom properties in `src/styles/global.css`
- Layout: Adjust responsive breakpoints and max-width (65ch) in BlogPost.astro
- Typography: Google Fonts loaded in BaseHead.astro (Crimson Text + Source Sans 3)

## Integration Details

- **RSS**: Auto-generated at `/rss.xml` using @astrojs/rss
- **Sitemap**: Auto-generated using @astrojs/sitemap
- **SEO**: Comprehensive meta tags, Open Graph, and canonical URLs in BaseHead
- **Sharp**: Image optimization for Astro's Image component