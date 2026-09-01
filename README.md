# Camp registration front door

A front door for **Camp Miniwanca** and **Camp Merrowvista** — American Youth
Foundation summer camps. It welcomes families and captures a short lead
(camper name, age, camp, parent email) in about a minute, then hands off to
follow-up.

There are three versions, each a single self-contained file (all CSS,
JavaScript, and the logo are inlined — no build step, no asset paths):

| Page | File | What it is |
|------|------|------------|
| Both camps | [`index.html`](index.html) | Bright summer look, green buttons, families choose a camp in the form. |
| Camp Miniwanca | [`miniwanca/index.html`](miniwanca/index.html) | Blue-themed, single camp, no camp picker. |
| Camp Merrowvista | [`merrowvista/index.html`](merrowvista/index.html) | Teal-themed, single camp, no camp picker. |

The single-camp pages drop the "which camp?" step and lead with that camp's
color and content.

## Run it locally

Just open `index.html` in a browser, or serve the folder:

```bash
python3 -m http.server 8080
# then visit http://localhost:8080
```

## Host it on Render (free static site)

### Option A — Blueprint (uses `render.yaml`)

The blueprint publishes all three as separate free static sites:
`ayf-camp-registration` (both camps), `camp-miniwanca`, and `camp-merrowvista`.

1. Make sure this repo is on GitHub and the branch you want is pushed.
2. In the [Render dashboard](https://dashboard.render.com), click
   **New → Blueprint**.
3. Connect this repository. Render reads `render.yaml` and proposes the sites.
4. Pick the branch to deploy, then click **Apply**. Delete any of the three
   services you do not want before applying.

### Option B — Static Site (point and click)

1. Render dashboard → **New → Static Site**, connect this repo.
2. **Branch:** the branch you want to publish.
3. **Build command:** leave empty.
4. **Publish directory:** `.` for both camps, `miniwanca` for the Miniwanca
   page, or `merrowvista` for the Merrowvista page.
5. Click **Create Static Site**. Repeat for each version you want live.

Either way, Render gives you a free `https://<name>.onrender.com` URL with
automatic HTTPS, and redeploys on every push. You can add a custom domain
(for example a dedicated one per camp) under **Settings → Custom Domains**.

The both-camps site also serves the single-camp pages at `/miniwanca/` and
`/merrowvista/`, so you can share those paths without a second deploy.

## Collecting real leads

The form is in **demo mode**: it validates and shows the confirmation, but
nothing is stored or sent anywhere yet. A static host cannot run server code,
so to route real submissions somewhere, wire the form to an endpoint. In
`index.html`, find the comment `DEMO MODE — not collecting input yet` and
either:

- POST to a form service (Formspree, Getform, Basin), or
- POST to your CRM / email tool / registration platform API, or
- POST to a small companion web service (also hostable on Render).
