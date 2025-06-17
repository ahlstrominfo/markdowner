# Markdowner ⚡ Wrangler v4 Edition

A modernized fork of [Markdowner](https://github.com/dhravya/markdowner) by [Dhravya Shah](https://github.com/dhravya) - updated for Wrangler v4 and latest Cloudflare Workers patterns.

**🚀 What's New in This Fork:**
- ✅ Updated to Wrangler v4 with latest features  
- ✅ Modern JSON configuration format
- ✅ Strict TypeScript with zero compilation errors
- ✅ Enhanced development safety with separate KV namespaces
- ✅ Latest dependency versions and security updates
- ✅ Comprehensive developer documentation

## 📝 About

A fast tool to convert any website into LLM-ready markdown data, now modernized for the latest Cloudflare Workers ecosystem.

Perfect for AI applications where structured markdown data improves LLM response quality significantly compared to raw HTML.

## Features 🚀

- Convert any website into markdown
- LLM Filtering with AI Workers
- Detailed markdown mode
- Auto Crawler (without sitemap!)
- Text and JSON responses
- Easy to self-host on Cloudflare
- Modern development experience with Wrangler v4
- Type-safe development with strict TypeScript

## Usage

To use the API, make a GET request with a URL parameter:

```bash
curl 'https://your-markdowner.your-subdomain.workers.dev/?url=https://example.com'
```

### Required Parameters

- `url` (string) → The website URL to convert into markdown

### Optional Parameters

- `enableDetailedResponse` (boolean: false) → Include full HTML content instead of just article content
- `crawlSubpages` (boolean: false) → Crawl and return markdown for up to 10 subpages
- `llmFilter` (boolean: false) → Filter out unnecessary information using LLM

### Response Types

- Add `Content-Type: text/plain` in headers for plain text response
- Add `Content-Type: application/json` in headers for JSON response

## Tech Stack

This modernized version uses:

- **Cloudflare Workers** with Wrangler v4
- **Browser Rendering API** for web scraping
- **Durable Objects** for stateful browser management  
- **KV Storage** for caching with separate dev/prod namespaces
- **AI Workers** for content filtering
- **TypeScript** with strict type checking
- **Modern ES2022** syntax and patterns

## Self Hosting

You can easily self-host this modernized version. You'll need the [Workers paid plan](https://developers.cloudflare.com/workers-ai/platform/pricing/) for Browser Rendering and Durable Objects.

### Prerequisites

- Node.js 18+
- Cloudflare account with Workers paid plan
- Git

### Setup

1. **Clone this modernized fork:**
   ```bash
   git clone https://github.com/ahlstrominfo/markdowner
   cd markdowner
   ```

2. **Install dependencies:**
   ```bash
   npm install
   ```

3. **Create KV namespaces:**
   ```bash
   npm run kv:create
   npx wrangler kv namespace create md_cache --preview
   ```

4. **Update wrangler.json with your KV namespace IDs**

5. **Deploy:**
   ```bash
   npm run deploy
   ```

### Development

For local development with the modern setup:

```bash
# Start development server
npm run dev

# Type checking
npm run lint

# View logs
npm run logs

# Generate types
npm run types
```

## Architecture

The modernized architecture includes:

- **Main Worker**: Modern export with proper TypeScript typing
- **Browser Durable Object**: Manages browser instances with enhanced error handling
- **Caching Layer**: KV storage with separate development and production namespaces
- **Rate Limiting**: API protection with configurable limits
- **AI Integration**: Optional LLM filtering for content cleanup

## Credits & License

This is a modernized fork of the excellent [Markdowner](https://github.com/dhravya/markdowner) originally created by [Dhravya Shah](https://github.com/dhravya).

**Original Creator:** [Dhravya Shah](https://dhr.wtf)  
**Modernization:** Updated for Wrangler v4 and latest Cloudflare Workers patterns

Both the original and this fork are licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Support

- 🐛 **Issues**: Report bugs or request features in the [Issues](https://github.com/ahlstrominfo/markdowner/issues) section
- 💡 **Original Project**: Check out the [original Markdowner](https://github.com/dhravya/markdowner) by Dhravya Shah
- 📚 **Documentation**: See [CLAUDE.md](CLAUDE.md) for development guidance

---

⭐ **Star this repo** if the Wrangler v4 modernization helped you!