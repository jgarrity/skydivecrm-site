# skydivecrm.com — launch guide

A one-page landing site for Skydive CRM, built from the Skydive CRM Brand Board (Sora + Manrope, Midnight / Open Sky / Canopy Coral). Plain HTML, no build step.

```
index.html    the whole site (styles and script inline)
favicon.svg   browser tab icon
CNAME         tells GitHub Pages to serve at skydivecrm.com
assets/       spare folder for images, if you add any
```

## Step 1. Put the files on GitHub

1. Sign in at github.com and click **New repository**. Name it `skydivecrm-site`. Make it **Public** (GitHub Pages on a free account needs a public repo).
2. On the new repo page, click **uploading an existing file**, drag in everything from this folder (including `CNAME`), and click **Commit changes**.

## Step 2. Turn on GitHub Pages

1. In the repo, go to **Settings → Pages**.
2. Under **Build and deployment**, set Source to **Deploy from a branch**, Branch to **main**, folder **/ (root)**, then **Save**.
3. **Custom domain** should already read `skydivecrm.com` (from the CNAME file). If not, type it and save.
4. Within a minute or two the site is live at `https://<your-username>.github.io/skydivecrm-site/`. Check it there first.

## Step 3. Point skydivecrm.com at GitHub (IONOS)

In IONOS: **Domains & SSL → skydivecrm.com → DNS**.

1. Delete any existing **A** and **AAAA** records for `@` (IONOS adds parking records by default).
2. Add four **A** records, host `@`, one for each of these values:
   - `185.199.108.153`
   - `185.199.109.153`
   - `185.199.110.153`
   - `185.199.111.153`
3. Add (or edit) a **CNAME** record: host `www`, value `<your-username>.github.io`
4. DNS can take from a few minutes to a few hours. Back in **Settings → Pages**, wait for the DNS check to pass, then tick **Enforce HTTPS**.

Recommended: in your GitHub account **Settings → Pages → Add a domain**, verify `skydivecrm.com` with the TXT record GitHub gives you. That stops anyone else from claiming your domain on GitHub Pages.

## Step 4. Hook up the gated demo

GitHub Pages only serves files, so form submissions need a small outside service. Formspree is the simplest:

1. Create a form at formspree.io pointed at the inbox where you want leads. Copy its endpoint (looks like `https://formspree.io/f/abcdwxyz`).
2. Upload the full demo video somewhere you can share by link without listing it publicly (Vimeo or YouTube **unlisted**). Copy the link.
3. In `index.html`, near the bottom, fill in:
   ```js
   const FORM_ENDPOINT = "https://formspree.io/f/abcdwxyz";
   const FULL_DEMO_URL = "https://vimeo.com/your-unlisted-link";
   ```
4. Commit. Submit the form once yourself to confirm the lead arrives and the "Watch the full demo" button appears.

How the gate works: the visitor fills in name, work email, company, role, and Dynamics setup; you get the lead; they get the link on screen. It's a lead-capture gate, not a lock: anyone with the link can watch. If you later want to confirm emails are real, switch to emailing the link instead of revealing it.

## Step 5. Add the free teaser

Upload the teaser to YouTube or Vimeo. In `index.html`, find `TEASER VIDEO`, paste the embed `<iframe>` where the comment shows, and delete the `video-placeholder` div below it. Don't commit large video files to the repo itself.

## Step 6. Swap in the final logo

The mark lives in one place: the `<symbol id="mark">` near the top of `<body>`. Replace the shapes inside it (keep the same `viewBox` proportions, or update it) and the nav, hero, and footer all update. Update `favicon.svg` to match.

## Editing copy later

Edit `index.html` directly on GitHub (pencil icon) and commit. The live site updates in about a minute.

Placeholders still to fill: `[Account name]` / `[Opportunity name]` in the hero card, `[Teaser video goes here]`, and the two settings above.
