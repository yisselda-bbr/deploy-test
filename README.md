# Deploy Branch Selector Demo

A succinct, clear, and precise demonstration of best deployment UX for dev/test environments. Deploy any feature branch straight to dev, before opening a PR, using the GitHub Actions "Use workflow from" dropdown—branch autocomplete built-in!

## Why This Matters
This repo is crafted by a senior staff lead software engineer & solutions architect, with a passion for UX and a pedagogical bias rooted in the neuroscience of deep learning (inspired by Barbara Oakley, Terrence Sejnowski, Alistair McConville). The workflow maximizes learnability, minimizes cognitive friction, and fits iterative shipping.

## Quick Demo
1. Push this repo to GitHub.
2. Create a feature branch:  
   `git checkout -b feature/my-new-feature && git push origin feature/my-new-feature`
3. From the Actions tab, manually trigger the deploy workflow.
4. Select any branch using the branch dropdown (with autocomplete) and hit "Run workflow."
5. Confirm the workflow operates on the selected branch (see output).

## Implementation
- No free-text branch input!
- Uses GitHub's built-in branch picker for branch selection (via `workflow_dispatch` default UI)
- The workflow reads `github.ref` to deploy the selected branch, making the process precise and foolproof.

## Key Workflow Example
```yaml
on:
  workflow_dispatch:
    # No inputs - use "Use workflow from" dropdown
jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/github-script@v7
        with:
          script: |
            const ref = context.ref.replace('refs/heads/', '');
            // ref = the branch picked in "Use workflow from"
```

## Designed for Teaching & Speed
This example is optimized to help you, your team, or your students ship, test, and learn faster—with fewer mistakes.
