# GCP Projects Overview

**Category:** projects
**Tags:** gcp, firebase, deployment, infrastructure
**Source:** Claude_Max
**Created:** 2025-02-03
**Confidence:** high

## Summary

Overview of GCP/Firebase projects and their deployment configuration.

## Projects

| Project ID | Purpose | Services |
|------------|---------|----------|
| `glassy-polymer-477908-g9` | Main project (StateOS, ChatBot) | Cloud Run, Firebase Hosting |
| `legimental-prod` | Legislative compliance | Cloud Run, Firebase |
| `phoenix-analytics-44917` | Electoral analytics | Cloud Run, Firebase |

## Authentication Status

| Service | Auth Method | Deploy Command |
|---------|-------------|----------------|
| GCP/Cloud Run | `gcloud auth login` | `gcloud run deploy ...` |
| Firebase | `firebase login` | `firebase deploy` |

## Live Deployments

### ChatBot (vladnirealita.cz)
- **URL:** https://www.vladnirealita.cz/
- **Project:** glassy-polymer-477908-g9
- **Type:** Firebase Hosting + Cloud Run backend
- **Features:**
  - Guardrails (odpovídá jen na politiku/vládu)
  - Viditelný text v inputu

## Deployment Commands

### Cloud Run (Backend)

```bash
# Quick deploy from source
gcloud run deploy SERVICE_NAME \
  --source . \
  --region europe-west1 \
  --project glassy-polymer-477908-g9 \
  --allow-unauthenticated

# With env vars
gcloud run deploy SERVICE_NAME \
  --source . \
  --region europe-west1 \
  --set-env-vars="KEY=value" \
  --allow-unauthenticated
```

### Firebase Hosting (Frontend)

```bash
# Build first (Next.js)
npm run build

# Deploy
firebase deploy --only hosting --project PROJECT_ID
```

### Full Stack Deploy

```bash
# 1. Backend
cd backend
gcloud run deploy backend --source . --region europe-west1

# 2. Frontend
cd ../frontend
npm run build
firebase deploy --only hosting
```

## Hard Refresh After Deploy

Inform users to clear cache:
- **Chrome/Edge:** Ctrl+Shift+R
- **Firefox:** Ctrl+F5
- **Safari:** Cmd+Shift+R

## Related

- [GCP Service Account Auth](../technologies/gcp-service-account-auth.md)
- [GCP Skill](../../Claude_Max/.claude/skills/gcp/SKILL.md)
