# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Markdowner is a modern Cloudflare Worker application that converts websites into LLM-ready markdown format. It uses Cloudflare's Browser Rendering API with Puppeteer to scrape web content and convert it to clean markdown using Mozilla's Readability library and Turndown.js.

## Architecture

### Core Components
- **Main Worker** (`src/index.ts`): Modern Worker export with proper TypeScript typing
- **Browser Durable Object** (`src/index.ts:Browser`): Manages browser instances and web scraping operations
- **Response Templates** (`src/response.ts`): Contains HTML template for the help/landing page

### Key Technologies
- Cloudflare Workers with modern ES2022 syntax and `satisfies ExportedHandler<Env>`
- Durable Objects for stateful browser management
- Puppeteer for browser automation
- KV storage for caching converted markdown
- AI Workers for optional LLM filtering
- Rate limiting for API protection

### Data Flow
1. Request comes in with URL parameter
2. Rate limiting check (unless authenticated with `BACKEND_SECURITY_TOKEN`)
3. Durable Object manages browser instance lifecycle
4. Browser navigates to URL and waits for `networkidle0`
5. Content extraction using Readability + Turndown conversion
6. Optional LLM filtering for content cleanup
7. Result cached in KV store with 1-hour TTL
8. Response returned as text or JSON based on Content-Type header

## Development Commands

```bash
# Local development with hot reload
npm run dev

# Deploy to production
npm run deploy

# Deploy to staging environment
npm run deploy:staging

# Generate TypeScript types for Cloudflare bindings
npm run types

# Type checking (no emit)
npm run lint

# View live logs
npm run logs

# Create KV namespace
npm run kv:create
```

## Modern Cloudflare Workers Features

### Updated Configuration
- Uses compatibility date `2024-06-17` with latest features
- Modern binding syntax in `wrangler.toml`
- Strict TypeScript configuration with ES2022 target
- Updated to latest Wrangler v3.103.0 and Workers Types

### Modern Code Patterns
- Proper `ExportedHandler<Env>` typing with `satisfies`
- ExecutionContext parameter in fetch handler
- Explicit return types (`Promise<Response>`, `Promise<void>`)
- Modern browser binding configuration
- Improved error handling and type safety

## API Parameters

### Required
- `url`: Website URL to convert to markdown

### Optional
- `enableDetailedResponse=true`: Include full HTML content instead of just article content
- `crawlSubpages=true`: Crawl up to 10 subpages (only available with JSON response)
- `llmFilter=true`: Use AI to filter out ads and irrelevant content

### Response Types
- `Content-Type: text/plain`: Returns raw markdown text
- `Content-Type: application/json`: Returns structured JSON with URL and markdown

## Special Handling

### Twitter/X URLs
- Direct API integration with Twitter syndication endpoint
- Bypasses browser rendering for tweets
- Extracts tweet content, metadata, and media information
- Results cached separately by tweet ID

### Browser Management
- Browsers kept alive for 60 seconds after last use
- Automatic cleanup and retry logic for failed browser instances
- Connection reuse for performance
- Modern null safety patterns

## Configuration Files

### Updated Bindings
- `BROWSER_DO`: Durable Object namespace for browser management
- `BROWSER`: Browser Rendering API binding
- `MD_CACHE`: KV namespace for caching
- `RATELIMITER`: Rate limiting binding
- `AI`: AI Workers binding

### Configuration Structure
- `wrangler.toml`: Modern Cloudflare Worker configuration with proper sectioning
- `worker-configuration.d.ts`: TypeScript interfaces for Cloudflare bindings
- `tsconfig.json`: Optimized TypeScript configuration for Workers with strict typing
- `package.json`: Updated scripts and latest dependency versions

## Environment Variables

Set in Cloudflare Workers dashboard:
- `BACKEND_SECURITY_TOKEN`: Bypass rate limiting for authenticated requests

All other bindings are configured in `wrangler.toml` and auto-generated in types.