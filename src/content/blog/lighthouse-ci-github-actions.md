---
title: "How to Install Official Lighthouse CI in GitHub Actions"
description: "Learn how to set up Google's official Lighthouse CI in your GitHub Actions workflow to automatically test your website performance, accessibility, and SEO."
pubDate: "Oct 22 2024"
heroImage: "../../assets/lighthouse-ci-hero.jpg"
---

Google Lighthouse is one of the most popular tools for auditing web performance, accessibility, and SEO. It is convenient to have it integrated into your CI/CD pipeline to get informed about performance regressions without running the tool manually.

Lighthouse is not the holy grail. Reaching a 100% score, especially on performance and SEO, will not guarantee a lot of traffic or conversions. Other factors, like accessibility and best practices, are more important to ensure a good user experience. SEO is a complex topic that requires more than a 100% score on Google Lighthouse.

Having it installed gives a good indication of what you should optimize on your website for every deployment.

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


As you can see, we are using the official `@lhci/cli` package from Google, not a user-created GitHub Action. My colleague, who is a DevOps specialist, discouraged using third-party actions when possible, as they can be outdated or even dangerous.

The YAML file is quite simple: it pulls the code, sets up Node.js, builds the project, installs Lighthouse CI, and runs it. The environment variable `LHCI_GITHUB_APP_TOKEN` is required to allow Lighthouse CI to comment on pull requests presenting the results.


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

Most likely you'll want to adjust the scores to fit your project needs. As I mentioned, reaching 100% in all categories wouldn't necessarily be beneficial for your project.

If you want another tool to check accessibility in your pipeline, you can install [pa11y](https://github.com/pa11y/pa11y), an open-source accessibility testing tool.
