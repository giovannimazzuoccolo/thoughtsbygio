---
title: 'How to Install Official Lighthouse CI in GitHub Actions'
description: 'Learn how to set up Google's official Lighthouse CI in your GitHub Actions workflow to automatically test your website performance, accessibility, and SEO.'
pubDate: 'Oct 22 2024'
heroImage: '/blog-placeholder-3.jpg'
---

Performance monitoring is crucial for any website, and Google's Lighthouse is the gold standard for measuring web performance, accessibility, best practices, and SEO. In this guide, I'll show you how to integrate the official Lighthouse CI directly into your GitHub Actions workflow.

## Why Lighthouse CI?

Lighthouse CI allows you to:
- Automatically test your site on every deployment
- Track performance metrics over time
- Catch performance regressions before they reach production
- Ensure accessibility and SEO standards are maintained

## Setting Up the Workflow

First, create a new workflow file in your repository at `.github/workflows/lighthouse.yml`:

```yaml
name: Lighthouse CI

on:
  push:
    branches: [ main ]
  pull_request:
    branches: [ main ]

jobs:
  lighthouse:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-node@v4
        with:
          node-version: 18
      - run: npm ci
      - run: npm run build
      - name: Install Lighthouse CI
        run: npm install -g @lhci/cli@0.12.x
      - name: Run Lighthouse CI
        run: lhci autorun
        env:
          LHCI_GITHUB_APP_TOKEN: ${{ secrets.GITHUB_TOKEN }}
```

## Configuration File

Create a `lighthouserc.json` file in your project root to configure Lighthouse CI:

```json
{
  "ci": {
    "collect": {
      "staticDistDir": "./dist",
      "url": [
        "http://localhost/",
        "http://localhost/blog/"
      ]
    },
    "assert": {
      "assertions": {
        "categories:performance": ["warn", {"minScore": 0.9}],
        "categories:accessibility": ["error", {"minScore": 0.9}],
        "categories:best-practices": ["warn", {"minScore": 0.9}],
        "categories:seo": ["warn", {"minScore": 0.9}]
      }
    },
    "upload": {
      "target": "temporary-public-storage"
    }
  }
}
```

## Key Configuration Options

- **staticDistDir**: Points to your built site directory
- **url**: Array of URLs to test (relative to your site root)
- **assertions**: Set minimum score thresholds for each category
- **upload**: Where to store the detailed reports

## What Happens Next

Once set up, Lighthouse CI will:

1. **Build your site** using your existing build process
2. **Start a local server** to serve your static files
3. **Run Lighthouse audits** on specified URLs
4. **Check assertions** against your defined thresholds
5. **Upload reports** to temporary public storage
6. **Comment on PRs** with performance insights (if configured)

## Benefits of the Official Implementation

Using Google's official `@lhci/cli` directly instead of third-party actions gives you:

- **Latest features** as soon as they're released
- **Better reliability** with fewer dependencies
- **More control** over configuration and customization
- **Official support** from the Lighthouse team

## Viewing Results

After each run, you'll see:
- **Pass/fail status** in your GitHub Actions summary
- **Detailed reports** via the uploaded artifacts
- **Performance metrics** for each audited page
- **Specific recommendations** for improvements

## Conclusion

Integrating Lighthouse CI into your workflow ensures your site maintains high performance and accessibility standards. The official implementation provides the most reliable and up-to-date experience, helping you catch issues before they impact your users.

Start monitoring your site's performance today and never ship a slow website again!
