# Too Humble Couture - Deployment Guide

## Quick Deploy to Vercel

### Option 1: Vercel Dashboard (Easiest)

1. **Go to Vercel**
   - Visit [vercel.com](https://vercel.com)
   - Log in to your account

2. **Create New Project**
   - Click "Add New..." → "Project"
   - Choose "Upload" (or "Import Git Repository" if you push to GitHub first)

3. **Upload Files**
   - Drag and drop the `too-humble-couture-site` folder
   - Or upload the entire project directory

4. **Configure Settings**
   - Framework Preset: `Other` (static site)
   - Root Directory: `./`
   - Output Directory: `public`
   - Click "Deploy"

5. **Wait for Deployment**
   - Vercel will build and deploy automatically
   - You'll get a URL like `too-humble-couture-site.vercel.app`

---

### Option 2: Vercel CLI

1. **Install Vercel CLI** (if not installed)
   ```bash
   npm install -g vercel
   ```

2. **Login to Vercel**
   ```bash
   vercel login
   ```

3. **Navigate to Project**
   ```bash
   cd too-humble-couture-site
   ```

4. **Deploy**
   ```bash
   vercel --prod
   ```

5. **Follow Prompts**
   - Link to existing project or create new
   - Confirm settings

---

## Connect Custom Domain (toohumblecouture.com)

### Step 1: Add Domain in Vercel

1. Go to your project in Vercel Dashboard
2. Click **"Settings"** → **"Domains"**
3. Enter `toohumblecouture.com`
4. Click **"Add"**

### Step 2: Configure DNS Records

Vercel will show you the required DNS records. Update your domain registrar:

**Option A: Using Vercel Nameservers (Recommended)**
Point your domain nameservers to:
```
ns1.vercel-dns.com
ns2.vercel-dns.com
```

**Option B: Using A/CNAME Records**
Add these records at your domain registrar:

| Type | Name | Value |
|------|------|-------|
| A | @ | 76.76.21.21 |
| CNAME | www | cname.vercel-dns.com |

### Step 3: Add WWW Redirect

1. In Vercel Domains settings
2. Add `www.toohumblecouture.com`
3. Set it to redirect to `toohumblecouture.com`

### Step 4: Enable HTTPS

- Vercel automatically provisions SSL certificate
- Wait 5-10 minutes for HTTPS to activate
- No additional configuration needed

---

## Post-Deployment Checklist

After deploying, verify these work:

- [ ] Homepage loads at toohumblecouture.com
- [ ] Navigation menu works (Shop, About, Size Guide, Contact)
- [ ] All legal pages load:
  - [ ] `/privacy` - Privacy Policy
  - [ ] `/terms` - Terms of Service
  - [ ] `/returns` - Returns Policy
  - [ ] `/shipping` - Shipping Info
  - [ ] `/faq` - FAQ
- [ ] Contact form submits (currently shows toast message)
- [ ] Newsletter form works
- [ ] Mobile menu toggles correctly
- [ ] Cart modal opens/closes
- [ ] Smooth scroll works on anchor links
- [ ] HTTPS is active (green lock icon)

---

## Kit Email Integration

### Update Newsletter Form

1. Log into [kit.com](https://kit.com)
2. Go to **Forms** → Create new form or use existing
3. Get your form ID from the embed code
4. Update `index.html` - find this line:

```html
<form class="newsletter-form" id="newsletter-form" action="https://app.kit.com/forms/YOUR_FORM_ID/subscriptions" method="post">
```

Replace `YOUR_FORM_ID` with your actual Kit form ID.

### Alternative: Kit JavaScript Embed

For better functionality, replace the newsletter form with Kit's JavaScript embed:

1. In Kit, get the JavaScript embed code
2. Replace the existing `newsletter-form` with Kit's code
3. Style to match your site

---

## Environment Variables (If Needed)

If you add backend functionality later, set these in Vercel:

1. Go to Project → **Settings** → **Environment Variables**
2. Add variables as needed:

| Variable | Description |
|----------|-------------|
| `KIT_API_KEY` | For Kit email automation |
| `STRIPE_KEY` | If adding payments |
| `DATABASE_URL` | If adding Neon PostgreSQL |

---

## Updating the Site

### Quick Updates
1. Make changes to files locally
2. Run `vercel --prod` to redeploy

### Via Vercel Dashboard
1. Go to project → Deployments
2. Click "Redeploy" on latest deployment
3. Or upload new files

### Via GitHub (Recommended for Ongoing)
1. Push project to GitHub repository
2. Connect GitHub repo to Vercel
3. Auto-deploys on every push to main branch

---

## Troubleshooting

### Site not loading
- Check Vercel deployment logs
- Verify DNS propagation: [dnschecker.org](https://dnschecker.org)
- Clear browser cache

### HTTPS not working
- Wait 10-15 minutes for SSL provisioning
- Check domain is properly verified in Vercel

### 404 on pages
- Ensure files are in `/public` directory
- Check `vercel.json` configuration
- Verify `cleanUrls: true` is set

### Forms not working
- Update Kit form ID
- Check browser console for errors
- Verify form action URL

---

## File Structure Reference

```
too-humble-couture-site/
├── public/
│   ├── index.html        # Homepage
│   ├── privacy.html      # Privacy Policy
│   ├── terms.html        # Terms of Service
│   ├── returns.html      # Returns Policy
│   ├── shipping.html     # Shipping Info
│   └── faq.html          # FAQ
├── printify-designs/     # Design files for Printify
│   ├── *.png             # Print-ready PNG files
│   └── *.svg             # Editable source files
├── vercel.json           # Vercel configuration
├── package.json          # Project metadata
├── PRINTIFY-SETUP-GUIDE.md
├── DEPLOYMENT-GUIDE.md   # This file
└── README.md
```

---

## Support

For Vercel issues: [vercel.com/docs](https://vercel.com/docs)
For Kit issues: [help.kit.com](https://help.kit.com)

---

*Last updated: November 2025*
