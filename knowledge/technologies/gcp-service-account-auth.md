# GCP Service Account Authentication

**Category:** technologies
**Tags:** gcp, firebase, authentication, service-account, deployment
**Source:** Claude_Max
**Created:** 2025-02-03
**Confidence:** high

## Summary

Non-interactive GCP/Firebase authentication using Service Account JSON key. Eliminates need for manual `gcloud auth login`.

## Problem

`gcloud auth login` requires interactive browser authentication, which fails in automated/CI environments and expires periodically.

## Solution

Use Service Account with JSON key for persistent, non-interactive authentication.

### Step 1: Create Service Account

```bash
gcloud iam service-accounts create claude-deployer \
  --display-name="Claude Code Deployer" \
  --project=YOUR_PROJECT_ID
```

### Step 2: Grant Required Roles

```bash
PROJECT_ID="YOUR_PROJECT_ID"
SA_EMAIL="claude-deployer@${PROJECT_ID}.iam.gserviceaccount.com"

# Cloud Run deployment
gcloud projects add-iam-policy-binding $PROJECT_ID \
  --member="serviceAccount:${SA_EMAIL}" \
  --role="roles/run.admin"

# Cloud Storage access
gcloud projects add-iam-policy-binding $PROJECT_ID \
  --member="serviceAccount:${SA_EMAIL}" \
  --role="roles/storage.admin"

# Cloud Build for container builds
gcloud projects add-iam-policy-binding $PROJECT_ID \
  --member="serviceAccount:${SA_EMAIL}" \
  --role="roles/cloudbuild.builds.editor"

# Act as service account (for Cloud Run)
gcloud projects add-iam-policy-binding $PROJECT_ID \
  --member="serviceAccount:${SA_EMAIL}" \
  --role="roles/iam.serviceAccountUser"
```

### Step 3: Download Key

```bash
mkdir -p ~/.gcp

gcloud iam service-accounts keys create ~/.gcp/claude-deployer-key.json \
  --iam-account=claude-deployer@YOUR_PROJECT_ID.iam.gserviceaccount.com
```

### Step 4: Set Environment Variable

Add to `~/.bashrc`, `~/.zshrc`, or Windows environment:

```bash
export GOOGLE_APPLICATION_CREDENTIALS="$HOME/.gcp/claude-deployer-key.json"
```

Windows (CMD):
```batch
setx GOOGLE_APPLICATION_CREDENTIALS "%USERPROFILE%\.gcp\claude-deployer-key.json"
```

## Firebase Integration

For Firebase Hosting, add additional role:

```bash
gcloud projects add-iam-policy-binding $PROJECT_ID \
  --member="serviceAccount:${SA_EMAIL}" \
  --role="roles/firebasehosting.admin"
```

## Roles Reference

| Role | Purpose |
|------|---------|
| `roles/run.admin` | Deploy to Cloud Run |
| `roles/storage.admin` | Access Cloud Storage buckets |
| `roles/cloudbuild.builds.editor` | Build container images |
| `roles/iam.serviceAccountUser` | Act as service account |
| `roles/firebasehosting.admin` | Deploy to Firebase Hosting |
| `roles/cloudfunctions.developer` | Deploy Cloud Functions |
| `roles/cloudscheduler.admin` | Manage Cloud Scheduler |
| `roles/cloudtasks.admin` | Manage Cloud Tasks |

## Security Notes

- Store key file in `~/.gcp/` (outside project directories)
- Add `*.json` to `.gitignore` in projects
- Never commit service account keys
- Rotate keys periodically
- Use minimal required roles (principle of least privilege)

## Verification

```bash
# Test authentication
gcloud auth activate-service-account --key-file=$GOOGLE_APPLICATION_CREDENTIALS
gcloud config list
```

## Related

- [GCP Skill](../../.claude/skills/gcp/SKILL.md)
- [Firebase Auth](firebase-auth.md)
