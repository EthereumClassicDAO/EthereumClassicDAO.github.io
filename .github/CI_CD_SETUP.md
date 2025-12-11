# CI/CD Pipeline Setup

This repository includes automated CI/CD pipelines for building and previewing pull requests.

## Workflows

### 1. CI Workflow (`ci.yml`)
Runs on every pull request and push to main/master branches.

**Checks performed:**
- ✅ Validates all required HTML files exist
- ✅ Validates HTML5 syntax
- ✅ Checks for broken links
- ✅ Verifies asset directory structure

### 2. PR Preview Workflow (`pr-preview.yml`)
Automatically deploys preview deployments for pull requests using Netlify.

**Features:**
- 🚀 Automatic preview deployment on PR open/update
- 💬 Comments on PR with preview URL
- 🗑️ Cleanup when PR is closed

## Setup Instructions

### Prerequisites
To enable PR preview deployments, you need to configure Netlify:

1. **Create a Netlify account** at https://netlify.com
2. **Create a new site** (you can use a manual deploy initially)
3. **Get your credentials:**
   - Go to User Settings → Applications → Personal Access Tokens
   - Create a new access token (this is your `NETLIFY_AUTH_TOKEN`)
   - Go to your site's Settings → General → Site details
   - Copy your Site ID (this is your `NETLIFY_SITE_ID`)

### Adding Secrets to GitHub

1. Go to your repository on GitHub
2. Navigate to Settings → Secrets and variables → Actions
3. Click "New repository secret"
4. Add the following secrets:
   - **Name:** `NETLIFY_AUTH_TOKEN`
     **Value:** Your Netlify personal access token
   - **Name:** `NETLIFY_SITE_ID`
     **Value:** Your Netlify site ID

### How It Works

Once configured, the workflow will automatically:
1. Run validation checks on every PR
2. Deploy a preview to Netlify when a PR is opened or updated
3. Post a comment on the PR with the preview URL
4. Clean up the preview when the PR is closed

## Alternative: Without Netlify

If you prefer not to use Netlify, you can:
- Remove the "Deploy to Netlify" step from `pr-preview.yml`
- Use GitHub Pages with branch deployments
- Use other services like Vercel, Cloudflare Pages, or Surge.sh

## Local Testing

To test your changes locally before pushing:

```bash
# Simply open the HTML files in your browser
open index.html

# Or use a simple HTTP server
python3 -m http.server 8000
# Then visit http://localhost:8000
```

## Troubleshooting

**Preview deployment not working?**
- Check that the secrets are properly configured in repository settings
- Verify that the workflow has the correct permissions
- Check the Actions tab for detailed error logs

**Validation failing?**
- Review the HTML5 validator output in the CI workflow logs
- Fix any syntax errors in the HTML files
- Ensure all required files are present
