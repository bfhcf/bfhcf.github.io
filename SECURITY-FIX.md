# Security Fix: Exposed API Keys

## Issue
Google detected exposed API keys in the public GitHub repository:
- YouTube API Key: `AIzaSyADnoqPB_iM1Q2qhtbCe64x3HS4fB903z0`
- Podcast API Key: `f3f01cb7cc23bb7b308833bab0f18db9`

## Immediate Actions Required

### 1. Regenerate API Keys

#### YouTube API Key
1. Go to [Google Cloud Console Credentials](https://console.cloud.google.com/apis/credentials?project=youtube-3-297801)
2. Find the exposed key `AIzaSyADnoqPB_iM1Q2qhtbCe64x3HS4fB903z0`
3. Click "Edit" and then "Regenerate Key"
4. **Add API restrictions** to limit key usage:
   - Application restrictions: HTTP referrers (websites)
   - Add: `https://www.breadfromheaven.org/*`, `https://breadfromheaven.org/*`
   - API restrictions: Restrict to YouTube Data API v3 only
5. Save the new key securely

#### Podcast API Key
1. Log into your podcast API service (ListenNotes or similar)
2. Regenerate/revoke the exposed key: `f3f01cb7cc23bb7b308833bab0f18db9`
3. Generate a new key
4. Add domain restrictions if available

### 2. Set Up Environment Variables

#### For Local Development
1. Copy `.env.example` to `.env`:
   ```bash
   cp .env.example .env
   ```

2. Edit `.env` and add your NEW keys:
   ```bash
   YOUTUBE_API_KEY=your_new_youtube_api_key
   PODCAST_API_KEY=your_new_podcast_api_key
   ```

3. Load environment variables before building:
   ```bash
   export $(cat .env | xargs)
   bundle exec jekyll build
   ```

#### For GitHub Pages Deployment
GitHub Pages doesn't support environment variables natively. You have two options:

**Option A: Use GitHub Actions with Secrets (Recommended)**
1. Go to your repo Settings → Secrets and variables → Actions
2. Add repository secrets:
   - `YOUTUBE_API_KEY`: your new YouTube key
   - `PODCAST_API_KEY`: your new podcast key
3. Create `.github/workflows/jekyll.yml` to build with secrets
4. The keys will be injected during build time

**Option B: Use API Key Restrictions Only**
If you must keep keys in `_config.yml`:
1. Keep the keys in the file BUT add strict API restrictions:
   - HTTP referrer restrictions (your domain only)
   - API restrictions (specific APIs only)
   - Usage quotas and alerts
2. This limits damage if keys are exposed
3. Still not ideal, but better than unrestricted keys

### 3. Remove Keys from Git History

The keys exist in past commits and need to be removed:

```bash
# Option 1: Use BFG Repo-Cleaner (easier)
# Download from: https://rtyley.github.io/bfg-repo-cleaner/
brew install bfg  # or download jar file

# Create a file with the exposed keys
cat > passwords.txt << 'EOF'
AIzaSyADnoqPB_iM1Q2qhtbCe64x3HS4fB903z0
f3f01cb7cc23bb7b308833bab0f18db9
EOF

# Remove passwords from history
bfg --replace-text passwords.txt
git reflog expire --expire=now --all && git gc --prune=now --aggressive

# Force push to update remote history (WARNING: This rewrites history)
git push --force
```

```bash
# Option 2: Use git filter-repo (more powerful)
# Install: pip install git-filter-repo
git filter-repo --invert-paths --path _config.yml
# Then re-add _config.yml with environment variables
```

**⚠️ WARNING:** Rewriting git history will affect anyone who has cloned the repo. Coordinate with your team.

### 4. Monitor Usage

1. Check [Google Cloud Console](https://console.cloud.google.com/apis/dashboard?project=youtube-3-297801) for unexpected usage
2. Set up billing alerts
3. Review API usage regularly

## Files Changed

- `_config.yml` - Replaced API keys with environment variable placeholders
- `.gitignore` - Added `.env` and `.env.local`
- `.env.example` - Template for required environment variables
- `SECURITY-FIX.md` - This documentation

## Prevention

- ✅ Never commit API keys, passwords, or secrets to git
- ✅ Use environment variables for sensitive data
- ✅ Add `.env` to `.gitignore`
- ✅ Use API restrictions (domain, API type, quotas)
- ✅ Set up security scanning (GitHub Advanced Security)
- ✅ Review commits before pushing

## Resources

- [Google API Key Best Practices](https://cloud.google.com/docs/authentication/api-keys)
- [GitHub Removing Sensitive Data](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/removing-sensitive-data-from-a-repository)
- [BFG Repo-Cleaner](https://rtyley.github.io/bfg-repo-cleaner/)

---

**Status:** Keys removed from current code, awaiting regeneration and git history cleanup.

**Date:** 2026-07-25
