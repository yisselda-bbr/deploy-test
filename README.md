# Deploy Branch Selector Demo

A quick demo repo: deploy any feature branch to dev using GitHub Actions' built-in branch dropdown.

## How It Works
- No inputs—just use the "Use workflow from" dropdown for branch selection.
- Workflow deploys the selected branch.

## Test It
1. Create a branch:  
   `git checkout -b feature/my-new-feature && git push origin feature/my-new-feature`
2. In Actions → Deploy to Development → Run workflow, pick a branch from the dropdown.

## Key Snippet
```yaml
on:
  workflow_dispatch:
jobs:
  deploy:
    steps:
      - uses: actions/github-script@v7
        with:
          script: |
            const ref = context.ref.replace('refs/heads/', '');
```