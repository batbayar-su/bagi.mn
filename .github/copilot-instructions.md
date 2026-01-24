# Copilot Instructions for bagi.mn

## Project Overview
This is a **Hugo static site** using the **Blowfish theme**. The site is multilingual (English and Mongolian) and hosted at https://bagi.mn/.

## Technology Stack
- **Static Site Generator**: Hugo
- **Theme**: Blowfish (located in `themes/blowfish/`)
- **Languages**: English (default), Mongolian
- **Styling**: Custom CSS in `assets/css/custom.css`
- **Base URL**: https://bagi.mn/

## Project Structure

### Key Directories
- **`content/`**: All site content (markdown files for posts, pages, etc.)
  - Organize by language code subdirectories if needed
  - Use front matter for metadata (title, date, tags, categories, authors, etc.)
- **`config/_default/`**: Configuration files
  - `hugo.toml`: Main Hugo configuration
  - `languages.en.toml` & `languages.mn.toml`: Language-specific settings
  - `params.toml`: Blowfish theme parameters
  - `menus.en.toml`: English menu configuration
  - `markup.toml`: Markdown rendering settings
  - `module.toml`: Hugo modules configuration
- **`layouts/`**: Custom layout overrides (overrides theme templates)
  - `partials/`: Partial templates
- **`assets/`**: Source assets (CSS, JS, images) processed by Hugo
  - `css/custom.css`: Custom styles
  - `img/`: Source images
- **`static/`**: Static files served as-is (not processed)
- **`themes/blowfish/`**: The Blowfish theme (do not modify directly)
- **`public/`**: Generated site output (do not edit, regenerated on build)
- **`resources/_gen/`**: Generated resources cache

## Content Creation Guidelines

### Creating New Content
Use Hugo archetypes to create new content with proper front matter:
```bash
hugo new content/posts/my-new-post.md
```

### Front Matter Structure
```yaml
---
title: "Post Title"
date: 2026-01-23T12:00:00+00:00
draft: false
description: "Short description for SEO"
tags: ["tag1", "tag2"]
categories: ["category1"]
authors: ["author-name"]
---
```

### Multilingual Content
- Default language: English (en)
- Secondary language: Mongolian (mn)
- Language-specific content should follow Hugo's multilingual conventions
- Check `languages.*.toml` files for language-specific configurations

## Theme Customization

### Blowfish Theme Parameters
- Theme configuration is in `config/_default/params.toml`
- Color scheme: "github" with dark mode default
- Features enabled: search, code copy, auto appearance switching
- Header layout: "basic"
- Reference: https://blowfish.page/docs/

### Customizing Styles
- Add custom CSS to `assets/css/custom.css`
- **Do not modify** theme files in `themes/blowfish/` directly
- Override theme templates by copying to `layouts/` directory

### Overriding Theme Templates
To customize a theme template:
1. Copy the template from `themes/blowfish/layouts/` to `layouts/`
2. Maintain the same directory structure
3. Modify the copied file in `layouts/`

## Development Workflow

### Local Development
```bash
# Start Hugo development server with drafts
hugo server -D

# Start server for specific language
hugo server --buildDrafts --buildFuture

# Start with custom port
hugo server -p 1314
```

### Building the Site
```bash
# Build for production
hugo

# Build with specific environment
hugo --environment production

# Clean public directory and rebuild
rm -rf public/ && hugo
```

### Testing
- Preview site at http://localhost:1313/
- Test both languages (en and mn)
- Verify responsive design
- Check dark/light mode switching

## Configuration Management

### Hugo Configuration (`hugo.toml`)
- Base URL: https://bagi.mn/
- Default content language: en
- Theme: blowfish
- Enable robots.txt
- Enable emoji support
- Pagination: 100 items per page

### Theme Parameters (`params.toml`)
- Color scheme: github
- Default appearance: dark
- Auto-switch appearance: enabled
- Search: enabled
- Code copy: enabled

### Taxonomies
- Tags: `tags`
- Categories: `categories`
- Authors: `authors`

## Common Tasks

### Adding a New Blog Post
1. Create content: `hugo new content/posts/post-name.md`
2. Edit front matter (title, date, tags, categories)
3. Write content in Markdown
4. Set `draft: false` when ready to publish
5. Build and deploy

### Adding Custom CSS
1. Open `assets/css/custom.css`
2. Add your styles
3. Hugo will automatically process and bundle CSS

### Updating Menus
- Edit `config/_default/menus.en.toml` for English menu
- Create `menus.mn.toml` for Mongolian menu if needed
- Follow Blowfish menu structure conventions

### Managing Theme Updates
```bash
git submodule update --remote --recursive
```

## Important Notes

### Do Not Edit
- **`public/`**: Regenerated on every build
- **`resources/_gen/`**: Auto-generated cache
- **`themes/blowfish/`**: Theme source (customize via overrides)

### Always Check
- Front matter is valid YAML/TOML
- Markdown syntax is correct
- Images are optimized and in correct directories
- Links use Hugo's relref/ref for internal links
- Multilingual content has proper language codes

### Blowfish-Specific Features
- Refer to https://blowfish.page/docs/ for:
  - Shortcodes available
  - Page layouts and types
  - Front matter options
  - Icon usage
  - Advanced features (search, analytics, comments, etc.)

## Helpful Commands

```bash
# Check Hugo version
hugo version

# List all content
hugo list all

# Check for draft posts
hugo list drafts

# Validate configuration
hugo config

# Clean cache and generated resources
hugo mod clean
```

## Best Practices
1. **Always test locally** before deploying
2. **Use descriptive commit messages** for content changes
3. **Optimize images** before adding to `assets/` or `static/`
4. **Keep theme updated** regularly for security and features
5. **Use Hugo shortcodes** for complex content elements
6. **Follow Blowfish conventions** for maximum compatibility
7. **Backup configuration** before major changes
8. **Test multilingual** features if adding/editing translations