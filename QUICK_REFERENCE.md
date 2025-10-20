# 🚀 Quick Reference Guide

## 📝 Common Tasks

### Enable Automatic Updates

**Default state:** Schedule is commented out (manual trigger only)

**To enable automatic updates every 3 hours:**

```yaml
# Edit: .github/workflows/update-profile.yml
on:
  schedule:
    - cron: "5 */3 * * *"  # ← Uncomment these lines
  workflow_dispatch:
```

**Then commit and push:**
```bash
git add .github/workflows/update-profile.yml
git commit -m "⏰ Enable automatic updates"
git push
```

---

### Disable Automatic Updates

**To run manually only:**

```yaml
# Edit: .github/workflows/update-profile.yml
on:
  #schedule:              # ← Comment out these lines
  #  - cron: "5 */3 * * *"
  workflow_dispatch:
```

---

### Change Update Frequency

| Frequency | Cron Expression | Updates per day |
|-----------|-----------------|-----------------|
| Every 1 hour | `5 * * * *` | 24 |
| Every 3 hours | `5 */3 * * *` | 8 |
| Every 6 hours | `5 */6 * * *` | 4 |
| Every 12 hours | `5 */12 * * *` | 2 |
| Once daily | `5 0 * * *` | 1 |

**Example:**
```yaml
schedule:
  - cron: "5 */6 * * *"  # Every 6 hours
```

---

### Manual Trigger

1. Go to: `github.com/YOUR_USERNAME/YOUR_USERNAME/actions`
2. Click: "Update GitHub Profile"
3. Click: "Run workflow" button
4. Select branch: `main`
5. Click: "Run workflow"

---

### Update Your Information

**Edit `src/index.ts`:**

```typescript
// Around line 150-160, find:
location: "Your City, Country",
bio: "Your Job Title",
company: "@YourCompany",
```

**Then rebuild and push:**
```bash
npm run build
git add src/index.ts dist/
git commit -m "📝 Update personal information"
git push
```

---

### Test Locally

```bash
# Set token
export GITHUB_TOKEN=your_token_here

# Build and generate
npm run build
npm run generate

# Check output
ls -la profile.svg README.md
cat README.md
```

---

### Rebuild After Changes

```bash
# After editing src/index.ts:
npm run build
git add dist/
git commit -m "🔨 Rebuild after changes"
git push
```

---

### Check Workflow Status

**Via Web:**
- Go to Actions tab
- Look for green ✅ (success) or red ❌ (failed)

**Via CLI:**
```bash
# Install GitHub CLI
gh workflow list
gh run list
gh run view
```

---

### Troubleshooting Commands

```bash
# Verify file structure
ls -la .github/workflows/
ls -la src/

# Check dependencies
npm list

# Rebuild everything
rm -rf node_modules dist
npm install
npm run build

# Force workflow run
git commit --allow-empty -m "Trigger workflow"
git push
```

---

## 🎨 Quick Customizations

### Change Colors

**Edit `src/index.ts`:**
```typescript
// Find color codes like:
fill="#0d1117"  // Background
fill="#58a6ff"  // Blue accent
fill="#238636"  // Green

// Replace with your colors:
fill="#1a1b27"  // New background
fill="#7aa2f7"  // New accent
```

### Add Technology Badge

**In `src/index.ts`, find Tech Stack section:**
```typescript
<g transform="translate(x, y)">
  <rect width="95" height="32" rx="8" fill="#0d1117" stroke="#YOUR_COLOR"/>
  <text fill="#YOUR_COLOR">Tech Name</text>
</g>
```

### Hide/Show Stats

**Comment out sections you don't want:**
```typescript
// Hide commits stat:
/*
<g transform="translate(0, 0)">
  <!-- Commits stat -->
</g>
*/
```

---

## ⚠️ Important Notes

### Schedule is Disabled by Default

- ✅ **Allows testing first**
- ✅ **Prevents wasted Actions minutes**
- ⚠️ **Must uncomment to enable auto-updates**

### Token Security

- ❌ Never commit token in code
- ✅ Store in repository secrets as `GH_TOKEN`
- ✅ Token is encrypted and hidden in logs

### Actions Minutes

- Free tier: 2,000 minutes/month
- Every 3 hours: ~240 runs/month (~240 minutes)
- Every 6 hours: ~120 runs/month (~120 minutes)

### Cron Delays

- GitHub Actions cron can be delayed 3-15 minutes
- This is normal behavior
- Not guaranteed to run at exact time

---

## 📚 File Locations

| File | Purpose | Edit? |
|------|---------|-------|
| `.github/workflows/update-profile.yml` | Workflow config | ✅ Yes (for schedule) |
| `src/index.ts` | Generator code | ✅ Yes (for customization) |
| `package.json` | Dependencies | ⚠️ Rarely |
| `tsconfig.json` | TypeScript config | ⚠️ Rarely |
| `profile.svg` | Generated card | ❌ Auto-generated |
| `README.md` | Profile README | ❌ Auto-generated |
| `dist/` | Compiled code | ❌ Auto-generated |

---

## 🔗 Quick Links

- **Your Profile:** `github.com/YOUR_USERNAME`
- **Actions Tab:** `github.com/YOUR_USERNAME/YOUR_USERNAME/actions`
- **Settings → Secrets:** `github.com/YOUR_USERNAME/YOUR_USERNAME/settings/secrets/actions`
- **Create Token:** [github.com/settings/tokens](https://github.com/settings/tokens)
- **Cron Helper:** [crontab.guru](https://crontab.guru)

---

## 💡 Pro Tips

1. **Test locally** before pushing to GitHub
2. **Enable schedule** after first successful run
3. **Check Actions logs** if something fails
4. **Commit regularly** to keep workflow active
5. **Use `git push --force-with-lease`** if needed
6. **Hard refresh profile** (Ctrl+F5) to see updates

---

## 🆘 Quick Fixes

| Problem | Quick Fix |
|---------|-----------|
| Workflow not running | Uncomment schedule in workflow file |
| Token error | Check `GH_TOKEN` secret exists |
| Build fails | `npm install && npm run build` |
| Files not updated | Check Actions logs for errors |
| Old data showing | Hard refresh: Ctrl+F5 |

---

<div align="center">

**Need more help?** Check [INSTALLATION.md](INSTALLATION.md) or [README.md](README.md)

</div>
