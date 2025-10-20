# 📦 Installation Guide

This guide will walk you through setting up your automated GitHub profile step-by-step.

## 📋 Prerequisites

Before you begin, make sure you have:

- ✅ A GitHub account
- ✅ Git installed on your computer
- ✅ Node.js 18 or higher installed ([Download](https://nodejs.org/))
- ✅ A code editor (VS Code recommended)
- ✅ Basic command line knowledge

## 🚀 Installation Steps

### Step 1: Create Your Profile Repository

1. **Go to GitHub** and click the **+** icon → **New repository**

2. **Repository name:** Must be exactly your username
   ```
   Example: If your username is "johndoe"
   Repository name must be: "johndoe"
   ```

3. **Settings:**
   - ✅ Public
   - ✅ Add a README file
   - ❌ Don't add .gitignore or license (we'll add them)

4. Click **Create repository**

---

### Step 2: Clone the Repository

Open your terminal and run:

```bash
# Replace YOUR_USERNAME with your GitHub username
git clone https://github.com/YOUR_USERNAME/YOUR_USERNAME.git
cd YOUR_USERNAME
```

---

### Step 3: Download Project Files

**Option A: Download from releases**
1. Go to the [releases page](https://github.com/Dineshs737/test-custom-profile)
2. Download the latest release
3. Extract files into your repository folder

**Option B: Clone the template**
```bash
# Download the template files
git clone https://github.com/Dineshs737/test-custom-profile
cp -r temp/src temp/.github temp/package.json temp/tsconfig.json temp/.gitignore .
rm -rf temp
```

---

### Step 4: Create Folder Structure

Your repository should look like this:

```
YOUR_USERNAME/
├── .github/
│   └── workflows/
│       └── update-profile.yml
├── src/
│   └── index.ts
├── package.json
├── tsconfig.json
├── .gitignore
└── README.md (will be auto-generated)
```

Create the folders:

```bash
mkdir -p .github/workflows
mkdir -p src
```

---

### Step 5: Copy Configuration Files

**Create `.gitignore`:**
```bash
cat > .gitignore << 'EOF'
node_modules/
dist/
.env
*.log
.DS_Store
*.js.map
EOF
```

**Create `package.json`:**
```bash
cat > package.json << 'EOF'
{
  "name": "github-profile-generator",
  "version": "1.0.0",
  "description": "Automated GitHub profile README generator",
  "main": "dist/index.js",
  "scripts": {
    "build": "tsc",
    "generate": "node dist/index.js",
    "dev": "ts-node src/index.ts"
  },
  "dependencies": {
    "@octokit/rest": "^20.0.2"
  },
  "devDependencies": {
    "@types/node": "^20.10.0",
    "ts-node": "^10.9.2",
    "typescript": "^5.3.3"
  }
}
EOF
```

**Create `tsconfig.json`:**
```bash
cat > tsconfig.json << 'EOF'
{
  "compilerOptions": {
    "target": "ES2020",
    "module": "commonjs",
    "lib": ["ES2020"],
    "outDir": "./dist",
    "rootDir": "./src",
    "strict": true,
    "esModuleInterop": true,
    "skipLibCheck": true,
    "moduleResolution": "node"
  },
  "include": ["src/**/*"],
  "exclude": ["node_modules", "dist"]
}
EOF
```

Copy:
- `src/index.ts` from the template
- `.github/workflows/update-profile.yml` from the template

---

### Step 6: Install Dependencies

```bash
npm install
```

You should see:
```
✅ added 150+ packages
```

---

### Step 7: Customize Your Information

Edit `src/index.ts` and update your information:

```typescript
// Find these lines and update:
location: "Your City, Country",
bio: "Your Job Title",
company: "@YourCompany",
```

**Tech Stack:**
Update the technologies displayed in your profile card by modifying the SVG generation section.

---

### Step 8: Create GitHub Personal Access Token

1. **Go to:** [https://github.com/settings/tokens](https://github.com/settings/tokens)

2. **Click:** "Generate new token" → "Generate new token (classic)"

3. **Configure:**
   - **Note:** `GitHub Profile Auto-Updater`
   - **Expiration:** No expiration (or 1 year)
   
4. **Select scopes:**
   - ✅ **repo** (check all sub-boxes)
   - ✅ **read:user**
   - ✅ **user:email**

5. **Click:** "Generate token"

6. **IMPORTANT:** Copy the token immediately!
   ```
   It will look like: ghp_xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
   ```
   
   ⚠️ **You won't be able to see it again!**

---

### Step 9: Add Token to Repository Secrets

1. **Go to your repository on GitHub:**
   ```
   https://github.com/YOUR_USERNAME/YOUR_USERNAME
   ```

2. **Click:** Settings (top menu bar)

3. **Click:** Secrets and variables → Actions (left sidebar)

4. **Click:** "New repository secret" (green button)

5. **Fill in:**
   - **Name:** `GH_TOKEN` (must be exact)
   - **Secret:** Paste your token from Step 8

6. **Click:** "Add secret"

7. **Verify:** You should see `GH_TOKEN` in the secrets list

---

### Step 10: Test Locally (Optional but Recommended)

```bash
# Build the TypeScript
npm run build

# Should create dist/index.js
ls -la dist/

# Test generation (replace with your token)
export GITHUB_TOKEN=ghp_your_token_here
npm run generate

# Check if files were created
ls -la profile.svg README.md

# View the generated files
cat README.md
```

If successful, you'll see:
- ✅ `profile.svg` created
- ✅ `README.md` created
- ✅ Stats summary displayed

---

### Step 11: Commit and Push to GitHub

```bash
# Add all files
git add .

# Commit with a message
git commit -m "🎉 Initial setup: Automated GitHub profile generator"

# Push to GitHub
git push origin main
```

If you get an error about branch name, try:
```bash
git push origin master
```

---

### Step 11.5: Enable Automatic Updates (IMPORTANT!)

⚠️ **By default, the workflow is set to manual trigger only.** You need to enable the schedule for automatic updates.

**Edit `.github/workflows/update-profile.yml`:**

Find these lines at the top:
```yaml
on:
  #schedule:
    # Run at minute 5 past every hour (more reliable)
  # - cron: "5 */3 * * *"
  workflow_dispatch: # Manual trigger
```

**Uncomment the schedule** to enable automatic updates every 3 hours:
```yaml
on:
  schedule:
    # Run every 3 hours at minute 5
    - cron: "5 */3 * * *"
  workflow_dispatch: # Manual trigger
```

**Save the file and push:**
```bash
git add .github/workflows/update-profile.yml
git commit -m "⏰ Enable automatic updates every 3 hours"
git push
```

**Update Schedule Options:**

Choose how often you want updates:

```yaml
# Every 3 hours (recommended)
- cron: "5 */3 * * *"

# Every 6 hours (saves Actions minutes)
- cron: "5 */6 * * *"

# Every 12 hours (twice daily)
- cron: "5 */12 * * *"

# Once per day at midnight UTC
- cron: "5 0 * * *"

# Every hour (frequent updates)
- cron: "5 * * * *"
```

💡 **Why is it commented out by default?**
- Allows you to test the setup first
- You can verify everything works before enabling auto-updates
- Prevents unnecessary runs during initial setup

---

### Step 12: Enable GitHub Actions

1. **Go to your repository on GitHub**

2. **Click the "Actions" tab**

3. If you see "Workflows aren't being run on this forked repository", click **"I understand my workflows, go ahead and enable them"**

4. You should see your workflow: **"Update GitHub Profile"**

---

### Step 13: Run Your First Workflow

1. **In the Actions tab**, click **"Update GitHub Profile"** in the left sidebar

2. **Click the "Run workflow" button** (blue button on the right)

3. **Select branch:** `main` (or `master`)

4. **Click "Run workflow"** (green button)

5. **Wait 10-20 seconds**, then refresh the page

6. You should see a workflow run in progress (yellow circle 🟡)

7. **Click on the workflow run** to see detailed logs

8. **Wait 1-2 minutes** for it to complete (green checkmark ✅)

---

### Step 14: Verify Your Profile

1. **Go to your profile:**
   ```
   https://github.com/YOUR_USERNAME
   ```

2. **You should see:**
   - ✅ Animated profile card
   - ✅ Your stats displayed
   - ✅ Tech stack with icons
   - ✅ GitHub activity metrics

3. **Check repository:**
   - `profile.svg` should exist
   - `README.md` should exist
   - Recent commit: "🤖 Auto-update profile stats"

---

## ✅ Verification Checklist

Go through this checklist to ensure everything is working:

- [ ] Repository created with correct name (matches username)
- [ ] All files in correct locations
- [ ] `npm install` completed successfully
- [ ] `npm run build` works without errors
- [ ] `GH_TOKEN` secret added to repository
- [ ] Workflow file exists in `.github/workflows/`
- [ ] First workflow run completed successfully
- [ ] `profile.svg` visible in repository
- [ ] `README.md` updated in repository
- [ ] Profile displays correctly on `github.com/YOUR_USERNAME`
- [ ] No errors in Actions tab

---

## 🎨 Post-Installation Customization

### Update Schedule

Edit `.github/workflows/update-profile.yml`:

```yaml
schedule:
  - cron: '5 */3 * * *'  # Current: Every 3 hours
  # - cron: '5 */6 * * *'  # Every 6 hours
  # - cron: '5 0 * * *'    # Daily at midnight
```

### Change Colors

In `src/index.ts`, find color codes:

```typescript
// Dark theme (current)
fill="#0d1117"  // Background
fill="#58a6ff"  // Blue accent

// Light theme example
fill="#ffffff"  // Background
fill="#0366d6"  // Blue accent
```

### Add More Technologies

Find the Tech Stack section and add:

```typescript
<g transform="translate(x, y)">
  <rect width="95" height="32" rx="8" fill="#0d1117" stroke="#FF6B6B"/>
  <text fill="#FF6B6B">Ruby</text>
</g>
```

### Modify Stats Displayed

Edit the `generateSVG()` method to show/hide different metrics.

---

## 🔧 Troubleshooting

### Issue: "npm: command not found"

**Solution:** Install Node.js from [nodejs.org](https://nodejs.org/)

### Issue: "Permission denied" when pushing

**Solution:**
```bash
# Set up authentication
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"

# If using HTTPS, you may need a personal access token
# Use SSH instead: git remote set-url origin git@github.com:USERNAME/USERNAME.git
```

### Issue: Workflow fails with "GH_TOKEN not found"

**Solution:**
1. Double-check secret name is exactly `GH_TOKEN`
2. Verify secret exists in Settings → Secrets
3. Re-create the secret if needed

### Issue: "tsc: command not found"

**Solution:**
```bash
# Reinstall dependencies
rm -rf node_modules package-lock.json
npm install
```

### Issue: Files generated but not showing on profile

**Solution:**
1. Check if commit happened (Actions → View logs)
2. Wait 5 minutes for GitHub cache to clear
3. Hard refresh your profile page (Ctrl+F5 or Cmd+Shift+R)
4. Check repository - files should be there

### Issue: Workflow doesn't run automatically

**Solution:**
1. Make a commit to keep repo active
2. Manually trigger once to activate schedule
3. Check workflow is enabled (Actions tab)
4. GitHub Actions cron can be delayed 3-15 minutes

---

## 📊 Understanding the Workflow

### What Happens Every 3 Hours:

1. **GitHub Actions triggers** the workflow
2. **Checks out** your repository code
3. **Installs** Node.js and dependencies
4. **Builds** TypeScript to JavaScript
5. **Fetches** your GitHub stats via API
6. **Generates** profile.svg and README.md
7. **Commits** changes if stats changed
8. **Pushes** to your repository
9. **Profile updates** automatically on GitHub

### Files Modified by Workflow:

- `profile.svg` - Your animated profile card
- `README.md` - Your profile README

### Files NOT Modified:

- `src/index.ts` - Your source code
- `.github/workflows/` - Workflow configuration
- `package.json` - Dependencies
- Everything else stays untouched

---

## 🎓 Advanced Setup

### Run on Multiple Schedules

```yaml
schedule:
  - cron: '5 */3 * * *'  # Every 3 hours
  - cron: '0 9 * * 1'    # Every Monday at 9 AM
```

### Add Workflow Notifications

Get notified when workflow runs:

1. Go to: Settings → Notifications → Actions
2. Enable: "Send notifications for failed workflows"

### Use Different Branches

```yaml
push:
  branches:
    - main
    - develop  # Also trigger on develop branch
```

### Add Manual Inputs

```yaml
workflow_dispatch:
  inputs:
    force_update:
      description: 'Force update even if no changes'
      required: false
      default: 'false'
```

---

## 📱 Mobile Setup

You can also set this up from your phone using GitHub's mobile app:

1. Install GitHub Mobile app
2. Create repository via app
3. Use GitHub web interface for token creation
4. Use GitHub Codespaces for editing files
5. Trigger workflows from mobile app

---

## 🚀 Next Steps

After successful installation:

1. ⭐ **Star the repository** if you found it helpful
2. 🎨 **Customize** colors and layout
3. 📊 **Share** your profile with others
4. 🤝 **Contribute** improvements back to the project
5. 📖 **Read** the main README for more features

---

## 💡 Tips for Success

✅ **Test locally first** before pushing to GitHub
✅ **Check Actions logs** if something doesn't work
✅ **Keep token secure** - never commit it
✅ **Commit regularly** to keep workflow active
✅ **Force refresh** (Ctrl+F5) to see updates immediately
✅ **Be patient** - First run can take 2-3 minutes

---

## 🆘 Getting Help

If you're stuck:

1. **Check the logs** in Actions tab
2. **Search existing issues** on GitHub
3. **Open a new issue** with details
4. **Join discussions** for community help
5. **Read the FAQ** in main README

---

## 📚 Additional Resources

- [GitHub Actions Documentation](https://docs.github.com/en/actions)
- [GitHub REST API](https://docs.github.com/en/rest)
- [TypeScript Documentation](https://www.typescriptlang.org/docs/)
- [Node.js Documentation](https://nodejs.org/docs/)
- [Cron Expression Guide](https://crontab.guru/)

---

## 🎉 Success!

Congratulations! Your automated GitHub profile is now set up and will update every 3 hours automatically!

Your profile URL: `https://github.com/Dineshs737`

**Enjoy your awesome new profile!** 🚀

---

<div align="center">

### Questions? Issues? Contributions?

[Open an Issue](https://github.com/Dineshs737/test-custom-profile/issues) · [Start a Discussion](https://github.com/Dineshs737/test-custom-profile/discussions)

**Made with ❤️ for the GitHub community**

</div>
