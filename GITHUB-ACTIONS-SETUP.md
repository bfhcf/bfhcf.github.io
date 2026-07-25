# GitHub Actions Setup Guide

This guide walks you through setting up automated Jekyll builds with secure API key injection using GitHub Actions.

## Overview

Instead of storing API keys in the repository, we:
1. Store keys as **GitHub Secrets** (encrypted)
2. Use **GitHub Actions** to build Jekyll
3. Inject keys at build time into `_config_secrets.yml`
4. Deploy to GitHub Pages automatically

## Step 1: Add Secrets to GitHub

1. Go to your repository on GitHub: `https://github.com/bfhcf/bfhcf.github.io`

2. Click **Settings** → **Secrets and variables** → **Actions**

3. Click **"New repository secret"** and add:

   **Secret 1:**
   - Name: `YOUTUBE_API_KEY`
   - Value: `[paste your new YouTube API key here]`
   - Click "Add secret"

   **Secret 2:**
   - Name: `PODCAST_API_KEY`
   - Value: `[paste your podcast API key here]`
   - Click "Add secret"

## Step 2: Enable GitHub Pages to Use Actions

1. Go to **Settings** → **Pages**

2. Under **"Build and deployment"**, change:
   - Source: **GitHub Actions** (not "Deploy from a branch")

3. Save changes

## Step 3: Enable Workflow Permissions

1. Go to **Settings** → **Actions** → **General**

2. Scroll to **"Workflow permissions"**

3. Select **"Read and write permissions"**

4. Check ✅ **"Allow GitHub Actions to create and approve pull requests"**

5. Click **"Save"**

## Step 4: Push and Test

After pushing the workflow file (`.github/workflows/jekyll.yml`), the build will:

1. ✅ Trigger automatically on every push to `master`
2. ✅ Check out your code
3. ✅ Install Ruby and dependencies
4. ✅ Create `_config_secrets.yml` with your secrets
5. ✅ Build Jekyll with both `_config.yml` and `_config_secrets.yml`
6. ✅ Deploy to GitHub Pages

### Monitor Build Status

- Go to **Actions** tab in your repository
- Watch the "Build and Deploy Jekyll Site" workflow
- Check for any errors

## Local Development Setup

For local development with API keys:

### Option 1: Using _config.local.yml (Recommended)

1. Copy the example config:
   ```bash
   cp _config.local.yml.example _config.local.yml
   ```

2. Edit `_config.local.yml` and add your API keys

3. Build Jekyll with both configs:
   ```bash
   bundle exec jekyll serve --config _config.yml,_config.local.yml
   ```

### Option 2: Using Environment Variables

1. Copy `.env.example` to `.env`:
   ```bash
   cp .env.example .env
   ```

2. Edit `.env` and add your keys

3. Export and build:
   ```bash
   export $(cat .env | xargs)
   bundle exec jekyll serve
   ```

## How It Works

### GitHub Actions Workflow

The workflow (`.github/workflows/jekyll.yml`) does this:

```yaml
# Creates a temporary config with secrets
- name: Create _config_secrets.yml with API keys
  run: |
    cat > _config_secrets.yml << EOF
    youtube_api_key: ${{ secrets.YOUTUBE_API_KEY }}
    podcast_api_key: ${{ secrets.PODCAST_API_KEY }}
    EOF

# Builds Jekyll with both configs (values in _config_secrets.yml override _config.yml)
- name: Build with Jekyll
  run: bundle exec jekyll build --config _config.yml,_config_secrets.yml
```

### Security Benefits

✅ **Keys never appear in git history**
✅ **Keys encrypted at rest in GitHub Secrets**
✅ **Keys only accessible during build**
✅ **`_config_secrets.yml` never committed** (in .gitignore)
✅ **Can rotate keys without code changes**

## Troubleshooting

### Build Fails with "Secret not found"

- Make sure you added both secrets: `YOUTUBE_API_KEY` and `PODCAST_API_KEY`
- Secret names are case-sensitive and must match exactly

### GitHub Pages Shows Old Site

- Check the Actions tab for build status
- Wait 1-2 minutes for deployment to complete
- Hard refresh your browser (Ctrl+Shift+R or Cmd+Shift+R)

### Local Build Can't Find API Keys

Make sure you're using the config override:
```bash
bundle exec jekyll serve --config _config.yml,_config.local.yml
```

Or exporting environment variables if using that method.

### Workflow Doesn't Run

1. Check that GitHub Pages source is set to "GitHub Actions"
2. Verify workflow permissions are correct
3. Look for any syntax errors in `.github/workflows/jekyll.yml`

## Files Overview

| File | Purpose | Committed? |
|------|---------|------------|
| `.github/workflows/jekyll.yml` | GitHub Actions workflow | ✅ Yes |
| `_config.yml` | Main config (empty API keys) | ✅ Yes |
| `_config.local.yml.example` | Template for local dev | ✅ Yes |
| `_config.local.yml` | Your local API keys | ❌ No (gitignored) |
| `_config_secrets.yml` | Generated during build | ❌ No (gitignored) |
| `.env.example` | Template for environment vars | ✅ Yes |
| `.env` | Your environment variables | ❌ No (gitignored) |

## Next Steps

1. ✅ Add secrets to GitHub (Step 1 above)
2. ✅ Enable GitHub Actions for Pages (Step 2)
3. ✅ Set workflow permissions (Step 3)
4. ✅ Push this workflow to GitHub
5. ✅ Watch the Actions tab for successful build
6. ✅ Verify your site works at https://www.breadfromheaven.org

## Monitoring

After setup, you can:
- View build logs in the **Actions** tab
- Get email notifications on build failures
- See deployment history in **Settings** → **Pages**

## Rotating Keys

To rotate API keys:
1. Generate new keys in Google Cloud Console / API provider
2. Update GitHub Secrets (Settings → Secrets and variables → Actions)
3. Update your local `_config.local.yml` or `.env`
4. Push any commit to trigger a rebuild

No code changes needed!

---

**Created:** 2026-07-25  
**Status:** Ready to deploy
