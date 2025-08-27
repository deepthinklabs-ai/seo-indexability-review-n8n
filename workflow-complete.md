# SEO Indexability Review - Complete Workflow Export

This is the complete n8n workflow export from the original workflow. Import this file directly into n8n.

**Note**: You'll need to update credentials and configuration after importing.

## What's Included

- 24 nodes including manual trigger, HTTP requests, code execution, AI analysis, and email reporting
- Complete connection logic and data flow
- AI prompts for indexability analysis and report generation
- Email template with HTML formatting
- Error handling and fallback mechanisms

## Import Instructions

1. Download this file
2. In n8n: Workflows → Import from File
3. Configure credentials (see INSTALL.md)
4. Update website URL in "Init Site" node
5. Test execution

The workflow includes sophisticated logic for:
- Sitemap parsing and URL extraction
- Dual crawling strategy (HEAD + GET requests)
- JavaScript rendering via Firecrawl
- AI-powered SEO analysis with Claude
- Structured report generation
- HTML email delivery

For detailed setup instructions, see [INSTALL.md](INSTALL.md).
