# SEO Indexability Review - n8n Workflow

> **Automated SEO indexability review workflow using n8n, Firecrawl, Claude AI, and SMTP**

This n8n workflow provides comprehensive SEO indexability analysis for websites. It automatically crawls sitemaps, analyzes page indexability factors, and emails detailed audit reports with recommendations.

## Quick Start

**Download Complete Workflow**: [SEO Indexability Review - Complete JSON](https://gist.githubusercontent.com/deepthinklabs-ai/959f79aa4b37623070753d0cc6126b7f/raw/seo-indexability-review-complete.json)

1. Right-click and save the JSON file
2. Import into n8n via Workflows → Import from File
3. Configure credentials (see [INSTALL.md](INSTALL.md))
4. Update website URL and email settings
5. Execute workflow

## Features

- **Automated Sitemap Crawling**: Fetches and parses XML sitemaps
- **Comprehensive Page Analysis**: Checks HTTP status, content-type, robots tags, canonicals, and more
- **AI-Powered SEO Audit**: Uses Claude AI to analyze indexability factors and provide recommendations with up to date standards
- **Dual Crawling Strategy**: Raw HTTP requests + JavaScript rendering via Firecrawl
- **Detailed Reporting**: Generates prioritized recommendations with P0/P1/P2 classification
- **Email Notifications**: Sends a formatted HTML report via email for each page analyzed

## What It Analyzes

### Core Indexability Factors
- HTTP status codes and redirects
- Content-Type validation (HTML detection)
- Robots meta tags and X-Robots-Tag headers
- Canonical URL implementation
- Page type classification (login, cart, search pages, etc.)

### Technical SEO Elements
- Cache control headers
- Security headers (HSTS, CSP, X-Frame-Options)
- Content encoding and compression
- Server response characteristics
- Redirect chains and location headers

### AI Analysis Includes
- **Scoring System**: 0-100 indexability score
- **Priority Classification**: P0 (Critical), P1 (High), P2 (Medium/Low) fixes
- **Page Type Detection**: Identifies problematic page types
- **Canonical Conflicts**: Detects multiple or conflicting canonical URLs
- **Actionable Recommendations**: Specific steps to resolve issues

## Setup Requirements

### n8n Nodes Required
- **HTTP Request** - For fetching pages and sitemaps
- **Code** - For parsing XML and data transformation
- **Split in Batches** - For processing multiple URLs
- **Wait** - For rate limiting
- **If/Switch** - For conditional logic
- **Set** - For data manipulation
- **Merge** - For combining data streams
- **Email Send** - For report delivery
- **AI Agent** - For analysing raw JSON results and identifying areas to improve
- **Anthropic Chat Model** - For compiling the HTML report to be emailed

### External Services
1. **Firecrawl API** - For JavaScript rendering and metadata extraction
2. **Anthropic API** - For AI-powered SEO analysis
3. **SMTP Server** - For email notifications

### Credentials Needed
- Firecrawl API key
- Anthropic API key  
- SMTP credentials for email sending

## Installation

See [INSTALL.md](INSTALL.md) for detailed setup instructions.

## Security Review

**The workflow is safe to share publicly:**
- No API keys or tokens are exposed
- Email addresses are templated as placeholders
- Website URLs use placeholder values
- Credential references use IDs, not actual keys
- All sensitive data must be configured after import

## Usage

### Basic Execution
1. Open the workflow in n8n
2. Set Firecrawl Credentials in Render Page (SPA) node
3. Set Anthropic Credentials in Anthropic Chat Model connected to Indexability Review Agent node
4. Set Anthropic Credentials in Report Writer - Indexability node
5. Set SMTP Credentials in Send email node
6. In the"Init Site" node, replace "INSERT_WEBSITE_URL_TO_REVIEW" with the website you want to review
7. In the Send email node, replace the placeholders for To and From fields with actual email addresses.
8. Click "Execute workflow" to start the analysis
9. The workflow will automatically:
   - Fetch the sitemap
   - Analyze each URL for indexability
   - Generate AI-powered recommendations
   - Send a detailed report via email

### Customization Options

#### Target Different Websites
```javascript
// In the "Init Site" node, modify:
{
  "site": "https://your-website.com"
}
```

#### Adjust Analysis Scope
The workflow processes all URLs found in the sitemap. To limit scope:
- Modify the sitemap parsing logic
- Add URL filtering in the expansion phase
- Implement batch size limits

#### Customize AI Analysis
The Claude AI agent uses a detailed system prompt that can be modified for:
- Different scoring criteria
- Custom page type detection
- Industry-specific SEO rules
- Additional technical factors

## Output Format

### Email Report Includes
- **Page URL**: The analyzed URL
- **Indexability Score**: 0-100 rating
- **Verdict**: indexable/non-indexable/conditionally-indexable
- **Key Findings**: Categorized by severity (high/medium/low)
- **Priority Fixes**: Actionable recommendations with P0/P1/P2 classification
- **Technical Details**: HTTP status, content-type, security headers

### Sample Analysis Output
```json
{
  "page_url": "https://example.com/page",
  "score": 85,
  "verdict": "indexable",
  "page_type": "standard",
  "findings": [
    {
      "severity": "medium",
      "detail": "Missing canonical URL"
    }
  ],
  "recommendations": [
    {
      "priority": "P1",
      "action": "Add canonical URL",
      "rationale": "Prevents duplicate content issues"
    }
  ]
}
```

## Performance Considerations

- **Batch Processing**: URLs are processed in batches to manage load
- **Rate Limiting**: Built-in delays prevent overwhelming target servers
- **Error Handling**: Continues processing even if individual URLs fail
- **Dual Strategy**: Falls back from HEAD to GET requests when needed

## Contributing

Contributions are welcome! Areas for improvement:
- Additional SEO factors
- Enhanced page type detection
- Custom reporting formats
- Integration with SEO tools
- Performance optimizations

## License

This project is open source and available under the MIT License.

## Related Links

- [n8n Documentation](https://docs.n8n.io/)
- [Firecrawl API](https://firecrawl.dev/)
- [Anthropic Claude](https://www.anthropic.com/)
- [Google Search Essentials](https://developers.google.com/search/docs/essentials)

## Support

For questions or issues:
- Open a GitHub issue
- Email: dave@deepthinklabs.ai
- n8n Workflow URL: https://deepthinklabs.app.n8n.cloud/workflow/4K11kIFyqo0Gxp6Y

---

**Built by [DeepThinkLabs.ai](https://deepthinklabs.ai) - AI-powered automation solutions**
