# Anvaya Spice Co. — landing page

A single static file (`index.html`). No build step, no server, no framework.
You can open it by double-clicking it right now to preview the design.

Before it can take real orders and track ads, do the three setup steps below.

---

## 1. Order capture (Web3Forms — already connected)

The checkout form sends orders through [Web3Forms](https://web3forms.com),
which is free for up to 250 submissions/month (Formspree's free tier is only
50/month) and needs no backend code.

Your access key is already in `index.html`:
```js
web3formsAccessKey: '5e39d341-89f8-4711-8549-d6e60811af68'
```

Every order emails you automatically at the address tied to that access key
on web3forms.com — check your inbox (and spam folder the first time) after
placing a test order once the site is live. If you ever need to rotate the
key or add a second one, generate it at web3forms.com and swap it in here.

If you outgrow 250/month, either upgrade Web3Forms or tell me and I'll wire
up a free, unlimited Google Sheets version instead — same file, different
backend, no rebuild.

## 2. Connect Meta Pixel (for ads)

1. Go to https://business.facebook.com/events_manager2, create a Pixel if you
   don't have one, and copy its **Pixel ID** (a long number).
2. Open `index.html` and replace **both** occurrences of `YOUR_PIXEL_ID`
   (one in the `<script>` tag, one in the `<noscript>` tag near the top)
   with your real Pixel ID.
3. The page already fires three standard events for you:
   - `PageView` — automatic, every visit
   - `InitiateCheckout` — when someone opens the delivery details form
   - `Purchase` — when an order is successfully placed (COD orders are
     tracked as Purchase since there's no separate payment step; if you'd
     rather Meta treat these as leads until you've called to confirm, say so
     and I'll switch this one event to `Lead`)
4. After deploying, install the **Meta Pixel Helper** Chrome extension,
   visit your live site, and confirm you see a green check for PageView.
   Place a test order and confirm Purchase fires too.

## 3. Deploy

### Option A — Vercel (recommended, easiest custom domain setup)
1. Push this folder to a new GitHub repository.
2. Go to https://vercel.com, sign in with GitHub, click **Add New → Project**,
   and import the repository.
3. Leave all settings as default (it's a static site — no framework, no
   build command needed) and click **Deploy**.
4. You'll get a live URL like `anvaya.vercel.app` within a minute.

### Option B — GitHub Pages (also free)
1. Push this folder to a GitHub repository.
2. In the repo, go to **Settings → Pages**.
3. Under **Source**, choose the branch (usually `main`) and folder `/root`,
   then save.
4. Your site goes live at `https://yourusername.github.io/repo-name`
   within a few minutes.

## 4. Add your custom domain

**On Vercel:**
1. In your project, go to **Settings → Domains**, type your domain
   (e.g. `anvayaspice.com`), and click **Add**.
2. Vercel shows you a DNS record to add (usually an A record or a CNAME).
   Log into wherever you bought the domain and add that record.
3. It usually goes live within 10–60 minutes.

**On GitHub Pages:**
1. In **Settings → Pages**, enter your custom domain under **Custom domain**
   and save — this creates a `CNAME` file in your repo automatically.
2. At your domain registrar, add a CNAME record pointing to
   `yourusername.github.io`, or the A records GitHub's docs list for apex
   domains.
3. Tick **Enforce HTTPS** once it's verified.

## Before you launch ads — checklist

- [ ] Placed one test order and confirmed the email from Web3Forms arrived
- [ ] Real Pixel ID added in both places, Pixel Helper shows PageView firing
- [ ] Placed a full test order on the *live* URL and watched Purchase fire
      in Meta Events Manager's **Test Events** tab
- [ ] Replaced the placeholder brand name, logo, product photos, price,
      and phone number (all marked `EDIT` in the code — see below)
- [ ] Custom domain resolving and showing a padlock (HTTPS)

## What to edit for your real brand

Search `index.html` for the word `EDIT` — every spot that needs your real
content is marked, including:
- Brand name/logo (currently text, swap for `<img>` once you have a logo file)
- The four product tiles (currently colored placeholders — swap each
  `.spice-art` div for an `<img>` of your real product)
- Price, market-price comparison, currency symbol (`CONFIG` object)
- Phone/WhatsApp number in the footer

Send me your logo, product photos, real brand name, and pricing whenever
you're ready and I'll drop them into the file for you.
