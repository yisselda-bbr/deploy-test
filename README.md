# Deploy Branch Selector Demo

A minimal repo to test GitHub Actions `workflow_dispatch` with branch autocomplete.

## The Goal

Get a branch dropdown with autocomplete when manually triggering deployments, instead of a free-text input field.

## How It Works

Instead of using `workflow_dispatch` inputs (which only support static choices or free text), we leverage the built-in **"Use workflow from"** dropdown that GitHub provides for all `workflow_dispatch` workflows.

The workflow reads `context.ref` to determine which branch was selected and deploys that.

## Testing

1. Push this repo to GitHub
2. Create a few test branches:
   ```bash
   git checkout -b feature/test-1
   git push origin feature/test-1
   
   git checkout -b feature/test-2  
   git push origin feature/test-2
   ```
3. Go to **Actions** → **Deploy to Development** → **Run workflow**
4. Click the **"Use workflow from"** dropdown - you'll see autocomplete!
5. Select a branch and click **Run workflow**
6. Check the workflow output to confirm it deployed the right branch

## Key Workflow Snippet

```yaml
on:
  workflow_dispatch:
    # No inputs - use "Use workflow from" dropdown instead

jobs:
  deploy:
    steps:
      - uses: actions/github-script@v7
        with:
          script: |
            const ref = context.ref.replace('refs/heads/', '');
            // ref now contains the branch selected in "Use workflow from"
```

## Applying to Your Real Workflow

Once confirmed working, update your production workflow's `resolve-ref` job to use `context.ref` for `workflow_dispatch` events instead of `context.payload.inputs.ref`.
