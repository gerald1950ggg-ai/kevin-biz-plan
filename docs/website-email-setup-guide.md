# Miles of Tile Styles — Website & Email Setup Guide
**Domain + Hosting + Professional Email — All Free (Except the Domain)**

---

## Overview

This guide walks through setting up a professional website and business email for Miles of Tile Styles LLC. The entire stack costs ~$12/year (just the domain registration). Everything else is free.

### The Stack

| Component | Service | Cost | What It Does |
|---|---|---|---|
| Domain name | Domain.com or Namecheap | ~$10–15/year | Own `milesoftilestyles.com` |
| DNS + Email routing | Cloudflare (free plan) | $0 | Routes web traffic to GitHub, email to Gmail |
| Website hosting | GitHub Pages | $0 | Hosts the actual website files |
| Email inbox | Gmail (Kevin's existing) | $0 | Receives and sends email as `kevin@milesoftilestyles.com` |

### How It Works

```
Web visitor types milesoftilestyles.com
  → Cloudflare DNS receives the request
  → Routes to GitHub Pages (your website loads)

Someone emails kevin@milesoftilestyles.com
  → Cloudflare Email Routing receives it
  → Forwards to Kevin's personal Gmail inbox

Kevin replies from Gmail
  → Gmail sends it showing "kevin@milesoftilestyles.com" as the sender
  → Client never sees the personal Gmail address
```

### Domain Status

**`milesoftilestyles.com` is available** as of May 26, 2026. Register it before someone else does.

---

## Step 1: Buy the Domain

**Where:** Domain.com or Namecheap (either works)

1. Go to [domain.com](https://www.domain.com) or [namecheap.com](https://www.namecheap.com)
2. Search for `milesoftilestyles.com`
3. Purchase it (typically $10–15/year for a `.com`)
4. **Enable Domain Privacy** if offered (usually free or a few dollars) — keeps Kevin's personal address off the public WHOIS record
5. **Do NOT buy their email add-on** — we're using Cloudflare for free instead

**Save your registrar login credentials.** You'll need them in Step 3 to change nameservers.

---

## Step 2: Create a Cloudflare Account

1. Go to [cloudflare.com](https://www.cloudflare.com) and sign up (free)
2. Click **"Add a Site"** (or "Onboard a domain")
3. Enter `milesoftilestyles.com`
4. Select the **Free plan**
5. Cloudflare will scan for existing DNS records — let it finish
6. Cloudflare will give you **two nameservers** (they look like `name1.ns.cloudflare.com` and `name2.ns.cloudflare.com`)
7. **Write down or copy both nameserver addresses** — you need them in the next step

---

## Step 3: Point Domain to Cloudflare

1. Log back into your **domain registrar** (Domain.com or Namecheap)
2. Find the **Nameservers** or **DNS settings** section for your domain
3. Change the nameservers from the default ones to the **two Cloudflare nameservers** from Step 2
4. Save
5. Wait 15–60 minutes for propagation
6. Back in Cloudflare, your domain should show as **"Active"**

**What this does:** Cloudflare now controls all traffic for your domain. It decides where web visitors go and where emails go. This is what makes everything else possible.

---

## Step 4: Set Up Email Routing (Receive Email)

This lets people email `kevin@milesoftilestyles.com` and have it land in Kevin's Gmail.

1. In the Cloudflare dashboard, click on your domain (`milesoftilestyles.com`)
2. In the left sidebar, click **Email** → **Email Routing**
3. Click **"Get Started"** or **"Enable Email Routing"**
4. Cloudflare will offer to add MX and TXT records automatically — **accept** (click "Add records and enable")
5. Go to **Routing Rules** → click **"Create Address"**
6. Fill in:
   - **Custom address:** `kevin` (this creates `kevin@milesoftilestyles.com`)
   - **Action:** Send to an email
   - **Destination:** Kevin's personal Gmail address (e.g., `kevsbliss@icloud.com` or his Gmail)
7. Click **Save**
8. Cloudflare sends a **verification email** to Kevin's Gmail — **Kevin must click the verify link** in that email
9. Once verified, the rule goes active

**Optional — Catch-all:** You can also enable a catch-all rule so that ANY email sent to `@milesoftilestyles.com` (typos, `info@`, `hello@`, anything) gets forwarded to Kevin's Gmail. This is under the same Routing Rules page.

**Test it:** Send an email from any other account to `kevin@milesoftilestyles.com`. It should arrive in Kevin's Gmail within seconds.

---

## Step 5: Set Up Gmail "Send As" (Send Email)

This lets Kevin reply FROM `kevin@milesoftilestyles.com` using his Gmail. The client never sees his personal address.

### 5a: Create a Google App Password

Gmail requires a special "App Password" for this (regular password won't work if 2FA is enabled, which it should be).

1. Go to [myaccount.google.com](https://myaccount.google.com)
2. Click **Security** in the left sidebar
3. Make sure **2-Step Verification** is turned ON (if not, enable it first)
4. Search for **"App Passwords"** or go to: `myaccount.google.com/apppasswords`
5. Select **Mail** as the app
6. Click **Generate**
7. Google gives you a **16-character password** — **copy it and save it**, you'll need it in the next step

### 5b: Add the Custom Address in Gmail

1. Open Gmail
2. Click the **gear icon** (top right) → **See all settings**
3. Go to the **"Accounts and Import"** tab
4. Under **"Send mail as:"** click **"Add another email address"**
5. Fill in:
   - **Name:** Kevin Gardner (or "Miles of Tile Styles" — whatever Kevin wants recipients to see)
   - **Email address:** `kevin@milesoftilestyles.com`
   - Uncheck "Treat as an alias" (optional — either way works for this use case)
6. Click **Next Step**
7. Fill in SMTP details:
   - **SMTP Server:** `smtp.gmail.com`
   - **Port:** `587`
   - **Username:** Kevin's full Gmail address (e.g., `kevsbliss@gmail.com`)
   - **Password:** The 16-character App Password from Step 5a
   - **Encryption:** TLS (should be selected by default)
8. Click **Add Account**
9. Gmail sends a confirmation code to `kevin@milesoftilestyles.com` — since Cloudflare is already forwarding email, this will land in Kevin's Gmail
10. Enter the confirmation code or click the link in the email

**Done.** Now when Kevin composes a new email or replies, he can select `kevin@milesoftilestyles.com` in the "From" dropdown. Replies to business emails will auto-fill with the business address.

### 5c: Make It the Default (Optional)

In Gmail → Settings → Accounts and Import → Send mail as, click **"make default"** next to the `kevin@milesoftilestyles.com` address. Now all outgoing email defaults to the business address.

---

## Step 6: Set Up the Website on GitHub Pages

We already have a GitHub repo (`gerald1950ggg-ai/kevin-biz-plan`) with the website files. We just need to connect the custom domain.

### 6a: Add Custom Domain in GitHub

1. Go to the repo: `github.com/gerald1950ggg-ai/kevin-biz-plan`
2. Click **Settings** → **Pages** (left sidebar)
3. Under **"Custom domain"**, enter `milesoftilestyles.com`
4. Click **Save**
5. Check **"Enforce HTTPS"** (GitHub provides free SSL)

### 6b: Add DNS Records in Cloudflare

1. In Cloudflare dashboard → your domain → **DNS** → **Records**
2. Add an **A record** for the apex domain:
   - **Type:** A
   - **Name:** `@`
   - **Content:** `185.199.108.153`
   - **Proxy status:** DNS only (gray cloud)
3. Add three more A records (GitHub Pages uses 4 IPs):
   - `185.199.109.153`
   - `185.199.110.153`
   - `185.199.111.153`
4. Add a **CNAME** for `www`:
   - **Type:** CNAME
   - **Name:** `www`
   - **Content:** `gerald1950ggg-ai.github.io`
   - **Proxy status:** DNS only (gray cloud)
5. Add a CNAME file to the repo (Gerald handles this)

### 6c: Add SPF Record for Outgoing Email

To make sure Kevin's outgoing emails don't get flagged as spam:

1. In Cloudflare DNS, find the existing TXT/SPF record that Cloudflare added for email routing
2. Update it to include Google's servers:
   - **Type:** TXT
   - **Name:** `@`
   - **Content:** `v=spf1 include:_spf.mx.cloudflare.net include:_spf.google.com ~all`

### 6d: Add DMARC Record

1. In Cloudflare DNS, add:
   - **Type:** TXT
   - **Name:** `_dmarc`
   - **Content:** `v=DMARC1; p=none; rua=mailto:kevin@milesoftilestyles.com`

**Wait 15–30 minutes** for DNS to propagate, then visit `milesoftilestyles.com` — your website should load.

---

## Step 7: Test Everything

Run through this checklist:

- [ ] Visit `milesoftilestyles.com` in a browser — website loads
- [ ] Visit `www.milesoftilestyles.com` — also loads (redirects to main domain)
- [ ] The URL shows a padlock icon (HTTPS/SSL working)
- [ ] Send an email to `kevin@milesoftilestyles.com` from any outside account — arrives in Kevin's Gmail
- [ ] Reply from Gmail using the business address — recipient sees `kevin@milesoftilestyles.com` as sender
- [ ] Compose a new email from Gmail, select `kevin@milesoftilestyles.com` in the "From" dropdown — sends correctly

---

## Important Notes

### What This Setup Can Do
- Receive unlimited emails at `kevin@milesoftilestyles.com`
- Send emails that show `kevin@milesoftilestyles.com` as the sender
- Create additional addresses (`info@`, `hello@`, etc.) all forwarding to the same Gmail
- Host a fast, mobile-friendly website with free SSL
- Free CDN through Cloudflare (website loads fast worldwide)

### One Limitation
- **No DKIM signing** for the custom domain on free Gmail. DKIM is a cryptographic signature that proves the email came from your domain. Google Workspace ($7/mo) adds this. For Kevin's use case (replying to clients and designers one-to-one), SPF alone is sufficient. Emails will deliver fine. This only matters for bulk/cold email, which Kevin isn't doing.

### Ongoing Costs
- Domain renewal: ~$10–15/year
- Everything else: $0, forever

### If Kevin Outgrows This Setup
- **More email features needed?** → Google Workspace ($7/mo) adds DKIM, calendar, Drive, the works
- **Website needs a CMS?** → Migrate to a template platform but keep the same domain/Cloudflare setup
- **Multiple team members need email?** → Add more routes in Cloudflare (free) or upgrade to Workspace

---

## Quick Reference Card

| What | Where | Login |
|---|---|---|
| Domain registration | Domain.com or Namecheap | _(Kevin's credentials)_ |
| DNS + Email routing | cloudflare.com | _(Kevin's credentials)_ |
| Website files | github.com/gerald1950ggg-ai/kevin-biz-plan | _(Gerald manages)_ |
| Email inbox | Gmail | _(Kevin's existing Gmail)_ |

**Support contact:** Marcus or Gerald for any setup questions.
