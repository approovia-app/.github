# approovia-app

Org-wide defaults, workflow templates, and onboarding guides.

## Workflow templates

| Template | Purpose |
|---|---|
| **QA Queue Notifier** | Dispatches a `pr-merged` event to `qa-dashboard` whenever a PR merges to `development` or `main`. Every repo that ships code or documents should have this. |

Add a template to any repo: **Actions → New workflow → "By approovia-app"**.

## Required secrets

| Secret | Scope | Purpose |
|---|---|---|
| `QA_DISPATCH_TOKEN` | Per repo | Fine-grained PAT — **Actions: write** on `approovia-app/qa-dashboard` |

## Wiring up a new repo

Run the bootstrap workflow in `qa-dashboard`:

```
gh workflow run bootstrap-repo.yml \
  --repo approovia-app/qa-dashboard \
  -f repo=approovia-app/<new-repo>
```

This opens a PR in the target repo that adds `qa-notify.yml` and reminds you to set the secret.
