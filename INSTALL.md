# Installation Guide

This guide will help you set up the SEO Indexability Review workflow in your n8n instance.

## Prerequisites

1. **n8n Instance**: Self-hosted or cloud-hosted n8n installation
2. **API Keys**: Access to required external services
3. **SMTP Server**: For email notifications

## Step 1: Get API Keys

### Firecrawl API
1. Visit [Firecrawl.dev](https://firecrawl.dev/)
2. Sign up for an account or login
3. Go to **API Keys**
4. Create an API Key 
5. Save the API key for later use

### Anthropic Claude API
1. Visit [Anthropic Console](https://console.anthropic.com/)
2. Create an account or log in
3. Go to **API Keys** then **Create Key**
4. Save the API key for later use

### SMTP Credentials
Configure your email service (Gmail, Outlook, etc.):
- **Gmail**: Enable 2FA and create an App Password
- **SendGrid**: Create an API key
- **Other SMTP**: Get host, port, username, password

## Step 2: Import the Workflow

### Method 1: Direct Import
1. Download the workflow file:
   ```bash
   curl -O https://raw.githubusercontent.com/deepthinklabs-ai/seo-indexability-review-n8n/main/seo_indexability_review_n8n.json
   ```

2. In n8n:
   - Go to **Workflows** → **Import from File**
   - Select the downloaded JSON file
   - Click **Import**

### Method 2: Copy from n8n Template (coming soon)
1. In n8n, go to **Templates**
2. Search for "SEO Indexability Review"
3. Click **Use this workflow**

## Step 3: Configure Credentials in n8n

### Firecrawl Credentials
1. In n8n, go to **Overview** → **Click Down Arrow Next to Create Workflow** → **Create Credential**
2. Select **Firecrawl API**
3. Base URL **https://api.firecrawl.dev/v1** (should be pre-populated)
4. Enter your Firecrawl API key
5. Save as "Firecrawl account"

### Anthropic Credentials
1. In n8n, go to **Overview** → **Click Down Arrow Next to Create Workflow** → **Create Credential**
2. Select **Anthropic**
3. Enter your Claude API key
4. Base URL **https://api.anthropic.com** (should be pre-populated)
5. Save as "Anthropic account"

### SMTP Credentials
1. In n8n, go to **Overview** → **Click Down Arrow Next to Create Workflow** → **Create Credential**
2. Select **SMTP**
3. Configure your email settings:
   - **Host**: smtp.gmail.com (for Gmail)
   - **Port**: 465 (for Gmail - May be different depending on email provider)
   - **Username**: Your email address
   - **Password**: Your app password (you will need to setup an app password in Google Console for Gmail)
   - **Security**: STARTTLS
4. Save as "Email SMTP"

## Step 4: Update Workflow Configuration

### 1. Configure Target Website
In the **"Init Site"** node:
```javascript
{
  "site": "https://your-website.com"
}
```

### 2. Update Email Settings
In the **"Send email"** node:
- **From Email**: your-email@domain.com
- **To Email**: recipient@domain.com
- **Subject**: Customize as needed

### 3. Assign Credentials
Ensure each node has the correct credentials:
- **Firecrawl nodes** → "Firecrawl account"
- **Claude AI nodes** → "Anthropic account"
- **Email node** → "Email SMTP"

## Step 5: Test the Workflow

### Initial Test
1. Click **"Execute workflow"** button
2. Monitor execution in the workflow view
3. Check for any errors in node execution
4. Verify email delivery

### Troubleshooting Common Issues

#### Sitemap Not Found
- Ensure the website has a sitemap.xml
- Check the sitemap URL manually in a browser
- Verify robots.txt points to the correct sitemap

#### API Rate Limits
- Increase **Wait** node delays
- Reduce batch sizes in **Split in Batches** nodes
- Check API usage in your service dashboards

#### Email Delivery Issues
- Verify SMTP credentials are correct
- Check spam/junk folders
- Test SMTP settings with a simple email first

#### Node Execution Errors
- Check credential assignments
- Verify API keys are valid and have proper permissions
- Review node-specific error messages

## Step 6: Customize for Your Needs

### Adjust Analysis Scope
- Modify sitemap parsing to filter specific URLs
- Add URL pattern matching in the expansion logic
- Implement custom URL filtering rules

### Custom Reporting
- Modify the email template in the **Send email** node
- Add additional data points to the analysis
- Create custom scoring criteria in the Claude AI prompt

### Performance Optimization
- Adjust batch sizes based on your server capacity
- Optimize wait times between requests
- Implement error handling and retry logic

## Advanced Configuration

### Webhook Triggers
Convert to webhook-triggered execution:
1. Replace **Manual Trigger** with **Webhook** node
2. Configure webhook authentication
3. Set up scheduled execution via external service

### Database Storage
Store results in a database:
1. Add database nodes after the analysis
2. Create tables for storing SEO data
3. Implement historical tracking

### Multi-Site Analysis
Analyze multiple websites:
1. Modify **Init Site** to accept an array of websites
2. Add iteration logic for multiple sites
3. Enhance reporting for multi-site results

## Support

If you encounter issues:

1. **Check the Logs**: Review n8n execution logs for detailed errors
2. **Test Components**: Test individual nodes to isolate issues
3. **API Documentation**: Refer to Firecrawl and Anthropic API docs
4. **Community**: Ask questions in the n8n community forums
5. **GitHub Issues**: Report bugs or request features in this repository

## Next Steps

Once installed:
1. Run your first analysis
2. Review the generated report
3. Customize the workflow for your specific SEO needs
4. Set up scheduled execution for regular audits
5. Integrate with your existing SEO workflow

Happy analyzing! 🚀
