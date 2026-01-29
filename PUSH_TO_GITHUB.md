# Push to GitHub Instructions

## Step 1: Create GitHub Repository

1. Go to https://github.com/new
2. Repository name: `billing-admin-saas` (or your preferred name)
3. Description: "Production-grade multi-tenant SaaS Billing & Admin platform"
4. Choose Public or Private
5. **DO NOT** initialize with README, .gitignore, or license (we already have these)
6. Click "Create repository"

## Step 2: Add Remote and Push

After creating the repository, GitHub will show you commands. Use these:

```bash
cd billing-admin-saas

# Add the remote (replace YOUR_USERNAME with your GitHub username)
git remote add origin https://github.com/YOUR_USERNAME/billing-admin-saas.git

# Or if using SSH:
# git remote add origin git@github.com:YOUR_USERNAME/billing-admin-saas.git

# Rename branch to main (if needed)
git branch -M main

# Push to GitHub
git push -u origin main
```

## Alternative: One-liner after creating repo

If you've already created the repo, you can run:

```bash
cd billing-admin-saas
git remote add origin https://github.com/YOUR_USERNAME/billing-admin-saas.git
git branch -M main
git push -u origin main
```

Replace `YOUR_USERNAME` with your actual GitHub username.


