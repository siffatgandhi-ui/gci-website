# Publishing the GCI site

`index.html` is the whole website — one self-contained file. All images, CSS and
JavaScript are embedded. No build step, no server, no dependencies. Any static
host will serve it.

Keep `preview.jpg` next to it — that's the image shown when the link is pasted
into WhatsApp, LinkedIn or email.

---

## Fastest — Netlify Drop (about 30 seconds, no terminal)

1. Go to **https://app.netlify.com/drop**
2. Drag this whole `GCI_site_deploy` folder onto the page.
3. You get a public link immediately, e.g. `https://cheerful-otter-1a2b3c.netlify.app`

Without an account the link expires in about an hour. Sign up (free) and it
becomes permanent, and you can rename it to something like
`golden-choice-impex.netlify.app` under **Site settings → Change site name**.

## Cloudflare Pages — free, fast in India

1. **https://pages.cloudflare.com** → Create a project → *Upload assets*
2. Upload the folder. You get `your-project.pages.dev`.

## GitHub Pages

1. Create a repository, upload `index.html` and `preview.jpg`.
2. **Settings → Pages → Source: main branch / root**.
3. Live at `https://<username>.github.io/<repo>/` in a minute or two.

---

## Putting it on goldenchoiceimpex.com

Any of the hosts above can serve the real domain:

- **Netlify / Cloudflare Pages** → add a custom domain in the dashboard, then
  point the DNS record they give you at it.
- **Existing hosting** → whoever manages the current site can drop `index.html`
  and `preview.jpg` into the web root. That's the entire deployment.

Once the real domain is live, change this line in `index.html` to the full URL so
link previews resolve correctly:

    <meta property="og:image" content="preview.jpg">
    →
    <meta property="og:image" content="https://goldenchoiceimpex.com/preview.jpg">

---

## Before it goes live on the real domain

- **The enquiry form** opens the visitor's mail client (a `mailto:` link). It does
  not submit anywhere. For real form submissions, a service like Formspree or
  Netlify Forms takes about ten minutes to wire up.
- **Headcount** — the brochure says 386, the brand Q&A says 200+. The page
  currently says "380+ across the group". Confirm which is right.
- **The logo** on this page is a redrawn proposal, not the approved vector
  master. Get sign-off before it represents the company publicly.

---

## Editing later

Don't hand-edit `index.html` — the images are inlined as base64 and it's a
1 MB file. Edit the source instead:

    ~/Desktop/GCI_Website_v2_source-no-images.html   (52 KB, images are @@tokens@@)

then re-run the build script, which regenerates both this folder and the
shareable Claude artifact from that one source:

    python3 build.py
