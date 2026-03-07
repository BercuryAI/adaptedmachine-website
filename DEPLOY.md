# Adapted Machine Website — Deployment Guide

## What's Here
`index.html` — Complete single-page website, production-ready. All copy, styles, and JS are embedded.

---

## Step 1: GitHub Repo Setup

```bash
cd /Users/jackberkery/.openclaw/workspace/adaptedmachine-website

# Initialize and push to GitHub
git init
git add index.html
git commit -m "feat: initial Adapted Machine website — v1 for staging review"

# Create the repo under BercuryAI (requires gh CLI logged into BercuryAI account)
gh repo create BercuryAI/adaptedmachine-website --public --source=. --remote=origin --push

# Create the staging branch
git checkout -b staging
git push origin staging

# Switch back to main
git checkout main
```

---

## Step 2: Connect to Cloudflare Pages

1. Go to **Cloudflare Dashboard** → Workers & Pages → Create Application → Pages
2. Click **Connect to Git** → select the `BercuryAI` GitHub account → select `adaptedmachine-website`
3. Configure the build:
   - **Production branch:** `main`
   - **Build command:** *(leave empty — pure static)*
   - **Build output directory:** `/` (or `.`)
4. Deploy

Cloudflare will automatically generate a preview URL for every branch. The `staging` branch will get a URL like:
`https://staging.adaptedmachine-website.pages.dev`

---

## Step 3: Connect Your Domain

1. In Cloudflare Pages → your project → Custom Domains
2. Add `adaptedmachine.com` and `www.adaptedmachine.com`
3. Since the domain is already on Cloudflare, DNS records will be added automatically

---

## Step 4: Form Setup (Formspree)

1. Sign up at [formspree.io](https://formspree.io) with `jack@adaptedmachine.com`
2. Create a new form → copy your Form ID (looks like `xpwzjqkn`)
3. In `index.html`, find this line:
   ```html
   action="https://formspree.io/f/YOUR_FORM_ID"
   ```
4. Replace `YOUR_FORM_ID` with your actual ID
5. Commit and push to staging for testing, then to main to go live

---

## Step 5: Workflow Going Forward

```bash
# Make changes → push to staging first
git checkout staging
# (make edits)
git add . && git commit -m "update: ..."
git push origin staging
# → Review at staging preview URL

# When approved → merge to main (production)
git checkout main
git merge staging
git push origin main
```

---

## What's Left Before Launch

- [ ] Replace the `JB` initials placeholder with Jack's actual photo in the About section
  - Add `jack-berkery.jpg` to the folder
  - In `index.html`, replace the `about-photo-wrap` div with: `<img src="jack-berkery.jpg" alt="Jack Berkery">`
- [ ] Set up Formspree form ID (see Step 4 above)
- [ ] Review all copy with Taylor one more time
- [ ] Decide if client case study names can be revealed (currently anonymized)
- [ ] Confirm retainer pricing narrative before launch

---

## Design Notes

- **Colors:** Dark navy `#0A1628` + teal accent `#0FA3A3` + white
- **Font:** Inter (loaded from Google Fonts — no local install needed)
- **No frameworks** — pure HTML/CSS/JS, loads in under 1 second
- **Mobile responsive** — tested breakpoints at 640px and 900px
