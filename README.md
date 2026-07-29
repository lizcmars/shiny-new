# Camp registration front door

A single-page front door for **Camp Miniwanca** and **Camp Merrowvista** —
American Youth Foundation summer camps. It welcomes families and captures a
short lead (camper name, age, camp, parent email) in about a minute, then
hands off to follow-up.

The entire page is one self-contained file, [`index.html`](index.html):
all CSS, JavaScript, and the logo are inlined, so it works anywhere that can
serve a static file — no build step, no asset paths.

## Run it locally

Just open `index.html` in a browser, or serve the folder:

```bash
python3 -m http.server 8080
# then visit http://localhost:8080
```

## Host it on Render (free static site)

### Option A — Blueprint (uses `render.yaml`)

1. Make sure this repo is on GitHub and the branch you want is pushed.
2. In the [Render dashboard](https://dashboard.render.com), click
   **New → Blueprint**.
3. Connect this repository. Render reads `render.yaml` and proposes a static
   site named `ayf-camp-registration`.
4. Pick the branch to deploy, then click **Apply**.

### Option B — Static Site (point and click)

1. Render dashboard → **New → Static Site**, connect this repo.
2. **Branch:** the branch you want to publish.
3. **Build command:** leave empty.
4. **Publish directory:** `.` (the repo root).
5. Click **Create Static Site**.

Either way, Render gives you a free `https://<name>.onrender.com` URL with
automatic HTTPS, and redeploys on every push. You can add a custom domain
under the site's **Settings → Custom Domains**.

## Collecting real leads

The form is in **demo mode**: it validates and shows the confirmation, but
nothing is stored or sent anywhere yet. A static host cannot run server code,
so to route real submissions somewhere, wire the form to an endpoint. In
`index.html`, find the comment `DEMO MODE — not collecting input yet` and
either:

- POST to a form service (Formspree, Getform, Basin), or
- POST to your CRM / email tool / registration platform API, or
- POST to a small companion web service (also hostable on Render).
