# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Techtribes is a Jekyll-based static site that lists active tech communities and meetups in Finland. The site automatically scrapes community event data from various platforms and displays them. Only communities with events in the past year are included.

## Key Architecture

- **Jekyll Static Site**: Located in `site/` directory with standard Jekyll structure (`_layouts`, `_includes`, `_data`)
- **TypeScript Scrapers**: Located in `src/scrapers/` for different platforms (Meetup, Meetabit, Luma, JSON)
- **Data Pipeline**:
  - Communities defined in `data/communities.yml`
  - Scrapers fetch event data and output to `site/_data/output.yml`
  - Jekyll builds the static site using this data
- **CSS Processing**: Uses Tabler CSS framework with PurgeCSS optimization

## Development Commands

### Prerequisites

```bash
bundle install
npm install
```

### Core Development Workflow

```bash
npm run scrape          # Scrape event data from all communities
npm start               # Start Jekyll dev server with live reload
npm run build           # Build static site for production
```

### CSS Development

```bash
npm run css             # Process CSS
npm run purgecss        # Optimize CSS by removing unused styles
```

### Data Management

```bash
npm run sort            # Sort communities.yml alphabetically by name
npm run images          # Process community logos
```

## Scraper Architecture

The scraping system (`src/scrape.ts`) supports multiple event platforms:

- **Meetup.com**: `src/scrapers/meetup.ts`
- **Meetabit.com**: `src/scrapers/meetabit.ts`
- **Luma.ma**: `src/scrapers/luma.ts`
- **JSON endpoints**: `src/scrapers/json.ts`

Each scraper extracts:

- Event date and link
- Community member count
- Filters out inactive communities (no events in past year)

## Data Structure

Communities in `data/communities.yml` require:

- `name`: Community name
- `location`: "City, Country" format
- `tags`: Array of technology tags
- `events`: URL to event platform
- `site`: (optional) Community homepage
- `logo`: Logo filename in `site/assets/logos/` or URL

## File Organization

- `data/communities.yml` - Master list of communities
- `site/` - Jekyll site source
- `src/` - TypeScript utilities and scrapers
- `site/assets/logos/` - Community logo images
- `site/_data/output.yml` - Generated event data for Jekyll

## Testing

The scrapers include test files (`.test.ts`) that should be run when modifying scraper logic.
