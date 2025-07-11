# Copilot Instructions for brian.dev 

## Project Overview
This is "brian.dev" - an Astro-powered blog template for Brian Ketelsen. It's built for performance with Tailwind CSS v4, TypeScript, and MDX support.

## Architecture & Key Patterns

### Content-First Structure
- **Blog content**: Lives in `src/content/blog/` as `.md/.mdx` files with strict frontmatter schema
- **Projects content**: Lives in `src/content/projects/` as `.md/.mdx` files with name, description, url, icon
- **Content collections**: Defined in `src/content.config.ts` using Astro's new glob loader
- **Required article frontmatter**: `title`, `description`, `pubDate`, optional `heroImage`, `updatedDate`, `featured`
- **Required projects frontmatter**: `name`, `description`, `url`, `icon` (Heroicons name)
- **Featured posts**: Use `featured: true` in frontmatter to appear on homepage

### Layout Hierarchy
- `BaseLayout.astro`: Root layout with dark/light theme, responsive container, header/footer
- `ArticleLayout.astro`: Extends BaseLayout for blog posts with typography styles
- All pages use this consistent container pattern: `mx-auto w-full max-w-7xl lg:px-8`

### Component Organization
- **Articles**: `src/components/articles/` - FeaturedArticles.astro, ArticleCard.astro
- **Core**: Root components for Header, Footer, Image handling, LightDarkToggle
- **Nested structure**: Group related components in subdirectories

### Styling Conventions
- **Tailwind CSS v4**: Uses new `@theme` syntax in `src/styles/global.css`
- **Custom properties**: Rose color palette as `--color-primary-*` 
- **Typography**: Space Grotesk for headings (`--font-headings`), Roboto for body (`--font-sans`)
- **Dark mode**: Uses `dark:` variants with localStorage persistence
- **Responsive images**: Light/dark variants using Astro's `<Image>` component

### File Routing Patterns
- **Dynamic routes**: `[...slug].astro` for articles, `[...page].astro` for pagination
- **Static generation**: All article routes pre-generated via `getStaticPaths()`
- **Content rendering**: Use `await render(post)` to get `<Content />` component

## Development Workflows

### Local Development
```bash
npm run dev          # Start dev server
npm run build        # Production build
npm run preview      # Preview production build
```

### Adding Content
1. **Articles**: Create `.md/.mdx` file in `src/content/blog/`
2. **Projects**: Create `.md/.mdx` file in `src/content/projects/`
3. Include required frontmatter fields for each content type
4. Use `featured: true` for articles to show on homepage
5. Place hero images in `src/images/` and reference relatively

### Theme Customization
- Modify color palette in `src/styles/global.css` `@theme` block
- Update fonts by changing `--font-headings` and `--font-sans` 
- Site metadata in `src/consts.ts` (SITE_TITLE, SITE_DESCRIPTION)

## Project-Specific Conventions

### Image Handling
- Uses Astro's optimized `<Image>` component throughout
- Development mode disables optimization for StackBlitz compatibility
- Light/dark image variants: `heroImageLight` and `heroImageDark` pattern

### Content Schema
- Dates auto-coerced with `z.coerce.date()` in content config
- Optional fields use `.optional()` pattern
- Image validation through Astro's `image()` helper

### Icon Usage
- `astro-icon` with Heroicons collection (`@iconify-json/heroicons`)
- Usage: `<Icon name="heroicons:moon-solid" class="..." />`



When contributing, maintain the existing architectural patterns and the playful theme while ensuring accessibility and performance standards.
