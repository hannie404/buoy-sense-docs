# Deployment Guide for BuoySense Documentation

This guide will help you deploy the documentation site to a subdomain like `docs-buoysense.yourdomain.com`.

## 📋 Prerequisites

- GitHub repository: `hannie404/buoy-sense-docs` ✅
- Vercel account (free)
- Custom domain access (for subdomain setup)

## 🚀 Deploy to Vercel

### Step 1: Import Project to Vercel

1. Go to [Vercel Dashboard](https://vercel.com/dashboard)
2. Click **Add New** → **Project**
3. Import from GitHub: `hannie404/buoy-sense-docs`
4. Configure project:
   - **Framework Preset**: Docusaurus
   - **Build Command**: `npm run build`
   - **Output Directory**: `build`
   - **Install Command**: `npm install`

5. Click **Deploy**

### Step 2: Set Up Custom Subdomain

#### Option A: Using Vercel DNS

1. In Vercel project, go to **Settings** → **Domains**
2. Add domain: `docs-buoysense.yourdomain.com`
3. Vercel will provide DNS records
4. Add to your DNS provider:
   ```
   Type: CNAME
   Name: docs-buoysense
   Value: cname.vercel-dns.com
   TTL: 3600
   ```

#### Option B: Using Your DNS Provider

1. Add domain in Vercel: `docs-buoysense.yourdomain.com`
2. Vercel shows you the CNAME record
3. Add to your DNS:
   ```
   Type: CNAME
   Name: docs-buoysense
   Value: <your-project>.vercel.app
   ```

### Step 3: Configure Build Settings

In Vercel Dashboard → **Settings** → **General**:

**Build & Development Settings**:
- Build Command: `npm run build`
- Output Directory: `build`
- Install Command: `npm install`

**Environment Variables** (if needed):
- None required for static docs

### Step 4: Enable Auto-Deploy

✅ Already enabled! Every push to `main` branch will trigger automatic deployment.

## 🔄 Continuous Deployment

Your documentation will auto-deploy when you:
1. Push to `main` branch
2. Merge a pull request
3. Make changes via GitHub web interface

## 📝 Making Updates

### Update Documentation

1. Clone the repo:
```bash
git clone https://github.com/hannie404/buoy-sense-docs.git
cd buoy-sense-docs
```

2. Make changes to `.md` files in `docs/`

3. Test locally:
```bash
npm start
```

4. Push changes:
```bash
git add -A
git commit -m "Update documentation"
git push
```

5. Vercel will automatically deploy in ~2 minutes

### Add New Pages

1. Create new `.md` file in `docs/`
2. Add frontmatter:
```markdown
---
title: New Page
sidebar_position: 5
---

# Content here
```

3. Update `sidebars.ts` if needed
4. Push to GitHub

## 🌐 Access Your Documentation

After deployment, your documentation will be available at:

- **Custom Domain**: https://docs-buoysense.yourdomain.com
- **Vercel URL**: https://buoy-sense-docs.vercel.app

## 🔗 Linking from Main Dashboard

Update your main dashboard to link to the docs:

In `buoy-sense-app-dashboard`:

```typescript
// components/dashboard-header.tsx or sidebar.tsx
<a href="https://docs-buoysense.yourdomain.com" target="_blank">
  Documentation
</a>
```

## ✅ Verification Checklist

- [ ] GitHub repository created and pushed
- [ ] Vercel project imported
- [ ] Custom subdomain configured
- [ ] DNS records added
- [ ] First deployment successful
- [ ] Custom domain working (allow 24-48h for DNS)
- [ ] Auto-deploy enabled
- [ ] Link added from main dashboard

## 🎯 Next Steps

1. **Customize Branding**: Edit `docusaurus.config.ts` colors and logo
2. **Add More API Docs**: Create files in `docs/api-reference/`
3. **User Guides**: Add tutorials in `docs/user-guide/`
4. **Blog**: Use the blog feature for updates and changelogs
5. **Search**: Enable Algolia DocSearch (free for open source)

## 🔧 Troubleshooting

**Build fails**:
- Check build logs in Vercel dashboard
- Verify `package.json` has correct scripts
- Run `npm run build` locally first

**Custom domain not working**:
- Wait 24-48 hours for DNS propagation
- Verify CNAME record with `dig docs-buoysense.yourdomain.com`
- Check DNS configuration in domain provider

**Changes not deploying**:
- Check Vercel deployment logs
- Verify git push was successful
- Check if build is triggered in Vercel dashboard

## 📞 Support

- Vercel Docs: https://vercel.com/docs
- Docusaurus Docs: https://docusaurus.io/docs
- GitHub Issues: https://github.com/hannie404/buoy-sense-docs/issues

---

**That's it! Your documentation is now deployed and will auto-update on every push! 🎉**
